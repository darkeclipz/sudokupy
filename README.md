# Fast Sudoku solver in Python with forward propagation

This is a fast Sudoku solver written in Python. It is inspired by the algorithm for solving constraint satisfaction problems (CSP). Essentially, it is a hard-coded CSP solver specifically for Sudoku.

The order of assignment of variables is determined by the minimum remaining values heuristic (MRV). This ensures that the search space is reduced very fast, and it fails quickly.

If a value is set, this value is removed from all the neighbouring cells that share the same constraint. If a cell has no more allowed values remaining, then the assignment is invalid (unless it is the last cell). 

This method gives two cool benefits:
    
1. The first is that is that if a puzzle can be solved without guessing, the algorithm will follow this route. This is the result of the MRV heuristic.

2. Secondly, we do not have to check if the contraints are met. Because the assigned value is removed from the allowed values for every cell that shares the same constrait, it is impossible to assign an invalid value, unless the puzzle is invalid to begin with.


## Example usage

```python
hardest_puzzle = "800000000003600000070090200050007000000045700000100030001000068008500010090000400"

from sudoku import SudokuSolver

solver = SudokuSolver(hardest_puzzle)
solver.solve()
solver.print_board()
solver.print_statistics()
```

Running the example will give the following output:

```
------- board -------
8 1 2 | 7 5 3 | 6 4 9
9 4 3 | 6 8 2 | 1 7 5
6 7 5 | 4 9 1 | 2 8 3
---------------------
1 5 4 | 2 3 7 | 8 9 6
3 6 9 | 8 4 5 | 7 2 1
2 8 7 | 1 6 9 | 5 3 4
---------------------
5 2 1 | 9 7 4 | 3 6 8
4 3 8 | 5 2 6 | 9 1 7
7 9 6 | 3 1 8 | 4 5 2

------- statistics -------
Total assignments: 14393
Runtime: 0.3474690914154053 seconds
```

If the provided puzzle string is an invalid puzzle, the solver will throw an `InvalidPuzzleError`.