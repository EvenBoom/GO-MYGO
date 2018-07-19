# 数据结构
## 简介
1.单链表
单链接节点
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
双链表
双链接节点
```
package node

type Node struct {
	Data     interface{}
	Next     *Node
	Previous *Node
}

```
连接成双链表
```
package main

import (
	"data-struct/node"
	"fmt"
)

func main() {
	headNode := new(node.Node)

	headNode.Data = "head"
	for i := 0; i < 1000; i++ {
		childNode := new(node.Node)
		childNode.Data = i
		childNode.Next = headNode
		headNode.Previous = childNode
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
	for {
		fmt.Println(resultNode.Data)
		if resultNode.Previous == nil {
			break
		}
		resultNode = resultNode.Previous
	}
}

```
