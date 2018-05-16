# 基础类型（Base-type）
## 目录（Catalog）
1.[string](https://github.com/EvenBoom/GO-MYGO/blob/master/base-type#string)</br>
2.[int](https://github.com/EvenBoom/GO-MYGO/blob/master/base-type#int)</br>
3.[float](https://github.com/EvenBoom/GO-MYGO/blob/master/base-type#float)</br>
## string
### 声明（Declaration）
```
var s string
```
### 初始化（Initialization）
```
var s string = "init" // s := "init"
```
## int
### 分类（Type）
1.int（有符号,长度取决于CPU,至少32位）</br>
2.int8,int16,int32,int64（有符号,固定长度）</br>
3.uint（无符号,长度取决于CPU,至少32位）</br>
4.uint8,uint16,uint32.uint64（无符号，固定长度）</br>
### 声明（Declaration）
int
-----------------------------------
```
var n int
var n int8
var n int16
var n int32
var n int64
```
unt
-----------------------------------
```
var n uint
var n uint8
var n uint16
var n uint32
var n uint64
```
### 初始化（Initialization）
int
-----------------------------------
```
var n int = 0 // n:=0
var n int8 = 0
var n int16 = 0
var n int32 = 0
var n int64 = 0
```
uint
-----------------------------------
```
var n uint = 0
var n uint8 = 0
var n uint16 = 0
var n uint32 = 0
var n uint64 = 0
```
## float
### 分类（Type）
1.float32</br>
2.float64</br>
### 声明（Declaration）
```
var f float32
var f float64
```
### 初始化(Initialization)
```
var f float64 = 0 // f:=0.0
var f float32 = 0
```
