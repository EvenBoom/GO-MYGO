# sync
## 简介（Brief-introduction）
sync是一个同步包，里面定义了与同步相关的一些操作
## 目录（Catalog）
1.[WaitGroup](#WaitGroup)
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
