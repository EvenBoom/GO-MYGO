# 数组（Array）
## 目录（Catalog）
1.[声明](#声明declaration)</br>
2.[初始化](#初始化initialization)</br>
3.[使用](#使用use)</br>
## 声明（Declaration）
```
var a [2]int
```
## 初始化（Initialization）
```
var a = [2]int{1, 2}
a := [2]int{1, 2}
var a = [...]int{1, 2}//...可以自己判断长度
a := [...]int{1, 2}//...可以自己判断长度
```
## 使用（Use）
```
var a = [2]int{1, 2}
fmt.Println(a[0])
```

