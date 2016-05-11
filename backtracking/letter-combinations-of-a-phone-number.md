# 17. Letter Combinations of a Phone Number
## 问题
Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![keyboard](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
## 分析
可以采用两种方式来分析思考本题，一种是回溯，一种是组合。
采用回溯时，可以认为digits中的第一个元素为根节点

