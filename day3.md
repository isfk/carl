## 代码随想录算法训练营第 3 天 | 链表理论基础，203.移除链表元素，707.设计链表，206.反转链表

## 链表理论基础

1. 链表是一个结构，由数据部分，指针部分构成
2. 链表可以是单链，也可以是双向链表

- https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

```go
type ListNode struct {
	Val int
	Next *ListNode
}
```

## 题目 1: 203.移除链表元素

> 给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。

### 分析

1. 在不使用虚拟头的情况下，要处理链表头值=`val`的情况
2. 虚拟头可以跳过单独处理链表头的逻辑，直接跳到 `1` 的后半部分逻辑

### 代码

- 从链表头开始处理

```go
for head != nil && head.Val == val {
	head = head.Next
}

current := head

for current != nil && current.Next != nil  {
	if (current.Next.Val == val) {
		current.Next = current.Next.Next
	} else {
		current = current.Next
	}
}

return head
```

- 虚拟头

```go
// 设置一个虚拟头节点
vHead := &ListNode{Next: head}

current := vHead

for current != nil && current.Next != nil {
	if (current.Next.Val == val) {
		current.Next = current.Next.Next
	} else {
		current = current.Next
	}
}

return vHead.Next
```

> 参考链接

1. https://leetcode.cn/problems/remove-linked-list-elements/
2. https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html

## 题目 2: 707.设计链表

### 分析

1. 从哪里断开很重要

### 代码

```go
type Node struct {
    Val int
    Next *Node
}

type MyLinkedList struct {
	DummyHead *Node
    Size int
}

func Constructor() MyLinkedList {
    dummyHead := &Node{Val: -1, Next: nil}
    return MyLinkedList{DummyHead: dummyHead, Size: 0}
}


func (this *MyLinkedList) Get(index int) int {
    if (index < 0 || index > this.Size - 1) {
        return -1
    }

    // 取虚拟头
    current := this.DummyHead

    for i := 0; i <= index; i++ {
        current = current.Next
    }

    return current.Val
}


func (this *MyLinkedList) AddAtHead(val int)  {
    newNode := &Node{Val: val, Next: nil}
    newNode.Next = this.DummyHead.Next
    this.DummyHead.Next = newNode
    this.Size++
}


func (this *MyLinkedList) AddAtTail(val int)  {
    newNode := &Node{Val: val, Next: nil}
    current := this.DummyHead

    for current.Next != nil {
        current = current.Next
    }

    current.Next = newNode
    this.Size++
}


func (this *MyLinkedList) AddAtIndex(index int, val int)  {
    if (index < 0 || index > this.Size) {
        return
    }
    if (index == this.Size) {
        this.AddAtTail(val)
        return
    }

    newNode := &Node{Val: val, Next: nil}
    current := this.DummyHead
    for i :=0; i <= index - 1; i++ {
        current = current.Next
    }
    newNode.Next = current.Next
    current.Next = newNode
    this.Size++
}


func (this *MyLinkedList) DeleteAtIndex(index int)  {
    if (index > this.Size - 1 || index < 0) {
        return
    }
    current := this.DummyHead
    for i := 0; i <= index - 1; i++ {
        current = current.Next
    }
    current.Next = current.Next.Next
    this.Size--
}
```

> 参考链接

1. https://leetcode.cn/problems/design-linked-list/
2. https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html

## 题目 3: 206.反转链表

### 分析

### 代码

- 双指针

```go
var pre *ListNode
current := head
for current != nil {
    next := current.Next
    current.Next = pre
    pre = current
    current = next
}

return pre
```

- 递归方法

```go
func reverseList(head *ListNode) *ListNode {
    return reverseTwo(nil, head)
}


func reverseTwo(pre, current *ListNode) *ListNode {
    if (current == nil) {
        return pre
    }

    next := current.Next
    current.Next = pre

    return reverseTwo(current, next)
}
```

> 参考链接

1. https://leetcode.cn/problems/reverse-linked-list/
2. https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html
