# 指针（Pointer）
## 目录（Catalog）
1.[简介](#%E7%AE%80%E4%BB%8Bbrief-introduction)</br>
2.[声明](#%E5%A3%B0%E6%98%8Edeclaration)</br>
3.[初始化](#%E5%88%9D%E5%A7%8B%E5%8C%96initialization)</br>
4.[使用](#%E4%BD%BF%E7%94%A8use)</br>
5.[注意](#%E6%B3%A8%E6%84%8Fattention)</br>
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
