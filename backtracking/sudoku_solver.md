# Sudoku Solver
## 问题描述
Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.
![sudoku 1](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
A sudoku puzzle...
![sudoku 2](http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)
...and its solution numbers marked in red.

## 分析
应该是采用回回溯的方式来对每个空白的地方进行不断的尝试。注意，在尝试之前可以进行一些预处理，去掉那些本行本列中以及存在的数，只尝试那些没出现的数。

## 代码实现