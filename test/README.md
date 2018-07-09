# 单元测试
## 目录
1.[简介](#简介)
2.[例子](#例子)
## 简介
单元测试在http测试中显得非常重要，如果没有单元测试，你每次的测试就要启动服务器，这是非常麻烦的，如果后台代码量比较大，则会出现每次测试都要花很长时间，效率是非常低。注意：命名例子：如http.go的测试类http_test.go，testGo()的测试方法名Test_testGo(t *testing.T)
## 方法单元测试例子
```
//要测试的方法
func testGo() {
	fmt.Println("Testing!")
}

//单元测试类
package testgo

import (
	"fmt"
	"testing"
)
//最简单的例子
package testgo

import (
	"testing"
)

func Test_testGo(t *testing.T) {

	testGo()

}
//标准的例子
func Test_testGo(t *testing.T) {
	tests := []struct {
		name string
	}{
		{"name"},//case
	}

	for _, test := range tests {
		t.Run(test.name, func(t *testing.T) {
			testGo()
			fmt.Println(test.name)
		})
	}
}

```
## http测试例子
测试http的中间件
```
package main

import (
	"fmt"
	"log"
	"net/http"
)
//中间件类
func main() {
	mux := http.NewServeMux()
	mux1 := middleware1(mux)
	mux2 := middleware2(mux1)
	mux.HandleFunc("test", test)
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
		fmt.Println("test before")
		w.Write([]byte("before1 "))
		next.ServeHTTP(w, req)
		w.Write([]byte(" after1"))
		fmt.Println("test after")
	})
}

func middleware2(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, req *http.Request) {
		w.Write([]byte("before2 "))
		next.ServeHTTP(w, req)
		w.Write([]byte(" after2"))
	})
}

func test(w http.ResponseWriter, req *http.Request) {
	fmt.Println("just do it")
	w.Write([]byte("just do it"))
}
//测试类
package main

import (
	"net/http"
	"net/http/httptest"
	"testing"
)

func Test_test(t *testing.T) {
	req := httptest.NewRequest("GET", "/test", nil)
	recorder := httptest.NewRecorder()
	h := middleware1(http.HandlerFunc(test))
	h.ServeHTTP(recorder, req)
}

```

