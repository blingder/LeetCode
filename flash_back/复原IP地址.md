```go
func restoreIpAddresses(s string) []string {
	// 结果接收
	var res, path []string
	// 功能函数
	var backTracking func(s string, startIndex int)
	backTracking = func(s string, startIndex int) {
		// 返回条件（添加结果）
		if len(s)-startIndex == 0 && len(path) == 4 { // 能走到这最后一步，并且path满足长度就加入结果集
			tmp := path[0] + "." + path[1] + "." + path[2] + "." + path[3]
			res = append(res, tmp)
			return
		}
		// 单层逻辑
		for i := startIndex; i < len(s); i++ {
			// len(path)>=4或者不符合要求就没必要递归下去了，当然有时候会不到4，所以上面if语句要有len(path)==4
			if len(path) < 4 && isNormalIp(s, startIndex, i) {
				path = append(path, s[startIndex:i+1])
				backTracking(s, i+1)
			} else {
				continue
			}
			// 回溯
			path = path[:len(path)-1]
		}
	}
	// 调用函数
	backTracking(s, 0)
	// 返回结果
	return res
}
func isNormalIp(s string, startIndex, i int) bool {
	if i-startIndex >= 3 { // 长度不能大于3
		return false
	}
	if i-startIndex > 0 && s[startIndex] == '0' { // 第一个数不能为0
		return false
	}
	checkInt, _ := strconv.Atoi(s[startIndex : i+1])
	if checkInt > 255 { // 数值不能大于255
		return false
	}
	return true
}
```

