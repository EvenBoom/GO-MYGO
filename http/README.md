# http
## 目录
## 简介
http包是处理http网络的一个包，很多人对http协议不了解，其实http协议是基于在tcp协议上的协议，有空可以用一个tcp去获取http的内容，你就可以了解到http协议是什么，主要包含header和body两部分。另外经常有人问http是长连接还是短连接这样的面试题，我觉得问这种问题的人都是不合格的面试官，因为这是要看http版本的，而且是可以设置的，对于我这种记忆力很差又内向的人，经常面试失败的原因就是面试官喜欢问细节，而且他自己也没搞懂，叫我情何以堪，我决定以后真要换工作的话我是不再接受问技术细节问题的，最多不再从事这行，当是爱好玩玩，像这种搜索引擎就能找到答案的问题我从来不去记忆。话题扯远了，现在http已经从http1.0->http1.1->http2.0了，http2.0多路复用和服务端主动推送将减少连接数和请求数，对速度有了不错的提升，可惜目前普及不多。另外学习这个包时看到cgi技术，目前好像是很老的技术了，已经很难再看到了，有空可以研究下，毕竟web服务器的配置有时还是可以看到这个东东，jsp，asp也是基于cgi的，不过现在都是前后分离了，json才是好东东。
## 简单启用http服务
来个官方例子，非常简单方便
```
// A trivial example server is:
//
package main

import (
	"io"
	"log"
	"net/http"
)

// hello world, the web server
func HelloServer(w http.ResponseWriter, req *http.Request) {
	io.WriteString(w, "hello, world!\n")
}

func main() {
	http.HandleFunc("/hello", HelloServer)
	log.Fatal(http.ListenAndServe(":12345", nil))
}

```
## Handler
下面是golang的源码，从中可以看出Handler是一个接口，仅声明了一个函数ServeHTTP，http处理函数是通过实现Handler来完成的。
```
type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
```
http.Handle和http.HandleFunc这两个函数都是匹配路由和处理函数，并且第1个参数都是路由，不过http.Handle第2个参数是Handler，http.Handler第2个参数是func(ResponseWriter, *Request)。
## ServeMux
ServeMux是匹配路由和Handler的管理器，本质也是一个Handler。</br>
在我们使用http.ListenAndServe函数时，第二个参数往往是nil，这样我们就会使用默认的ServeMux，即DefaultServeMux。</br>
```
package main

import (
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.Handle("/hello", hello(func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("Hello World!!!"))
	}))
	http.ListenAndServe(":8080", mux)
}

type hello func(w http.ResponseWriter, r *http.Request)

func (h hello) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	h(w, r)
}
```
## 获取请求参数
```
package main

import (
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/post", func(w http.ResponseWriter, r *http.Request) {
		v := r.FormValue("key")//获取url参数和body参数，若url参数和body参数key相同，优先获取body的参数
		//v := r.PostFormValue("key")//获取body参数，仅限POST，PUT，PATCH
		//v := r.URL.Query().Get("key")//获取url参数
		w.Write([]byte(v))
	})
	http.ListenAndServe(":8080", mux)
}

type hello func(w http.ResponseWriter, r *http.Request)

func (h hello) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	h(w, r)
}
```
注意：若要DELETE方法也能获取到body参数，必须修改golang源码，需要修改request.go中的ParseForm函数，在r.Method==...后面加上||r.Method=="DELETE"
## 中间件（Middleware）
```
package main

import (
	"log"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux1 := middleware1(mux)//中间件第一层
	mux2 := middleware2(mux1)//中间件第二层
	mux.HandleFunc("/test1", func(w http.ResponseWriter, req *http.Request) {
		// io.WriteString(w, "test1")
		w.Write([]byte("test1"))
	})
	mux.HandleFunc("/test2", func(w http.ResponseWriter, req *http.Request) {
		// io.WriteString(w, "test2")
		w.Write([]byte("test2"))
	})
	log.Fatal(http.ListenAndServe(":8080", mux2))
}

func middleware1(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, req *http.Request) {
		w.Write([]byte("before1 "))
		next.ServeHTTP(w, req)
		w.Write([]byte(" after1"))
	})
}

func middleware2(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, req *http.Request) {
		w.Write([]byte("before2 "))
		next.ServeHTTP(w, req)
		w.Write([]byte(" after2"))
	})
}

```
## 其它
这里有篇[文章](https://studygolang.com/articles/2680)可以看下，有时需要查询某些函数用法可以参考这篇文章

