# 函数（Function）
## 目录（Catalog）
1.[定义函数](#定义函数)</br>
2.[参数](#参数)</br>
3.[返回值](#返回值)</br>
## 定义函数
```
func f(){
  
}
```
## 参数
```
//一个参数
func f(n int){
  
}

//参数为函数
func f(f func(i int,j int) int){//i，j可以省略
  fmt.Println(f.(1,2))
}

//参数为通道
func f(c chan int){

}

//不同类型参数
func f(n int,s string){
  
}

//同类型参数
func f(n1, n2 int){
  
}

//不定参数
func f(args ...interface{}){
  //...为不定参数，args为slice
  for n, v:= range args{
    //转成指针，需要参数传地址，如&addr
    s := v.(*string)
    *s = "make it"
    
    //转成函数，需要参数传函数名，如f(add)
    f:=v.(func(i int,j int) int)//i，j可以省略
    result:=f(3,4)
  } 
}

```
## 返回值
1.返回值与参数一样语法</br>
```
//一个返回值
func f() int{

}

//多个返回值
func f() (int, string, ft float, func(), chan bool){
  //f为返回值定义的参数，可以直接return
  n:=0
  s:="test"
  fc:=test()
  c:=make(chan bool)
  return n,s,ft,fc,c
}

```
2.接收返回值
注意：\_下划线表示不接收这个返回值</br>
```
n:=f()
_,_,_,_,_,c:=f()//只接收最后一个值
```
