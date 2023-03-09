## 代码随想录算法训练营第 8 天 | 字符串

## 题目 1: 344.反转字符串

### 分析

1. 双指针，收尾交换

### 代码

```go
func reverseString(s []byte) {
    left := 0
    right := len(s)-1
    for left < right {
        s[left], s[right] = s[right], s[left]
        left++
        right--
    }
}
```

## 题目 2: 541. 反转字符串 II

> 给定一个字符串 s 和一个整数 k，从字符串开头算起，每计数至 2k 个字符，就反转这 2k 字符中的前 k 个字符。

> 如果剩余字符少于 k 个，则将剩余字符全部反转。

> 如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。

### 分析

1. 读题 2k 个字符中 前 k 个反转
2. 反转调用上一题的函数即可

### 代码

```go
func reverseStr(s string, k int) string {
    ss := []byte(s)
    length := len(s)
    for i := 0; i < length; i += 2 * k {
        if i + k <= length {
            reverse(ss[i:i+k])
        } else {
            reverse(ss[i:length])
        }
    }
    return string(ss)
}

func reverse(b []byte) {
    left := 0
    right := len(b) - 1
    for left < right {
        b[left], b[right] = b[right], b[left]
        left++
        right--
    }
}
```

## 题目 3: 剑指 Offer 05. 替换空格

> 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

### 分析

1. 一个空格替换为`%20`，在不使用新变量的情况下，扩充原空间
2. 从后往前替换，依然是双指针方法

### 代码

```go
func replaceSpace(s string) string {
    ss := []byte(s)
    length := len(b)
    spaceCount := 0
    for _, v := range ss {
        if v == ' ' {
            spaceCount++
        }
    }
    tmp := make([]byte, spaceCount * 2)	// 2 不是3，因为原来空格占1
    ss = append(ss, tmp...)
    i := length - 1
    j := len(ss) - 1
    for i >= 0 {
        if ss[i] != ' ' {
            ss[j] = ss[i]
            i--
            j--
        } else {
            ss[j] = '0'
            ss[j-1] = '2'
            ss[j-2] = '%'
            i--
            j = j - 3
        }
    }
    return string(b)
}
```
