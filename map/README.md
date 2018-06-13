# 映射（Map）
## 目录（Catalog）
1.[简介](#简介#brief-intruduction)
2.[声明](#声明#)
## 简介（Brief-introduction）
map是key-value存储的，底层用了hash算法，属于hashmap，并发是不安全的。据网上有人测试，数据量大时map的查询速度比slice快，数据量小时相反（若考虑性能的时候，最好都用来试一下，对比测试是最实际）。简书有一篇文章讲得很深入[如何设计并实现一个线程安全的 Map ？(上篇)](https://www.jianshu.com/p/cd41ca8741f4)，目前我只看懂了一部分，希望以后有时间再返回来看看。
## 声明（Declaration）
