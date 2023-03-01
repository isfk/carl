# 代码随想录算法训练营第一天 | 数组理论基础，704. 二分查找，27. 移除元素

> 2023-03-01

## 题目 1: 704. 二分查找

> 给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

### 分析

1. 在一个 `有序（升序）`的数组中，找到给定的一个值 `target`，找到返回对应索引，找不到返回 `-1`
2. 查找逻辑：假设数组左右尽头索引分别为 `l` `r` 取数组中间索引 `m`，将目标 `target` 与 `m`索引值 进行对比，如果 `target > nums[m]` ，那么 `t` 应该在 `m` 与 `r` 之间，反之应该在 `l` 与 `m` 之间，最终 如果 `target = nums[m]` 就是我们想要的结果
3. 然后就是判断边界的问题了。进行第二步的时候，不可能说一下子就找到或找不到目标，那么我们就要进行二分查找了，就是 `扔一半，留一半` 的操作

### 代码

- 左闭右闭

```go
func search(nums []int, target int) int {
    l := 0
    r := len(nums) - 1

    for l <= r {
        m := (l + r) / 2
        if (target > nums[m]) {
            l = m+1
        } else if (target < nums[m]) {
            r = m-1
        } else {
            return m
        }
    }
	return -1
}
```

- 左闭右开

```
func search(nums []int, target int) int {
    l := 0
    r := len(nums) - 1

    for l < r {
        m := (l + r) / 2
        if (target > nums[m]) {
            l = m+1
        } else if (target < nums[m]) {
            r = m
        } else {
            return m
        }
    }
	return -1
}
```

> 参考链接

1. [力扣](https://leetcode.cn/problems/binary-search/)
2. [代码随想](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)

## 题目 2: 27. 移除元素

> 给你一个数组 nums  和一个值 val，你需要 原地 移除所有数值等于  val  的元素，并返回移除后数组的新长度。
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

### 分析

1. 暴力解法。第一想法是新数组，后来一想不对，看了下随想录，整体移动
2. 双指针解法。双指针方法只需要一个循环，快指针向后一个一个的进行遍历，慢指针是最终的长度

### 代码

- 暴力解法

```go
func removeElement(nums []int, val int) int {
    size := len(nums) - 1
    for i := 0; i < len(nums); i++ {
        if (nums[i] == val) {   // 找到元素后，元素后面整体迁移
            for j := i + 1; j < size; j++ {
                nums[j-1] = nums[j]
            }
            i--
            size--
        }
    }
    return size
}
```

- 双指针解法

```go
func removeElement(nums []int, val int) int {
	size := len(nums) - 1
    slow := 0
	for i := 0; i < size; i++ {
        if (nums[i] != val) {
            nums[slow] = nums[i]
            slow++
        }
	}
	return slow
}
```

> 参考链接

1. [力扣](https://leetcode.cn/problems/remove-element/)
2. [代码随想](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)
