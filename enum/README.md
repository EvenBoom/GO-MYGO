# 枚举
1.例子
```
package main

import (
	"fmt"
)

type Week int

const (
	Monday Week = 1 + iota
	Tuesday
	Wednesday
	Thursday
	Friday
	Saturday
	Sunday
)

const (
	Year = iota
	Month
	Day
)

var weeks = [...]string{
	"Monday",
	"Tuesday",
	"Wednesday",
	"Thursday",
	"Friday",
	"Saturday",
	"Sunday",
}

func (w Week) String() string {
	return weeks[w-1]
}

func main() {
	var w Week
	w = day(1)//等价于 w = day(Monday)
	fmt.Println(w)
	fmt.Println(Tuesday)
	fmt.Println(Wednesday)
	fmt.Println(Thursday)
	fmt.Println(Friday)
	fmt.Println(Saturday)
	fmt.Println(Sunday)
	fmt.Println(Year)
	fmt.Println(Month)
	fmt.Println(Day)
}

func day(w Week) Week {
	return w
}

```
