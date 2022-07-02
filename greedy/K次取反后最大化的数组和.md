```go
func largestSumAfterKNegations(nums []int, k int) int {
	sort.Slice(nums, func(i, j int) bool { // 绝对值大小倒序排序
		return math.Abs(float64(nums[i])) > math.Abs(float64(nums[j])) // abs: 取绝对值
	})
	for i, v := range nums { // 排序完成后优先变换绝对值最大的负数
		if v < 0 && k > 0 {
			nums[i] = -nums[i]
		}
	}
	if k%2 == 1 { // 如果K为奇数时变动最小的那个
		nums[len(nums)-1] = -nums[len(nums)-1]
	}
	res := 0
	for _, v := range nums { // 把结果加起来
		res += v
	}
	return res
}
```

