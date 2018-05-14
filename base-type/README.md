# 基础类型（base-type）
## 目录（Catalog）
1.[string](https://github.com/EvenBoom/GO-MYGO/blob/master/base-type/README.md#%E5%88%9D%E5%A7%8B%E5%8C%96)
2.[int]
## string
### 声明
var s string
### 初始化
s="init"
### 声明并初始化
1.var s string = "init"</br>
2.s := "init"
## int
### 分类
int（有符号,长度取决于CPU,至少32位）</br>
int8,int16,int32,int64（有符号,固定长度）</br>
uint（无符号,长度取决于CPU,至少32位）</br>
uint8,uint16,uint32.uint64（无符号，固定长度）</br>
### 声明
var n int</br>
----------------------------
var n int8</br>
var n int16</br>
var n int32</br>
var n int64</br>

var n uint</br>
----------------------------
var n uint8</br>
var n uint16</br>
var n uint32</br>
var n uint64</br>
### 初始化
var n int = 0&nbsp;&nbsp;&nbsp;or n:=0</br>
----------------------------
var n int8 = 0</br>
var n int16 = 0</br>
var n int32 = 0</br>
var n int64 = 0</br>

var n uint = 0</br>
----------------------------
var n uint8 = 0</br>
var n uint16 = 0</br>
var n uint32 = 0</br>
var n uint64 = 0</br>
