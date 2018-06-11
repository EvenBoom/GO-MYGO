# 接口（Interface）
## 目录（Catalog）
1.[简介](#简介)</br>
2.[定义](#定义)</br>
3.[实现](#实现)</br>
4.[多态](#多态)</br>
4.[空接口](#空接口)</br>
## 简介
接口是一堆方法的集合
## 定义
```
type myInterface interface {
	myfunc()
}
```
## 实现
实现接口就是实现接口里面的所有方法
```
type myInterface interface {
	myfunc1() string
	myfunc2()
}

type mystruct struct {
}

func (s *mystruct) myfunc1() string {
	return "Make it!"
}

func (s *mystruct) myfunc2() {

}
```
## 多态
接口多态就是接口引用对象，同一个接口可以由不同类型的对象实现
```
var mi myInterface = new(mystruct1)
var mi myInterface = new(mystruct2)
```
## 空接口
空接口里面没有有方法，所以空接口会被所有对象实现，所以空接口被经常用来表示任何类型，最经典的例子Json
```
var myJson map[string]interface{}
```
