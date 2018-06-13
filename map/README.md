# 映射（Map）
## 目录（Catalog）
1.[简介](#简介brief-introduction)</br>
2.[声明](#声明declaration)</br>
3.[初始化](#初始化initialization)</br>
4.[使用](#使用use)</br>
## 简介（Brief-introduction）
map是key-value存储的，底层用了hash算法，属于hashmap，并发是不安全的。据网上有人测试，数据量大时map的查询速度比slice快，数据量小时相反（若考虑性能的时候，最好都用来试一下，对比测试是最实际）。简书有一篇文章讲得很深入[如何设计并实现一个线程安全的 Map ？(上篇)](https://www.jianshu.com/p/cd41ca8741f4)，目前我只看懂了一部分，希望以后有时间再返回来看看。
## 声明（Declaration）
```
var myMap map[string]string
```
## 初始化（Initialization）
```
var myMap map[string]string
myMap = map[string]string{
	"name": "Andy",
	"job":  "coder",
}

myMap = make(map[string]string)
```
## 使用（Use）
```
fmt.Println(myMap["name"], len(myMap))
```
注意：map是不能使用cap的
