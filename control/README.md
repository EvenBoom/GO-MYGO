# 流程控制（Control）
## 目录（Catalog）
1.[条件语句](#条件语句condition)</br>
2.[循环语句](#循环语句loop)</br>
## 条件语句（Condition）
1.if</br>
```
status:=0
if status==0 {
  fmt.Println("0")
} else if status==1 {
  fmt.Println("1")
} else {
  fmt.Println("-1")
}
```
2.switch
```
status:=0
switch status {
  case 0:
    fmt.Println("You are master")
  case 1:
    fmt.Println("You are user")
  case -1:
    fmt.Println("You are nothing")
  default:
    fmt.Println("What should i say")
}
```
## 循环语句（Loop）
go的循环只有for</br>
```
//普通循环
for i:=0; i<100; i++ {
  fmt.Println(i)
}

//遍历
```
for i, v := range nums{
  fmt.Println(i)//索引
  fmt.Println(v)//值
}
```
