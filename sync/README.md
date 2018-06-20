# sync
## 简介（Brief-introduction）
sync是一个同步包，里面定义了与同步相关的一些操作
## 目录（Catalog）
1.[WaitGroup](#waitgroup)</br>
2.[Pool](#pool)</br>
3.[Once](#once)</br>
4.[Mutex](#mutex)</br>
5.[RWMutex](#rwmutex)</br>
6.[Cond](#cond)</br>
7.[Map](#map)</br>
## WaitGroup
估计大家刚接触golang时都会遇到一个奇怪的问题，就是在main函数中使用goroutine没反应，这是因为协程还没走完，主线程就结束了</br>
WaitGroup就解决这个问题，WaitGroup可以阻塞主线程直到所有协程走完，主要三个方法Wait()，Add(int)和Done()
```
package main

import (
	"fmt"
	"sync"
)

//注意wg最后必须为0，大于0会造成死锁，小于0报错
var wg sync.WaitGroup

func main() {
	wg.Add(1)//Add和Wait函数必须在同一协程，否则会出现莫名的问题
	go hello()
	wg.Wait()//阻塞主线程，直到wg里的值为0
	fmt.Println("done!")
}

func hello() {
	fmt.Println("Hello World!")
	wg.Done()//等价于wg.Add(-1)
}

```
## Pool
sync.Pool设计的目的是提高临时对象的利用，减少GC压力，提高性能。因为sync.Pool存储临时对象时是分私有对象和共享对象数组，若存在私有对象，是提取私有对象，如若不存在，是需要到共享对象数组那提取，而获取共享对象数组是需要竞争锁的，所以使用sync.Pool也是需要消耗锁的性能的。</br>
sync.Pool主要的使用场景是初始化临时对象，用完再释放对象里的内容，然后Put进去。所以对象一定是要用完就扔（和小程序一样的感觉），而且每次都会创建这样一个对象的时候就可以使用。
```
type person struct {
	name string
	age  int
}

var personPool = sync.Pool{
	New: func() interface{} {
		return new(person)
	},
}

func takePerson() *person {
	return personPool.Get().(*person)
}

func freePerson(p *person) {
	p.name = ""
	p.age = 0
	personPool.Put(p)
}

func main() {
	p := takePerson()
	p.name = "john"
	p.age = 25
	fmt.Println(p.name + ":" + strconv.Itoa(p.age))
	freePerson(p)
}
```
## Once
sync.Once可以让一个无参数无返回值的函数只执行一次
```
package main

import (
	"fmt"
	"sync"
)

func main() {
	once.Do(f)
	once.Do(f)
}

var once sync.Once

func f() {
	fmt.Println("I just run once!")
}
```
## Mutex
sync.Mutex是一个互斥锁，一个锁只允许其中一个线程进入，直到解锁后才能允许其它线程获得锁，继承了sync.Locker接口，有Lock()方法和Unlock()方法
```
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup
var l sync.Mutex

func main() {
	wg.Add(8)
	go increase()
	go increase()
	go increase()
	go increase()
	go increase()
	go increase()
	go increase()
	go increase()
	wg.Wait()
}

var i int
//加锁后结果0,1,2,3,4,5,6,7
//不加锁的结果每次运行不太一样
func increase() {
	l.Lock()
	fmt.Println(i)
	i++
	l.Unlock()
	wg.Done()
}

```
## RWMutex
RWMutex读写锁，与输入输出流无关，不要混淆，获取了写锁的线程会排斥其它加了读或者写的线程，获取了读锁的线程会排斥其它加了写锁的线程（实际生产中要注意读锁还没解锁又被另一个读锁锁住了，导致写锁一直无法获取直至读锁全部解锁后才能获取的问题，这个发生概率还是很大的），下面的例子如果start到end中都没有出现一个锁的内容就表示和另一个锁是互斥的
```
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup
var l sync.RWMutex
var m sync.Mutex//加互斥锁是为了测试互斥锁和读写锁是不会相互影响的

func main() {
	wg.Add(24)
	go readS("Ra")
	go writeS("Wa")
	go readS("Rb")
	go writeS("Wb")
	go readS("Rc")
	go writeS("Wc")
	go readS("Rd")
	go writeS("Wd")
	go mutex("Ma")
	go mutex("Mb")
	go mutex("Mc")
	go mutex("Md")
	go readS("Re")
	go readS("Rf")
	go readS("Rg")
	go readS("Rh")
	go writeS("We")
	go writeS("Wf")
	go writeS("Wg")
	go writeS("Wh")
	go mutex("Me")
	go mutex("Mf")
	go mutex("Mg")
	go mutex("Mh")
	wg.Wait()
}

func readS(s string) {

	l.RLock()
	fmt.Println("read start")
	fmt.Println(s)
	fmt.Println("read end")
	l.RUnlock()
	wg.Done()
}

func writeS(s string) {
	l.Lock()
	fmt.Println("write start")
	fmt.Println(s)
	fmt.Println("write end")
	l.Unlock()
	wg.Done()
}

func mutex(s string) {
	m.Lock()
	fmt.Println("m start")
	fmt.Println(s)
	fmt.Println("m end")
	m.Unlock()
	wg.Done()
}

```
## Cond
sync.Cond是用来阻塞协程，唤醒协程的一个struct，sync.NewCond方法是创建一个sync.Cond类，参数是锁的地址，即需要加&符号。Wait方法是阻塞协程并等待唤醒，Signal是唤醒一个协程，Broadcast是全部唤醒。</br>
1.生产者-消费者例子
```
package main

import (
	"fmt"
	"sync"
)

var mu sync.Mutex
var cond *sync.Cond
var num int
var wg sync.WaitGroup

func main() {
	num = 5
	cond = sync.NewCond(&mu)
	for i := 0; i < 100; i++ {
		wg.Add(2)
		go minusOne()
		go addOne()
	}
	wg.Wait()
	fmt.Println(num)
}
//消费者
func minusOne() {
	cond.L.Lock()
	for num <= 0 {
		cond.Wait()
	}
	num--
	cond.L.Unlock()
	cond.Broadcast()
	wg.Done()
}
//生产者
func addOne() {
	cond.L.Lock()
	for num >= 10 {
		cond.Wait()
	}
	num++
	cond.L.Unlock()
	cond.Broadcast()
	wg.Done()
}
```
## Map
因为map是非线程安全的，所以sync.Map提供了线程安全的解决方法，里面的方法很简单，就不列举出来了
