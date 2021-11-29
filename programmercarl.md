## 数组

## 链表

## 哈希表

## 字符串

## 双指针

## 栈与队列

## 二叉树

## 回溯算法

#### [90. 子集 II](https://leetcode-cn.com/problems/subsets-ii/)

给你一个整数数组 `nums` ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。返回的解集中，子集可以按 **任意顺序** 排列。

**示例 1：**

```
输入：nums = [1,2,2]
输出：[[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**示例 2：**

```
输入：nums = [0]
输出：[[],[0]]
```

**提示：**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

 ```go
 func subsetsWithDup(nums []int) [][]int {
 	var res [][]int
 	sort.Ints(nums)
 	backtracking([]int{}, nums, 0, &res)
 	return res
 }
 
 func backtracking(track, nums []int, index int, res *[][]int) {
 	tmp := make([]int, len(track))
 	copy(tmp, track)
 	*res = append(*res, tmp)
 	for i := index; i < len(nums); i++ {
 		if i > index && nums[i] == nums[i-1] {
 			continue
 		}
 		track = append(track, nums[i])
 		backtracking(track, nums, i+1, res)
 		track = track[:len(track)-1]
 	}
 }
 ```

####  [491. 递增子序列](https://leetcode-cn.com/problems/increasing-subsequences/)


给你一个整数数组 `nums` ，找出并返回所有该数组中不同的递增子序列，递增子序列中 **至少有两个元素** 。你可以按 **任意顺序** 返回答案。

数组中可能含有重复元素，如出现两个整数相等，也可以视作递增序列的一种特殊情况。


**示例 1：**

```
输入：nums = [4,6,7,7]
输出：[[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

**示例 2：**

```
输入：nums = [4,4,3,2,1]
输出：[[4,4]]
```
**提示：**

- `1 <= nums.length <= 15`
- `-100 <= nums[i] <= 100`

```go
func findSubsequences(nums []int) [][]int {
	var res [][]int
	backtracking([]int{}, nums, 0, &res)
	return res
}

func backtracking(track, nums []int, index int, res *[][]int) {
	if len(track) > 1 {
		tmp := make([]int, len(track))
		copy(tmp, track)
		*res = append(*res, tmp)
	}
	history := [201]int{}
	for i := index; i < len(nums); i++ {
		if len(track) > 0 && nums[i] < track[len(track)-1] || history[nums[i]+100] == 1 {
			continue
		}
		history[nums[i]+100] = 1
		track = append(track, nums[i])
		backtracking(track, nums, i+1, res)
		track = track[:len(track)-1]
	}
}
```

#### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

给定一个不含重复数字的数组 `nums` ，返回其 **所有可能的全排列** 。你可以 **按任意顺序** 返回答案。

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**示例 2：**

```
输入：nums = [0,1]
输出：[[0,1],[1,0]]
```

**示例 3：**

```
输入：nums = [1]
输出：[[1]]
```

**提示：**

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- `nums` 中的所有整数 **互不相同

```go
func permute(nums []int) [][]int {
	var res [][]int
	var track []int
	used := make(map[int]bool, len(nums))
	backtracking(track, nums, used, &res)
	return res
}

func backtracking(track, nums []int, used map[int]bool, res *[][]int) {
	if len(track) == len(nums) {
		tmp := make([]int, len(track))
		copy(tmp, track)
		*res = append(*res, tmp)
		return
	}
	for i := 0; i < len(nums); i++ {
		if used[i] == true {
			continue
		}
		used[i] = true
		track = append(track, nums[i])
		backtracking(track, nums, used, res)
		used[i] = false
		track = track[:len(track)-1]
	}
}
```

####  [47. 全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

给定一个可包含重复数字的序列 `nums` ，**按任意顺序** 返回所有不重复的全排列。

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**提示：**

- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`

```go
func permuteUnique(nums []int) [][]int {
	var res [][]int
	var track []int
	sort.Ints(nums)
	used := make(map[int]bool, len(nums))
	backtracking(track, nums, used, &res)
	return res
}

func backtracking(track, nums []int, used map[int]bool, res *[][]int) {
	if len(track) == len(nums) {
		tmp := make([]int, len(track))
		copy(tmp, track)
		*res = append(*res, tmp)
		return
	}
	for i := 0; i < len(nums); i++ {
		if i > 0 && nums[i] == nums[i-1] && used[i-1] == false {
			continue
		}
		if used[i] == true {
			continue
		}
		used[i] = true
		track = append(track, nums[i])
		backtracking(track, nums, used, res)
		used[i] = false
		track = track[:len(track)-1]
	}
}
```



## 贪心

## 动态规划

## 单调栈
