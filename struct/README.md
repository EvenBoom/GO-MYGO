# 结构体（Struct）
## 目录（Catalog）
1.[定义类型](#定义类型def-type)</br>
2.[声明](#声明declaration)</br>
3.[初始化](#初始化initialization)</br>
4.[使用](#使用use)</br>
5.[继承](#继承inherit)
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
## 使用（Use）
```
fmt.Println(p.name)
```
## 继承（Inheritance）
继承既继承了字段，同时也继承了方法
```
type mystruct1 struct {
	s string
}

type mystruct2 struct {
	mystruct1
}

func (s *mystruct1) myfunc() string {
	return "Make it for mystruct1!"
}

func (s *mystruct2) myfunc() string {//重写方法，覆盖父对象的方法
	return "Make it for mystruct2!"
}
```
注意：golang并没有重载机制
