## 代码随想录算法训练营第 10 天 | 堆栈

## 题目 1: 232. 用栈实现队列

### 分析

### 代码

```go
type MyQueue struct {
    stackIn []int
    stackOut []int
}


func Constructor() MyQueue {
    return MyQueue{
        stackIn: make([]int, 0),
        stackOut:  make([]int, 0),
    }
}


func (this *MyQueue) Push(x int)  {
    this.stackIn = append(this.stackIn, x)
}


func (this *MyQueue) Pop() int {
    lenIn, lenOut := len(this.stackIn), len(this.stackOut)
    if lenOut == 0 {
        if lenIn == 0 {
            return -1
        }

        for i := lenIn - 1; i >= 0 ; i-- {
            this.stackOut = append(this.stackOut, this.stackIn[i])
        }

        this.stackIn = []int{}
        lenOut = len(this.stackOut)
    }
    val := this.stackOut[lenOut-1]
    this.stackOut = this.stackOut[:lenOut-1]

    return val
}


func (this *MyQueue) Peek() int {
    val := this.Pop()
    if val == -1 {
        return -1
    }

    this.stackOut = append(this.stackOut, val)
    return val
}


func (this *MyQueue) Empty() bool {
    return len(this.stackIn) == 0 && len(this.stackOut) == 0
}


/**
 * Your MyQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Peek();
 * param_4 := obj.Empty();
 */
```

> 参考链接

1. https://leetcode.cn/problems/implement-queue-using-stacks/
2. https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html

## 题目 2: 225. 用队列实现栈

### 分析

### 代码

```go
type MyStack struct {
    queue1 []int
    queue2 []int
}


func Constructor() MyStack {
    return MyStack {
        queue1: make([]int, 0),
        queue2: make([]int, 0),
    }
}


func (this *MyStack) Push(x int)  {
    this.queue2 = append(this.queue2, x)
    this.Move()
}

func (this *MyStack) Move() {
    if len(this.queue1) == 0 {
        this.queue1, this.queue2 = this.queue2, this.queue1
    } else {
        this.queue2 = append(this.queue2, this.queue1[0])
        this.queue1 = this.queue1[1:]
        this.Move()
    }
}


func (this *MyStack) Pop() int {
    val := this.queue1[0]
    this.queue1 = this.queue1[1:]
    return val
}


func (this *MyStack) Top() int {
    return this.queue1[0]
}


func (this *MyStack) Empty() bool {
    return len(this.queue1) == 0
}


/**
 * Your MyStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Empty();
 */
```

> 参考链接

1. https://leetcode.cn/problems/implement-stack-using-queues/
2. https://programmercarl.com/0225.%E7%94%A8%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.html
