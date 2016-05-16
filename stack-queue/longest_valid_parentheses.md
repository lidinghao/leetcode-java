# Longest Valid Parentheses

## 问题描述
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

## 分析
遍历字符串，并用栈记录当前索引，如果当前字符和栈顶索引指向的字符构成了“()”，则将栈顶元素弹出，并用当前索引减去此时栈顶索引，得到一个新的长度curLen，将curLen与原先保存的最大长度比较，并更新最大长度。