```go
func solveNQueens(n int) [][]string {
	// 声明返回值res
	var res [][]string
	// 初始化棋盘chessboard
	chessboard := make([][]string, n)
	// 初始化棋盘的行
	for i := 0; i < n; i++ {
		chessboard[i] = make([]string, n)
	}
	// 设置棋盘的初始值
	for i := 0; i < n; i++ {
		for j := 0; j < n; j++ {
			chessboard[i][j] = "."
		}
	}
	// 声明backtrack函数
	var backtrack func(int)
	// 编写函数功能
	backtrack = func(row int) {
		// 返回条件
		if row == n {
			// 初始化一个中间值
			temp := make([]string, n)
			// 将chessboard每行合成一个字符串存入temp[i]
			for i, rowStr := range chessboard {
				temp[i] = strings.Join(rowStr, "")
			}
			// temp存入res
			res = append(res, temp)
			return
		}
		// 每层开始遍历
		for i := 0; i < n; i++ {
			// 满足条件可以放皇后
			if isValid(n, row, i, chessboard) {
				// 放入皇后
				chessboard[row][i] = "Q"
				// 递归
				backtrack(row + 1)
				// 回溯
				chessboard[row][i] = "."
			}
		}
	}
	// 调用backtrack
	backtrack(0)
	// 返回res
	return res
}
func isValid(n, row, col int, chessboard [][]string) bool {
	// 检查列
	for i := 0; i < row; i++ {
		if chessboard[i][col] == "Q" {
			return false
		}
	}
	// 45度角
	for i, j := row-1, col-1; i >= 0 && j >= 0; i, j = i-1, j-1 {
		if chessboard[i][j] == "Q" {
			return false
		}
	}
	// 135度角
	for i, j := row-1, col+1; i >= 0 && j < n; i, j = i-1, j+1 {
		if chessboard[i][j] == "Q" {
			return false
		}
	}
	// 全都可以返回true
	return true
}
```



注释已经思路已经很清晰了，在isValid函数中没有检查行是因为在回溯函数每行遍历中每行只选取一个，所以行里面是不会重复的