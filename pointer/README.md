# 指针（Pointer）
## 目录（Catalog）
1.[简介](#简介brief-introduction)</br>
2.[声明](#声明declaration)</br>
3.[初始化](#初始化initialization)</br>
4.[使用](#使用use)</br>
5.[注意](#注意attention)</br>
## 简介（Brief-introduction）
指针并不存储数据，而是存储数据的内存地址。</br>
指针指向的数据改变时，目标数据也会改变。</br>
## 声明（Declaration）
```
var pointer *int
var pointer *float64
var pointer *string
var pointer *person
```
## 初始化（Initialization）
```
n:=0
var np *int=&num

f:=0.0
var fp *float=&f

s:="string"
var sp *string=&s

p:=person{
  name:"Boom"
}
var pp *person=&p
```
## 使用（Use）
```
fmt.Println(*np)
fmt.Println(*fp)
fmt.Println(*sp)
fmt.Println(pp.name)//fmt.Println((*pp).name)//fmt.Println(*(&pp.name))
```
## 注意（Attention）
1.struct类型可以省略\*号</br>
2.指针作为参数传递是可以改变原内存地址上的数据，而不用指针则是复制一份参数传递过去，明显使用指针可以使资源消耗更小</br>
