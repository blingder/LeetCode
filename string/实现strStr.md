```go
func strStr(haystack string, needle string) int {
outer:
	for i := 0; i <= len(haystack)-len(needle); i++ {
		for k := range needle {
			if needle[k] != haystack[i+k] { // 有不匹配的时候跳到上一个循环i+1，这里重新开始匹配
				continue outer
			}
		} 
// 能走到这一步说明有全部匹配的上的子字符串，要不然就是到最后i>len(haystack)-len(needle)时outer循环结束
		return i 
	}
	return -1
}
```

