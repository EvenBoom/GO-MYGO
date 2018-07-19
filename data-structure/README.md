# 数据结构
## 简介
1.单链表
节点
```
package node

type Node struct {
	Data interface{}
	Next *Node
}

```
连接成单链表
```
package main

import (
	"data-struct/node"
	"fmt"
)

func main() {
	headNode := new(node.Node)

	headNode.Data = "head"
	headNode.Next = nil
	for i := 0; i < 1000; i++ {
		childNode := new(node.Node)
		childNode.Data = i
		childNode.Next = headNode
		headNode = childNode
	}
	resultNode := headNode
	for {
		fmt.Println(resultNode.Data)
		if resultNode.Next == nil {
			break
		}
		resultNode = resultNode.Next
	}
}

```
