# Reverse Nodes in k-Group
## 问题描述
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

## 分析

## 扩展
这种题目，考察的主要是控制结构，这样在复杂的控制流程中写出正确，清晰的代码。
最主要的是要把控制流程的代码和正常的业务逻辑代码分开。首先要通过函数把不同的逻辑分开，其次要在代码中，把复杂的控制逻辑写在for中，而不是用while把业务逻辑和控制逻辑写在一起。