# Implement a Sudoku Solver From Scratch

<h1>Name: Mohamed Zabir Khan A</h1>
<h1> Register Number: 212224230162</h1>

<h1> Aim: </h1>

To implement a Sudoku solver from scratch using the backtracking algorithm by validating each number placement and recursively exploring all possible solutions until the puzzle is solved.

## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>

<hr>
<h1> Program: </h1>

```
M = 9

def print_grid(grid):
    for row in grid:
        print(" ".join(str(num) for num in row))

def is_safe(grid, row, col, num):
    for x in range(M):
        if grid[row][x] == num:
            return False
    for x in range(M):
        if grid[x][col] == num:
            return False
    start_row = row - row % 3
    start_col = col - col % 3
    for i in range(3):
        for j in range(3):
            if grid[i + start_row][j + start_col] == num:
                return False
    return True

def solve_sudoku(grid, row=0, col=0):
    if row == M - 1 and col == M:
        return True
    if col == M:
        row += 1
        col = 0
    if grid[row][col] > 0:
        return solve_sudoku(grid, row, col + 1)
    for num in range(1, M + 1):
        if is_safe(grid, row, col, num):
            grid[row][col] = num
            if solve_sudoku(grid, row, col + 1):
                return True
        grid[row][col] = 0
    return False

puzzle = [
    [3, 0, 6, 5, 0, 8, 4, 0, 0],
    [5, 2, 0, 0, 0, 0, 0, 0, 0],
    [0, 8, 7, 0, 0, 0, 0, 3, 1],
    [0, 0, 3, 0, 1, 0, 0, 8, 0],
    [9, 0, 0, 8, 6, 3, 0, 0, 5],
    [0, 5, 0, 0, 9, 0, 6, 0, 0],
    [1, 3, 0, 0, 0, 0, 2, 5, 0],
    [0, 0, 0, 0, 0, 0, 0, 7, 4],
    [0, 0, 5, 2, 0, 6, 3, 0, 0]
]

if solve_sudoku(puzzle):
    print_grid(puzzle)
else:
    print("No solution exists")
```

<hr>
<h1> Output: </h1>

![Screenshot 2025-04-24 214840](https://github.com/user-attachments/assets/1d6a6e53-bfdb-42d4-aebe-ec1a26456e3f)

<hr>
<h1> Result: </h1>

The Sudoku solver was successfully implemented from scratch using the backtracking algorithm, effectively validating and placing numbers to solve the puzzle.
