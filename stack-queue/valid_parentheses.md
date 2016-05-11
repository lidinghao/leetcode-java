# 20. Valid Parentheses
## 问题描述
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
## 分析
利用栈，将输入的字符依次入栈，发现对应的括号就从栈中弹出一个元素，最后栈为空，则Parentheses is valid,否者 invalid。
实现复杂度为O(n),空间复杂度也为O(n)。
## 代码实现
