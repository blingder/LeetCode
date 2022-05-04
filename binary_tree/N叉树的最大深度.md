```go
// 利用的是层序遍历方法
func maxDepth(root *Node) int {
	// 空时直接返回
	if root == nil {
		return 0
	}
	depth := 0
	// 初始化一个队列
	queue := list.New()
	// 根节点先入队
	queue.PushBack(root)
	// 队不为空一直循环
	for queue.Len() > 0 {
		length := queue.Len() // length记录这一层有几个节点
		for i := 0; i < length; i++ {
			// 将当前层出队
			node := queue.Remove(queue.Front()).(*Node)
			// 下一层入队
			for _, v := range node.Children {
				queue.PushBack(v)
			}
		}
		// 每层深度加一
		depth++
	}
	// 返回结果
	return depth
}
```

