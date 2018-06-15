# sync
## 简介（Brief-introduction）
sync是一个同步包，里面定义了与同步相关的一些操作
## 目录（Catalog）
1.[WaitGroup](#waitgroup)</br>
2.[Pool](#pool)</br>
3.[Once](#once)</br>
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
	wg.Add(1)
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
