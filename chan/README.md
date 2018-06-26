# 信道（chan）
## 目录（Catalog）
1.[简介](#简介brief-introduction)</br>
2.[声明](#声明declaration)</br>
3.[初始化](#初始化initialization)</br>
4.[缓冲信道](#缓冲信道buffered-channel)</br>
5.[Range-and-close](#range-and-close)</br>
6.[Select](#select)</br>
## 简介（Brief-introduction）
信道就是通道，官方翻译是信道。chan可以用来阻塞线程，用来代替锁，官方建议用chan来替代锁。
## 声明（Declaration）
```
var cs chan string//双向信道
var cs <-chan string//单向信道，只能从信道中接收数据
var cs chan<- string//单向信道，只能从发送数据到信道中
```
注意：单向信道一般用于协程的函数参数，避免coder犯错。
## 初始化（Initialization）
```
c := make(chan string)//c=make(chan string)
```
## 缓冲信道（Buffered-channel）
在使用make初始化时加入缓冲长度就会初始化为一个带缓冲的信道。
```
c:=make(chan string,10)
```
注意：向缓冲信道发送数据时需要缓冲长度填满才会阻塞，接收缓冲信道发来的数据时需要缓冲区为空才会阻塞。
```
c := make(chan bool, 2)//如果不是缓冲信道会报错，出现deadlock
c <- true
//c <- true
//c <- true  //这里会导致deadlock，因为超出缓冲信道的缓冲长度
go block(c)

func block(c chan bool) {
	result := <-c
	fmt.Println(result)
}
```
## Range-and-close
range可以不断让信道接收数据，直到信道被关闭。</br>
close可以用来关闭信道。</br>
注意：只有发送者可以关闭信道，因为关闭了信道后若继续发送数据会引发恐慌。</br>
```
c := make(chan bool, 2)
go block(c)
c <- true
c <- true
c <- true
c <- true
close(c)//通常情况下不用关闭，这里关闭是为了终止block函数里的range循环
c <- true//关闭后发送数据会引发恐慌

func block(c chan bool) {
	for result := range c {
		fmt.Println(result)
	}
}
```
## Select
select语句可以解决一个协程里多个chan等待的处理，都准备好会随机选一个执行。
```
c1 := make(chan string, 10)
c2 := make(chan string, 10)
go block(c1, c2)

c1 <- "I am c1!"
c2 <- "I am c2!"


func block(c1, c2 chan string) {
	var s string
	for {
		select {
		case s = <-c1:
			fmt.Println(s)
		case s = <-c2:
			fmt.Println(s)
		}
	}
}

```
