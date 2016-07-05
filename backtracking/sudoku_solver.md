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
```java
    public void solveSudoku(char[][] board) {
        if (board == null || board.length == 0)
            return;
        solve(board);

    }

    public static boolean solve(char[][] board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    for (char k = '1'; k <= '9'; k++) {
                        board[i][j] = k;
                        if (isValid(board, i, j) && solve(board))
                            return true;
                        else
                            board[i][j] = '.';
                    }
                    return false;
                }

            }
        }

        return true;

    }

    public static boolean isValid(char[][] board, int i, int j) {
        for (int col = 0; col < 9; col++) {
            if (col != j && board[i][col] == board[i][j])
                return false;
        }
        for (int row = 0; row < 9; row++) {
            if (row != i && board[row][j] == board[i][j])
                return false;
        }
        for (int row = (i / 3) * 3; row < (i / 3) * 3 + 3; row++) {
            for (int col = (j / 3) * 3; col < (j / 3) * 3 + 3; col++) {
                if ((row != i || col != j) && board[row][col] == board[i][j])
                    return false;
            }
        }
        return true;
    }
```

## 复杂度分析
Many recursive searches can be modeled as a tree. In Sodoku, you have 9 possibilities each time you try out a new field. At maximum, you have to put solutions into all 81 fields. At this point it can help drawing it up in order to see, that the resulting search space is a tree with a depth of 81 and a branching factor of 9 at each node of each layer, and each leaf is a possible solution. Given these numbers, the search space is 9^81.

Since you don't check if the solution is correct after trying 81 times but after each try, the actual search space is way smaller. I don't know how to put it into numbers really, maybe the branching factor gets smaller by 1 each time you set n tries, as a rough estimate. But given any Sodoku with k pre-set numbers, you can with 100% certainty say, that you will need at most n^(n²-k) tries.