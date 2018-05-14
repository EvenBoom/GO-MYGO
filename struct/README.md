# 结构体（Struct）
## 目录（Catalog）
1.[定义类型](https://github.com/EvenBoom/GO-MYGO/blob/master/struct/README.md#%E5%AE%9A%E4%B9%89%E7%B1%BB%E5%9E%8Bdef-type)<\br>
2.[声明](https://github.com/EvenBoom/GO-MYGO/blob/master/struct/README.md#%E5%A3%B0%E6%98%8E)<\br>
3.[初始化](https://github.com/EvenBoom/GO-MYGO/blob/master/struct/README.md#%E5%88%9D%E5%A7%8B%E5%8C%96)<\br>
4.[引用](https://github.com/EvenBoom/GO-MYGO/blob/master/struct/README.md#%E5%BC%95%E7%94%A8)<\br>
## 定义类型（Def-type）
```
type person struct {
	id        string
	name      string
}
```
## 声明
```
var p Person
```
## 初始化
```
p := person{
	name: "goer",
}
```
## 引用
```
fmt.Println(p.name)
```
