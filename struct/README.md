# 结构体（Struct）
## 目录（Catalog）
1.[定义类型](#定义类型def-type)</br>
2.[声明](#声明declaration)</br>
3.[初始化](#%初始化initialization)</br>
4.[引用](#引用use)</br>
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
