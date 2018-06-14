# 协程（goroutine）
## 简介（Brief-introduction）
goroutine是在语言层级实现的线程，比系统的线程更轻
## 使用（Use）

```
func main() {
  go hello()
}

func hello() {
	fmt.Println("Hello World!")
}
```
