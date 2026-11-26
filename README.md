# 8-Puzzle Solver — Greedy Best-First Search

Solving the 8-puzzle with greedy best-first search, and comparing three heuristics against breadth-first search (optimal) and a random walk over 50 start states.

Goal state:

```
1 4 7
2 5 8
3 6 _
```

## Heuristics

- **h1, misplaced tiles:** how many tiles are not in their goal cell
- **h2, Manhattan distance:** rows + columns each tile is away from its goal
- **h3, row + column:** +1 for each tile in the wrong row, +1 for each tile in the wrong column

## Results (average over 50 start states)

| Method | Moves in solution | States expanded |
|---|---|---|
| Greedy, h1 misplaced | 41.3 | 557.5 |
| Greedy, **h2 Manhattan** | **38.2** | **273.7** |
| Greedy, h3 row + column | 53.8 | 322.9 |
| BFS (optimal) | 18.6 | 47,965 |

- Manhattan distance was the best heuristic on both speed and path length.
- Greedy search expands about 86–175× fewer states than BFS, but its solutions are about twice as long as the optimal ones because it ignores path cost.

## What broke

- **The start state in the assignment could not be solved.** The search never finished on it. Counting inversions showed why: the start state had 18 (even) and the goal had 9 (odd). Legal moves can't change that parity, so no solution exists. I added an `is_solvable()` check and swapped tiles 8 and 3 to get a solvable version.
- **Random test states had to be guaranteed solvable.** Instead of shuffling tiles (half of those states are unsolvable), the code starts at the goal and makes random legal moves, without undoing the previous move.

## Files

- `8puzzle.py`: all search code, the 50-state experiment, tables and plots (exported from Colab)
- `report.pdf`: full report with the results for all 50 states

## Run it

```
pip install pandas matplotlib ipython
python 8puzzle.py
```

Best run in Jupyter or Colab, where the styled tables display properly.
