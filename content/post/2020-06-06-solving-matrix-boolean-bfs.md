---
title: "Graph toolbox: Solving Paint a Boolean Matrix"
date: 2021-06-06T20:07:44-07:00
hero: /images/matrix.jpg
excerpt: "In this article we will look to solve another classic graph and matrix problem, painting a boolean matrix."
timeToRead: 4
authors:
  - Cesar Jimenez
draft: false
---

# Solving Paint a Boolean Matrix

In this article we will look to solve another classic graph and matrix problem, painting a boolean matrix.

## Problem statement

```javascript
/*
 * Implement an algorithm that takes an n x m boolean array
 * together with an entry (x, y) and flips the color of
 * the region associated with (x, y).
 */
```

The 2 colors will be represented by 0's and 1's.

For this example, we will start in the center of the array or `[1,1]`.  Since we are starting in the center we will only be able to flip the upper, leftmost triangular matrix.

It's easier to understand by seeing it. See below:

```javascript
let starting = [
	[1, 1, 1],
	[1, 1, 0],
	[1, 0, 1]
]

let ending = {
	[0, 0, 0],
	[0, 0, 0],
	[0, 0, 1]
}

// Visual representation of what changed
let visual = [
	[X, X, X],
	[X, X, 0],
	[X, 0, 1]
]
```

## Understanding the problem

We can use a BFS approach to traverse the matrix.

Like in any matrix problem will need to check that we are within bounds of the matrix. We would also need to check the new position is colored the same as the previous position. If the new position fits the requirements, its color is flipped.

Our time complexity for this would be **O(mn)**

## Pseudocode

```javascript
/*
pcode:
- create color variable with image[x][y]
- set coordinate to the opposite color
- create a queue
- add all four direction from the starting point to the queue
- while the queue is not empty
	- if the direction is within bounds and the color is the same as our initial color then
		- set the color to the opposite to mark as visited
		- queue all four directions from there
- return image
*/
```

## Code

```javascript

function flipColorMatrix(image, x, y) {
  let color = image[x][y];
  image[x][y] = Number(!color);

  let queue = [];
  queue.unshift([x, y + 1]);
  queue.unshift([x + 1, y]);
  queue.unshift([x, y - 1]);
  queue.unshift([x - 1, y]);

  while (queue.length) {
    let [col, row] = queue.pop();

    if (col >= 0 && col < image.length && row >= 0 && row < image[col].length && image[col][row] == color) {
      image[col][row] = Number(!color);

      queue.unshift([col, row + 1]);
      queue.unshift([col + 1, row]);
      queue.unshift([col, row - 1]);
      queue.unshift([col - 1, row]);
    }
  }

  return image;
}

const image = [[1, 1, 1], [1, 1, 0], [1, 0, 1]];
console.log(flipColorMatrix(image, 1, 1));
```

Like in any matrix problem, its all about making sure you stay within the bounds while you are solving the problem.