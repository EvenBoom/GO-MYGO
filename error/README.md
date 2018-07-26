# 错误
1.例子
```
package main

import (
	"errors"
	"fmt"
)

func main() {
	err := test()
	if err != nil {
		fmt.Println(err.Error())//打印错误
	}
}

func test() error {
	return errors.New("just error")//创建错误
}

```
