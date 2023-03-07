## 代码随想录算法训练营第 4 天 | 第二章 链表

## 题目 1: 24. 两两交换链表中的节点

> 给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

> 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

### 分析

1. 正常交换中，遗漏了第三步

### 代码

```go
dummyHead := &ListNode{Val: -1, Next: nil}
dummyHead.Next = head

current := dummyHead
for current != nil && current.Next != nil && current.Next.Next != nil {
    tmp1 := current.Next
    tmp2 := current.Next.Next.Next

    current.Next = current.Next.Next
    current.Next.Next = tmp1
    current.Next.Next.Next = tmp2

    current = current.Next.Next
}

return dummyHead.Next
```

> 参考链接

1. https://leetcode.cn/problems/swap-nodes-in-pairs/
2. https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html

## 题目 2：19. 删除链表的倒数第 N 个结点

> 给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

> 进阶：你能尝试使用一趟扫描实现吗？

### 分析

1. 第一想法：明确删除弟 `N` 个，需要直到确切长度，或者反转之后从头开始，但这样肯定不对
2. 看录说快慢指针，定好间隔，快指针到末尾，慢指针指向就是要删除的

### 代码

```go
dummyHead := &ListNode{Val: 0}
dummyHead.Next = head
fast := dummyHead
slow := dummyHead

for n > 0 && fast != nil {
    fast = fast.Next
    n--
}

fast = fast.Next

for fast != nil {
    fast = fast.Next
    slow = slow.Next
}

slow.Next = slow.Next.Next

return dummyHead.Next
```

> 参考链接

1. https://leetcode.cn/problems/remove-nth-node-from-end-of-list/
2. https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html

## 题目 3：面试题 02.07. 链表相交

> 给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

### 分析

1. 出看题不知道以为半截相交后还可以半截分拆，自己思考错误，这种情况不能称之为相交
2. 图示的末尾对齐逻辑为相交的处理方式

### 代码

```go
currentA := headA
currentB := headB

lengthA := 0
lengthB := 0

for currentA != nil {
    lengthA++
    currentA = currentA.Next
}

for currentB != nil {
    lengthB++
    currentB = currentB.Next
}

count := 0
var fast *ListNode
var slow *ListNode

if (lengthB > lengthA) {
    count = lengthB - lengthA
    fast = headB
    slow = headA
} else {
    count = lengthA - lengthB
    fast = headA
    slow = headB
}

for count > 0 && fast != nil {
    fast = fast.Next
    count--
}

for fast != slow {
    fast = fast.Next
    slow = slow.Next
}

return fast
```

> 参考链接

1. https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/
2. https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html

## 题目 4：142. 环形链表 II

> 给定一个链表的头节点  head ，返回链表开始入环的第一个节点。  如果链表无环，则返回  null。

> 如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

> 不允许修改 链表。

### 分析

1. 看分析能理解，自己想肯定想不出来
2. 看代码能理解，自己写可能很复杂

### 代码

```go
fast := head
slow := head

for fast != nil && fast.Next != nil {
    slow = slow.Next
    fast = fast.Next.Next

    if(slow == fast) {
        i := fast
        j := head
        for i != j {
            i = i.Next
            j = j.Next
        }

        return j
    }
}
return nil
```

> 参考链接

1. https://leetcode.cn/problems/linked-list-cycle-ii/
2. https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html
