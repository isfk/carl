## 代码随想录算法训练营第 2 天 | 977.有序数组的平方 ，209.长度最小的子数组 ，59.螺旋矩阵 II

## 题目 1: 977.有序数组的平方

> 给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

### 分析

1. 大多数第一想法是每个元素进行平方运算，然后进行数组排序
2. `1` 虽然好用，但是考验不出对数组索引的使用
3. 使用双指针方法，每次取左右最大的一个平方数
4. 这题之前刷过，加上昨天的题目，今天解题思路更加清晰了

### 代码

```go
length := len(nums)
l := 0
r := length - 1
i := length - 1

newNums := make([]int, length)
for l <= r {
	if (nums[l]*nums[l] < nums[r]*nums[r]) {
		newNums[r] = nums[r]*nums[r]
		r--
	} else {
		newNums[l] = nums[l]*nums[l]
		l++
	}
	i--
}
return newNums
```

> 参考链接

1. https://leetcode.cn/problems/squares-of-a-sorted-array/
2. https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html

## 题目 2：209.长度最小的子数组

> 给定一个含有  n  个正整数的数组和一个正整数 target 。

> 找出该数组中满足其和 ≥ target 的长度最小的 连续子数组  [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

### 分析

1. 首先理解题目要求，例如数组：`nums=[1,3,5,2,2,4] target=8`，那么 `3+5`, `2+2+4`都满足和的要求，但`3+5`的长度最小，`2`应为结果长度
2. 暴力解法。两层循环，内循环进行累加操作
3. 滑动窗格。快慢指针

### 代码

- 内外循环

```go
subLength := 0
finalLength := len(nums) + 1
for i := 0; i < len(nums); i++ {
	sum := 0
	for j := i; j < len(nums); j++ {
		sum += nums[i]
		if (sum >= target) {
			subLength = j - i + 1
			if (subLength < finalLength) {
				finalLength = subLength
			}
			break
		}
	}
}

if (finalLength == len(nums) + 1) {
	return 0
}

return finalLength
```

- 滑动窗格

```go
slow := 0
finalLength := len(nums) + 1
sum := 0
for i := 0; i < len(nums); i++ {
	sum += nums[i]
	for sum >= target {
		subLength := i - slow + 1
		if (subLength < finalLength) {
			finalLength = subLength
		}
		sum -= nums[slow]
		slow++
	}
}

if (finalLength == len(nums) + 1) {
	return 0
}

return finalLength
```

> 参考链接

1. https://leetcode.cn/problems/minimum-size-subarray-sum/
2. https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html

## 题目 3：螺旋矩阵 II

> 给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

### 分析

1. 转圈的问题 使用权属进行外循环
2. 圈内按照 上行，右列，下行，左列进行左闭右开进行填充

### 代码

```go
loop := n / 2
center := loop
x, y := 0, 0

num := 1
offset := 1

result := make([][]int, n)

for i := 0; i < n; i++ {
	result[i] = make([]int, n)
}
fmt.Println(result)

for loop > 0 {
	i, j := x, y
	// 上行，行不变列变
	for j = y; j < n-offset; j++ {
		result[i][j] = num
		num++
	}

	// 右列， 行变列不变
	for i = x; i < n-offset; i++ {
		result[i][j] = num
		num++
	}

	// 下行， 行不变列变
	for ; j > y; j-- {
		result[i][j] = num
		num++
	}

	// 左列，行变列不变
	for ; i > x; i-- {
		result[i][j] = num
		num++
	}
	x++
	y++
	offset++
	loop--
}
if n%2 == 1 {
	result[center][center] = n * n
}
return result
```

> 参考链接

1. https://leetcode.cn/problems/spiral-matrix-ii/
2. https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html
