# Longest Valid Parentheses

## 问题描述
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

## 分析
遍历字符串，并用栈记录当前索引，对于每个字符：

1. 如果当前字符为'(',则将索引入栈。
2. 如果当前字符为')', 栈顶对应的字符为')'，则将栈顶元素弹出，并用当前索引减去栈顶索引，得到一个新的长度curLen，将curLen与原先保存的最大长度比较，更新最大长度。
3. 如果当前字符为')',栈为空，或栈顶对应的字符为')',则将索引压栈。

## 代码实现
```java
    public int longestValidParentheses(String s) {
        if (s.length()==0) {
            return 0;
        }
        char[] chars = s.toCharArray();
        Stack<Integer> stack = new Stack<>();
        int maxLen = 0;
        for (int i = 0; i < chars.length; i++) {
            if (chars[i] == '(') {
                stack.push(i);
            } else if (!stack.isEmpty() && chars[stack.peek()] == '(') {
                stack.pop();
                int curLen = 0;
                if (!stack.isEmpty()) {
                    curLen = i - stack.peek();
                } else {
                    curLen = i + 1;
                }
                maxLen = Math.max(maxLen, curLen);
            } else {
                stack.push(i);
            } 
        }
         return maxLen;
    }
```