# 恐慌
1.简介</br>
有了error为什么还要panic?这个问题挺困扰我的，我的理解就是panic是必须要这样做，但你没这样做，我就给你一个panic，告诉你不这样做后面程序很有可能出问题或者一定出问题，如空指针，数组越界等等。error是程序运行时可能会发生的问题，如断网等等。</br>
2.例子</br>
```
func testPanic() {
	panic("have a panic")
}
```
3.恢复</br>

```
package main

import (
	"fmt"
)

func main() {
	testPanic()
	fmt.Println("continue")
}
//发生panic的地方即使recover也不能继续执行panic下面的代码，也就是说这个函数结束了
func testPanic() {
	defer testRecover()//必须用defer，而且recover()不能单独用，需要包装成方法，原理是defer在panic发生时阻止其传递。
	panic("have a panic")
}

func testRecover() {
	if err := recover(); err != nil {
		fmt.Println(err)
	}
	fmt.Println("recover")
}
```
