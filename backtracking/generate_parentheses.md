# Generate Parentheses
## 问题描述

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"

## 分析
采用递归的方式构造括号串，当左括号数量 < n 时，添加左括号，直到=n,然后添加右括号，并不断回溯递归，直到右括号数量=n。
## 代码实现

```java
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result,"", 0, 0, n);
        return result;
    }

    private void backtrack(List<String> result, String str, int open, int close, int n) {
        if (str.length() == 2 * n) {
            result.add(str);
            return;
        }
        if (open < n) {
            backtrack(result, str + "(", open + 1, close, n);
        }
        if (close < open) {
            backtrack(result, str + ")", open, close + 1, n);
        }

    }
```