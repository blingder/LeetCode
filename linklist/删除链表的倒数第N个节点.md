```go
func removeNthFromEnd(head *ListNode, n int) *ListNode {
	dummy := &ListNode{Next: head} // 必要的
	fast := dummy
	slow := dummy

	for i := 0; i <= n; i++ { // 快指针先移动n+1次
		fast = fast.Next
	}
	for fast != nil {
		fast = fast.Next
		slow = slow.Next
	}

	slow.Next = slow.Next.Next
	return dummy.Next
}
```

删除最好要设置为有头节点，这样可以适应删到没有元素的情况