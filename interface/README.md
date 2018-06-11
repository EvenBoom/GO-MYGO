# 接口（Interface）
## 目录（Catalog）
1.[简介](#简介brief-introduction)</br>
2.[定义](#定义def)</br>
3.[实现](#实现implement)</br>
4.[多态](#多态polymorphism)</br>
4.[空接口](#空接口nil-interface)</br>
## 简介（Brief-introduction）
接口是一堆方法的集合
## 定义（Def）
```
type myInterface interface {
	myfunc()
}
```
## 实现（Implement）
实现接口就是实现接口里面的所有方法，和继承方法一样，实现方法需要接收者（方法名字前面括号的内容）
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
## 多态（Polymorphism）
接口多态就是接口引用对象，同一个接口可以由不同类型的对象实现
```
var mi myInterface = new(mystruct1)
var mi myInterface = new(mystruct2)
```
## 空接口（Nil-interface）
空接口里面没有方法，所以空接口会被所有对象实现，因此空接口被经常用来表示任何类型，最经典的例子Json
```
var myJson map[string]interface{}
```
