# 切片（Slice）
## 目录（Catalog）
1.[简介](#简介brief-introduction)</br>
2.[声明](#declaration)</br>
3.[初始化](#initialization)</br>
## 简介（Brief-introduction)
切片可以理解为数组里的片段。
## 声明（Declaration）
```
var a []int
```
## 初始化（Initialization）
```
var a []int
a = make([]int, 2, 4)//第1个参数是类型，第2个参数是长度，第3个参数是容量, 所有的值都初始为0

a := make([]int, 2, 4)

a := []int{1, 2, 3, 4}
```
