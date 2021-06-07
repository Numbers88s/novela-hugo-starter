---
title: "Graph toolbox: Let's solve search maze problem"
date: 2021-06-05
hero: /images/maze.jpg
excerpt: "In this article we will look to solve one of the classic graph problems, searching in a maze."
timeToRead: 5s
authors:
  - Cesar Jimenez
draft: false
---

# Solving Search Maze

In this article we will look to solve one of the classic graph problems, searching in a maze.

## Problem statement

```javascript
/*
 * Given a 2D array of O and X entries representing a maze with
 * designated entrance and exit points, find a path from the
 * entrance to the exit, if one exists. 😳
 */
```

We will represent the O entries with 0's and X entries with 1's. The O entries represent open areas and the X entries represent walls. The entrance and the exit points are represented by an array, the 0th index represents the column and the 1th index represent the row.

```javascript
maze = [
  [0,0,1,0,0],
  [0,0,0,0,0],
  [0,0,0,1,0],
  [1,1,0,1,1],
  [0,0.0.0.0]
];
```

## Understanding the problem

We can use a DFS approach to recursively traverse the maze.

We first think of our **base case**, or how we will know when to stop recursing, is either

1. **We have reached our exit and we'd set our hasPath variable to true**
2. **We have visited every O entry and did not find the exit so we return**.
3. **We are out of bounds** so we'd return out of the recurion.
4. **We are in a visited index so we'd return**

Our time complexity for this would be **O(v+e)**.

In order to keep track of the cells we have **visited**, we will replace the O with 1.

Our **recursive action** will be to move to all the positions we are able. We will capture this movement by increasing or decreasing either our column or our row. We are able to move:

* **up**: `col, row + 1`
* **down**: `col, row - 1`
* **right**: `col + 1, row `
* **left**: `col - 1, row`

We are not able to move diagonally.

## Diagram

```javascript
// Entry and Exit variables
let entry = [0, 4]
let exit = [3, 2]

// We are marking the entrance with an E
// and marking the exit with an X
// The I represent all the nodes visited.

let maze =
[    0 1 2 3 4
  0	[0,0,1,I,E],
  1	[0,I,I,I,I],
  2	[0,I,I,1,I],
  3	[1,1,X,1,1],
  4	[0,0.0.0.0]
]

```

## Pseudocode

```javascript
/*
	pcode:
	- create a hasPath variable
	- create a startCol variable
	- create a startRow variable
	- create recursive function
		- base case
			- if we found destination set hasPath as true
			- if out of bounds return
			- if we have visited return
		- mark current col & row in maze as visited (set to 1)
		- recusive actions:
			- call recursion on all four directions
				- col, row + 1
				- col, row - 1
				- col + 1, row
				- col - 1, row
	- set startCol and startRow in the maze as visited (set to 1)
	- instantiate recursive function for all four directions
	- return hasPath
*/
```
## Code

```javascript
function solveMaze(maze, start, destination) {
  let hasPath = false;
  let startCol = start[0];
  let startRow = start[1];

  function dfs(col, row) {
    // base cases
    // we found it
    if (col == destination[0] && row == destination[1]) {
      hasPath = true;
      return;
    }

    // its out of bounds
    if (col < 0 || col > maze.length || row < 0 || row > maze[col].length) {
      return;
    }

    // we have visited already
    if (maze[col][row] !== 0) {
      return;
    }

    // mark as visited
    maze[col][row] = 1;

    // recursive action
    // top
    dfs(col, row + 1);

    // right
    dfs(col + 1, row);

    // bottom
    dfs(col, row - 1);

    // left
    dfs(col - 1, row);
  }

  // mark as visited
  maze[startCol][startRow] = 1;

  // traverse all four directions
  dfs(startCol, startRow + 1);
  dfs(startCol, startRow - 1);
  dfs(startCol + 1, startRow);
  dfs(startCol - 1, startRow);

  return hasPath;
}

let maze = [
	[0, 0, 1, 0, 0],
	[0, 0, 0, 0, 0],
	[0, 0, 0, 1, 0],
	[1, 1, 0, 1, 1],
	[0, 0, 0, 0, 0]
];

solveMaze(maze, [0, 4], [3, 2])
```

Well that was fun. Let's see what other graph problem we can solve.