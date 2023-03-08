## 代码随想录算法训练营第 6 天 | 哈希表一

## 题目 1: 242. 有效的字母异位词

> 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

> 注意：若  s 和 t  中每个字符出现的次数都相同，则称  s 和 t  互为字母异位词。

### 分析

1. 异位词：字幕错位的意思

### 代码

```go
record := [26]int{}

for _, r := range s {
	record[r-rune('a')]++
}
for _, r := range t {
	record[r-rune('a')]--
}

return record == [26]int{}
```

> 参考链接

1. https://leetcode.cn/problems/valid-anagram/
2. https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html

## 题目 2: 349. 两个数组的交集

> 给定两个数组 nums1 和 nums2 ，返回 它们的交集 。输出结果中的每个元素一定是 唯一 的。我们可以 不考虑输出结果的顺序 。

### 分析

### 代码

```go
set := make(map[int]struct{}, 0)
result := make([]int, 0)

for _, r := range nums1 {
	if _, ok := set[r]; !ok {
		set[r] = struct{}{}
	}
}

for _, r := range nums2 {
	if _, ok := set[r]; ok {
		result = append(result, r)
		delete(set, r)
	}
}

return result
```

> 参考链接

1. https://leetcode.cn/problems/intersection-of-two-arrays/
2. https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html

## 题目 3: 202. 快乐数

> 编写一个算法来判断一个数 n 是不是快乐数。

> 「快乐数」  定义为：

    ```
    对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
    然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
    如果这个过程 结果为  1，那么这个数就是快乐数。
    如果 n 是 快乐数 就返回 true ；不是，则返回 false 。
    ```

### 分析

### 代码

```go
func isHappy(n int) bool {
    m := make(map[int]bool)

    for n != 1 && !m[n] {
        n, m[n] = getSum(n), true
    }
    return n == 1
}

func getSum(n int) int {
    sum := 0
    for n > 0 {
        sum += (n%10)*(n%10)
        n = n / 10
    }

    return sum
}
```

> 参考链接

1. https://leetcode.cn/problems/happy-number/
2. https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html

## 题目 4: 1. 两数之和

> 给定一个整数数组 nums  和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那   两个   整数，并返回它们的数组下标。

> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

> 你可以按任意顺序返回答案。

### 分析

### 代码

```go
m := make(map[int]int)

for k, v := range nums {
	if pk, ok := m[target-v]; ok {
		return []int{pk, k}
	} else {
		m[v] = k
	}
}

return []int{}
```

> 参考链接

1. https://leetcode.cn/problems/two-sum/
2. https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html
