# 远程调用（RPC）
# 目录
# 简介
golang的rpc是通过http协议进行的
# 简单例子
```
//服务端
package main

import (
	"net/http"
	"net/rpc"
)

func main() {
	my := new(MyNum)
	rpc.Register(my)
	rpc.HandleHTTP()
	http.ListenAndServe(":8088", nil)
}

type MyNum int

func (my *MyNum) Sum(args [2]int, reply *int) error {
	*reply = args[0] + args[1]
	return nil
}

//客户端
package main

import (
	"fmt"
	"net/rpc"
)

func main() {
	var reply int
	client, _ := rpc.DialHTTP("tcp", "127.0.0.1:8088")
	args := [2]int{1, 2}
	client.Call("MyNum.Sum", args, &reply)
	fmt.Println(reply)
}

```
