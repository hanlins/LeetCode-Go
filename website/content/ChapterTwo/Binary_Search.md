---
title: 2.11 Binary Search
type: docs
weight: 11
---

# Binary Search

- 二分搜索的经典写法。需要注意的三点：
	1. 循环退出条件，注意是 low <= high，而不是 low < high。
	2. mid 的取值，mid := low + (high-low)>>1
	3. low 和 high 的更新。low = mid + 1，high = mid - 1。

```go
func binarySearchMatrix(nums []int, target int) int {
	low, high := 0, len(nums)-1
	for low <= high {
		mid := low + (high-low)>>1
		if nums[mid] == target {
			return mid
		} else if nums[mid] > target {
			high = mid - 1
		} else {
			low = mid + 1
		}
	}
	return -1
}
```

- 二分搜索的变种写法。有 4 个基本变种:
	1. 查找第一个与 target 相等的元素，时间复杂度 O(logn)
	2. 查找最后一个与 target 相等的元素，时间复杂度 O(logn)
	3. 查找第一个大于等于 target 的元素，时间复杂度 O(logn)
	4. 查找最后一个小于等于 target 的元素，时间复杂度 O(logn)

```go
// 二分查找第一个与 target 相等的元素，时间复杂度 O(logn)
func searchFirstEqualElement(nums []int, target int) int {
	low, high := 0, len(nums)-1
	for low <= high {
		mid := low + ((high - low) >> 1)
		if nums[mid] > target {
			high = mid - 1
		} else if nums[mid] < target {
			low = mid + 1
		} else {
			if (mid == 0) || (nums[mid-1] != target) { // 找到第一个与 target 相等的元素
				return mid
			}
			high = mid - 1
		}
	}
	return -1
}

// 二分查找最后一个与 target 相等的元素，时间复杂度 O(logn)
func searchLastEqualElement(nums []int, target int) int {
	low, high := 0, len(nums)-1
	for low <= high {
		mid := low + ((high - low) >> 1)
		if nums[mid] > target {
			high = mid - 1
		} else if nums[mid] < target {
			low = mid + 1
		} else {
			if (mid == len(nums)-1) || (nums[mid+1] != target) { // 找到最后一个与 target 相等的元素
				return mid
			}
			low = mid + 1
		}
	}
	return -1
}

// 二分查找第一个大于等于 target 的元素，时间复杂度 O(logn)
func searchFirstGreaterElement(nums []int, target int) int {
	low, high := 0, len(nums)-1
	for low <= high {
		mid := low + ((high - low) >> 1)
		if nums[mid] >= target {
			if (mid == 0) || (nums[mid-1] < target) { // 找到第一个大于等于 target 的元素
				return mid
			}
			high = mid - 1
		} else {
			low = mid + 1
		}
	}
	return -1
}

// 二分查找最后一个小于等于 target 的元素，时间复杂度 O(logn)
func searchLastLessElement(nums []int, target int) int {
	low, high := 0, len(nums)-1
	for low <= high {
		mid := low + ((high - low) >> 1)
		if nums[mid] <= target {
			if (mid == len(nums)-1) || (nums[mid+1] > target) { // 找到最后一个小于等于 target 的元素
				return mid
			}
			low = mid + 1
		} else {
			high = mid - 1
		}
	}
	return -1
}
```

- 在基本有序的数组中用二分搜索。经典解法可以解，变种写法也可以写，常见的题型，在山峰数组中找山峰，在旋转有序数组中找分界点。第 33 题，第 81 题，第 153 题，第 154 题，第 162 题，第 852 题

```go
func peakIndexInMountainArray(A []int) int {
	low, high := 0, len(A)-1
	for low < high {
		mid := low + (high-low)>>1
		// 如果 mid 较大，则左侧存在峰值，high = m，如果 mid + 1 较大，则右侧存在峰值，low = mid + 1
		if A[mid] > A[mid+1] {
			high = mid
		} else {
			low = mid + 1
		}
	}
	return low
}
```

- max-min 最大值最小化问题。求在最小满足条件的情况下的最大值。第 410 题，第 875 题，第 1011 题，第 1283 题。


| No.      | Title | Solution | Difficulty | TimeComplexity | SpaceComplexity |Favorite| Acceptance |
|:--------:|:------- | :--------: | :----------: | :----: | :-----: | :-----: |:-----: |
|0004|Median of Two Sorted Arrays|[Go]({{< relref "/ChapterFour/0001~0099/0004.Median-of-Two-Sorted-Arrays.md" >}})|Hard||||31.8%|
|0029|Divide Two Integers|[Go]({{< relref "/ChapterFour/0001~0099/0029.Divide-Two-Integers.md" >}})|Medium||||17.0%|
|0033|Search in Rotated Sorted Array|[Go]({{< relref "/ChapterFour/0001~0099/0033.Search-in-Rotated-Sorted-Array.md" >}})|Medium||||36.3%|
|0034|Find First and Last Position of Element in Sorted Array|[Go]({{< relref "/ChapterFour/0001~0099/0034.Find-First-and-Last-Position-of-Element-in-Sorted-Array.md" >}})|Medium||||38.0%|
|0035|Search Insert Position|[Go]({{< relref "/ChapterFour/0001~0099/0035.Search-Insert-Position.md" >}})|Easy||||42.9%|
|0050|Pow(x, n)|[Go]({{< relref "/ChapterFour/0001~0099/0050.Powx-n.md" >}})|Medium| O(log n)| O(1)||31.2%|
|0069|Sqrt(x)|[Go]({{< relref "/ChapterFour/0001~0099/0069.Sqrtx.md" >}})|Easy| O(log n)| O(1)||35.7%|
|0074|Search a 2D Matrix|[Go]({{< relref "/ChapterFour/0001~0099/0074.Search-a-2D-Matrix.md" >}})|Medium||||38.5%|
|0081|Search in Rotated Sorted Array II|[Go]({{< relref "/ChapterFour/0001~0099/0081.Search-in-Rotated-Sorted-Array-II.md" >}})|Medium||||33.8%|
|0153|Find Minimum in Rotated Sorted Array|[Go]({{< relref "/ChapterFour/0100~0199/0153.Find-Minimum-in-Rotated-Sorted-Array.md" >}})|Medium||||46.6%|
|0154|Find Minimum in Rotated Sorted Array II|[Go]({{< relref "/ChapterFour/0100~0199/0154.Find-Minimum-in-Rotated-Sorted-Array-II.md" >}})|Hard||||42.2%|
|0162|Find Peak Element|[Go]({{< relref "/ChapterFour/0100~0199/0162.Find-Peak-Element.md" >}})|Medium||||44.2%|
|0167|Two Sum II - Input array is sorted|[Go]({{< relref "/ChapterFour/0100~0199/0167.Two-Sum-II-Input-array-is-sorted.md" >}})|Easy| O(n)| O(1)||56.0%|
|0174|Dungeon Game|[Go]({{< relref "/ChapterFour/0100~0199/0174.Dungeon-Game.md" >}})|Hard||||33.6%|
|0209|Minimum Size Subarray Sum|[Go]({{< relref "/ChapterFour/0200~0299/0209.Minimum-Size-Subarray-Sum.md" >}})|Medium| O(n)| O(1)||40.2%|
|0222|Count Complete Tree Nodes|[Go]({{< relref "/ChapterFour/0200~0299/0222.Count-Complete-Tree-Nodes.md" >}})|Medium| O(n)| O(1)||50.3%|
|0230|Kth Smallest Element in a BST|[Go]({{< relref "/ChapterFour/0200~0299/0230.Kth-Smallest-Element-in-a-BST.md" >}})|Medium| O(n)| O(1)||63.4%|
|0240|Search a 2D Matrix II|[Go]({{< relref "/ChapterFour/0200~0299/0240.Search-a-2D-Matrix-II.md" >}})|Medium||||45.7%|
|0275|H-Index II|[Go]({{< relref "/ChapterFour/0200~0299/0275.H-Index-II.md" >}})|Medium||||36.4%|
|0287|Find the Duplicate Number|[Go]({{< relref "/ChapterFour/0200~0299/0287.Find-the-Duplicate-Number.md" >}})|Medium| O(n)| O(1)|❤️|58.2%|
|0300|Longest Increasing Subsequence|[Go]({{< relref "/ChapterFour/0300~0399/0300.Longest-Increasing-Subsequence.md" >}})|Medium| O(n log n)| O(n)||45.0%|
|0315|Count of Smaller Numbers After Self|[Go]({{< relref "/ChapterFour/0300~0399/0315.Count-of-Smaller-Numbers-After-Self.md" >}})|Hard||||42.3%|
|0327|Count of Range Sum|[Go]({{< relref "/ChapterFour/0300~0399/0327.Count-of-Range-Sum.md" >}})|Hard||||36.3%|
|0349|Intersection of Two Arrays|[Go]({{< relref "/ChapterFour/0300~0399/0349.Intersection-of-Two-Arrays.md" >}})|Easy| O(n)| O(n) ||65.8%|
|0350|Intersection of Two Arrays II|[Go]({{< relref "/ChapterFour/0300~0399/0350.Intersection-of-Two-Arrays-II.md" >}})|Easy| O(n)| O(n) ||52.4%|
|0354|Russian Doll Envelopes|[Go]({{< relref "/ChapterFour/0300~0399/0354.Russian-Doll-Envelopes.md" >}})|Hard||||38.1%|
|0367|Valid Perfect Square|[Go]({{< relref "/ChapterFour/0300~0399/0367.Valid-Perfect-Square.md" >}})|Easy||||42.3%|
|0378|Kth Smallest Element in a Sorted Matrix|[Go]({{< relref "/ChapterFour/0300~0399/0378.Kth-Smallest-Element-in-a-Sorted-Matrix.md" >}})|Medium||||56.9%|
|0392|Is Subsequence|[Go]({{< relref "/ChapterFour/0300~0399/0392.Is-Subsequence.md" >}})|Easy| O(n)| O(1)||49.7%|
|0410|Split Array Largest Sum|[Go]({{< relref "/ChapterFour/0400~0499/0410.Split-Array-Largest-Sum.md" >}})|Hard||||47.0%|
|0436|Find Right Interval|[Go]({{< relref "/ChapterFour/0400~0499/0436.Find-Right-Interval.md" >}})|Medium||||48.6%|
|0441|Arranging Coins|[Go]({{< relref "/ChapterFour/0400~0499/0441.Arranging-Coins.md" >}})|Easy||||42.8%|
|0454|4Sum II|[Go]({{< relref "/ChapterFour/0400~0499/0454.4Sum-II.md" >}})|Medium| O(n^2)| O(n) ||54.8%|
|0475|Heaters|[Go]({{< relref "/ChapterFour/0400~0499/0475.Heaters.md" >}})|Medium||||33.8%|
|0483|Smallest Good Base|[Go]({{< relref "/ChapterFour/0400~0499/0483.Smallest-Good-Base.md" >}})|Hard||||36.5%|
|0493|Reverse Pairs|[Go]({{< relref "/ChapterFour/0400~0499/0493.Reverse-Pairs.md" >}})|Hard||||27.5%|
|0497|Random Point in Non-overlapping Rectangles|[Go]({{< relref "/ChapterFour/0400~0499/0497.Random-Point-in-Non-overlapping-Rectangles.md" >}})|Medium||||39.1%|
|0528|Random Pick with Weight|[Go]({{< relref "/ChapterFour/0500~0599/0528.Random-Pick-with-Weight.md" >}})|Medium||||44.9%|
|0658|Find K Closest Elements|[Go]({{< relref "/ChapterFour/0600~0699/0658.Find-K-Closest-Elements.md" >}})|Medium||||42.6%|
|0668|Kth Smallest Number in Multiplication Table|[Go]({{< relref "/ChapterFour/0600~0699/0668.Kth-Smallest-Number-in-Multiplication-Table.md" >}})|Hard||||48.1%|
|0704|Binary Search|[Go]({{< relref "/ChapterFour/0700~0799/0704.Binary-Search.md" >}})|Easy||||54.5%|
|0710|Random Pick with Blacklist|[Go]({{< relref "/ChapterFour/0700~0799/0710.Random-Pick-with-Blacklist.md" >}})|Hard| O(n)| O(n)  ||33.1%|
|0718|Maximum Length of Repeated Subarray|[Go]({{< relref "/ChapterFour/0700~0799/0718.Maximum-Length-of-Repeated-Subarray.md" >}})|Medium||||50.8%|
|0719|Find K-th Smallest Pair Distance|[Go]({{< relref "/ChapterFour/0700~0799/0719.Find-K-th-Smallest-Pair-Distance.md" >}})|Hard||||32.8%|
|0744|Find Smallest Letter Greater Than Target|[Go]({{< relref "/ChapterFour/0700~0799/0744.Find-Smallest-Letter-Greater-Than-Target.md" >}})|Easy||||45.6%|
|0778|Swim in Rising Water|[Go]({{< relref "/ChapterFour/0700~0799/0778.Swim-in-Rising-Water.md" >}})|Hard||||55.1%|
|0786|K-th Smallest Prime Fraction|[Go]({{< relref "/ChapterFour/0700~0799/0786.K-th-Smallest-Prime-Fraction.md" >}})|Hard||||44.2%|
|0793|Preimage Size of Factorial Zeroes Function|[Go]({{< relref "/ChapterFour/0700~0799/0793.Preimage-Size-of-Factorial-Zeroes-Function.md" >}})|Hard||||40.6%|
|0852|Peak Index in a Mountain Array|[Go]({{< relref "/ChapterFour/0800~0899/0852.Peak-Index-in-a-Mountain-Array.md" >}})|Easy||||71.7%|
|0862|Shortest Subarray with Sum at Least K|[Go]({{< relref "/ChapterFour/0800~0899/0862.Shortest-Subarray-with-Sum-at-Least-K.md" >}})|Hard||||25.3%|
|0875|Koko Eating Bananas|[Go]({{< relref "/ChapterFour/0800~0899/0875.Koko-Eating-Bananas.md" >}})|Medium||||53.6%|
|0878|Nth Magical Number|[Go]({{< relref "/ChapterFour/0800~0899/0878.Nth-Magical-Number.md" >}})|Hard||||28.9%|
|0887|Super Egg Drop|[Go]({{< relref "/ChapterFour/0800~0899/0887.Super-Egg-Drop.md" >}})|Hard||||27.1%|
|0911|Online Election|[Go]({{< relref "/ChapterFour/0900~0999/0911.Online-Election.md" >}})|Medium||||51.6%|
|0927|Three Equal Parts|[Go]({{< relref "/ChapterFour/0900~0999/0927.Three-Equal-Parts.md" >}})|Hard||||34.7%|
|0981|Time Based Key-Value Store|[Go]({{< relref "/ChapterFour/0900~0999/0981.Time-Based-Key-Value-Store.md" >}})|Medium||||54.5%|
|1011|Capacity To Ship Packages Within D Days|[Go]({{< relref "/ChapterFour/1000~1099/1011.Capacity-To-Ship-Packages-Within-D-Days.md" >}})|Medium||||60.2%|
|1111|Maximum Nesting Depth of Two Valid Parentheses Strings|[Go]({{< relref "/ChapterFour/1100~1199/1111.Maximum-Nesting-Depth-of-Two-Valid-Parentheses-Strings.md" >}})|Medium||||72.9%|
|1157|Online Majority Element In Subarray|[Go]({{< relref "/ChapterFour/1100~1199/1157.Online-Majority-Element-In-Subarray.md" >}})|Hard||||40.9%|
|1170|Compare Strings by Frequency of the Smallest Character|[Go]({{< relref "/ChapterFour/1100~1199/1170.Compare-Strings-by-Frequency-of-the-Smallest-Character.md" >}})|Medium||||60.5%|
|1201|Ugly Number III|[Go]({{< relref "/ChapterFour/1200~1299/1201.Ugly-Number-III.md" >}})|Medium||||26.5%|
|1235|Maximum Profit in Job Scheduling|[Go]({{< relref "/ChapterFour/1200~1299/1235.Maximum-Profit-in-Job-Scheduling.md" >}})|Hard||||48.0%|
|1283|Find the Smallest Divisor Given a Threshold|[Go]({{< relref "/ChapterFour/1200~1299/1283.Find-the-Smallest-Divisor-Given-a-Threshold.md" >}})|Medium||||50.2%|
|1300|Sum of Mutated Array Closest to Target|[Go]({{< relref "/ChapterFour/1300~1399/1300.Sum-of-Mutated-Array-Closest-to-Target.md" >}})|Medium||||42.8%|
|1337|The K Weakest Rows in a Matrix|[Go]({{< relref "/ChapterFour/1300~1399/1337.The-K-Weakest-Rows-in-a-Matrix.md" >}})|Easy||||72.0%|
|1482|Minimum Number of Days to Make m Bouquets|[Go]({{< relref "/ChapterFour/1400~1499/1482.Minimum-Number-of-Days-to-Make-m-Bouquets.md" >}})|Medium||||51.6%|
|1631|Path With Minimum Effort|[Go]({{< relref "/ChapterFour/1600~1699/1631.Path-With-Minimum-Effort.md" >}})|Medium||||50.1%|
|1642|Furthest Building You Can Reach|[Go]({{< relref "/ChapterFour/1600~1699/1642.Furthest-Building-You-Can-Reach.md" >}})|Medium||||46.7%|
|1649|Create Sorted Array through Instructions|[Go]({{< relref "/ChapterFour/1600~1699/1649.Create-Sorted-Array-through-Instructions.md" >}})|Hard||||36.8%|
|1658|Minimum Operations to Reduce X to Zero|[Go]({{< relref "/ChapterFour/1600~1699/1658.Minimum-Operations-to-Reduce-X-to-Zero.md" >}})|Medium||||33.3%|
|------------|-------------------------------------------------------|-------| ----------------| ---------------|-------------|-------------|-------------|


----------------------------------------------
<div style="display: flex;justify-content: space-between;align-items: center;">
<p><a href="https://books.halfrost.com/leetcode/ChapterTwo/Breadth_First_Search/">⬅️上一页</a></p>
<p><a href="https://books.halfrost.com/leetcode/ChapterTwo/Math/">下一页➡️</a></p>
</div>
