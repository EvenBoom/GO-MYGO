# 时间（Time）
## 简介
time包是用来处理时间的包
## 例子
```
loc,_:=time.LoadLocation("Asia/Shanghai")//字符串转时区
t := time.Date(1992, 1, 1, 23, 59, 59, 123456789, loc)//参数分别为年月日时分秒纳秒和时区
t.Format("2006年01月02日 15时04分05秒.000000000")//网上有人总结记忆方法:612345，另.后面是纳秒，多少个零取多少位
time.Now().Unix()//秒时间戳
time.Now().UnixNano()//纳秒时间戳
time.Now().YearDay()//以1月1号为第1天，算出现在是第几天
time.Now().Year()//年份
time.Now().Month()//月份
time.Now().Day()//日
time.Now().Hour()//时
time.Now().Minute()//分
time.Now().Second()//秒
time.Now().Nanosecond()//纳秒
```
