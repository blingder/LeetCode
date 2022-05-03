```go
type Node struct {
	Val      int
	Children []*Node
}

func preorder(root *Node) []int {
	res := []int{}
	var fun func(root *Node)
	fun = func(root *Node) {
		if root == nil {
			return
		}
		res = append(res, root.Val) // 要是后序遍历就放在for之后
		for _, ch := range root.Children { //[]*Node  ch为当前节点的Children节点
			fun(ch)
		}
	}
	fun(root)
	return res
}
```

