# 结构体（Struct）
## 目录（Catalog）
1.[定义类型](#%E5%AE%9A%E4%B9%89%E7%B1%BB%E5%9E%8Bdef-type)</br>
2.[声明](#%E5%A3%B0%E6%98%8Edeclaration)</br>
3.[初始化](#%E5%88%9D%E5%A7%8B%E5%8C%96initialization)</br>
4.[引用](#%E5%BC%95%E7%94%A8use)</br>
## 定义类型（Def-type）
```
type person struct {
	id        string
	name      string
}
```
## 声明（Declaration）
```
var p Person
```
## 初始化（Initialization）
```
p := person{
	name: "goer",
}

var p = person{
	name: "goer",
}
```
## 引用（Use）
```
fmt.Println(p.name)
```
