---
title: "Graphs 101: Let's BFS and DFS"
date: 2021-06-04
hero: /images/graph.jpg
excerpt: "In this article we will dive into graph basics.  There are two graph traversals: breadth first search and depth first search."
timeToRead: 3
authors:
  - Cesar Jimenez
draft: false
---

# Graphs 101: Let's BFS and DFS.

In this article we will dive into graph basics.

The 2 most common used representation of graphs are the adjacency list and adjacency matrix.

Adjacency list

```javascript
	adjacencyList = {
		1: [2, 4],
		2: [1, 3],
		3: [2, 4],
		4: [1, 3]
	}
```


## Graph Traversals

There are two graph traversals: breadth first search and depth first search.

### Breadth First Search

BFS visits the nodes one level at a time. To prevent visiting the same node more than once, we'll maintain a visited object.

For BFS we utilize a **Queue** to process the nodes in a First In First Out fashion.  The time complexity is **O(v+e)**.

#### Pseudocode

```javascript
/*
	pcode:
	- create result array variable
	- create a queue variable
	- create a visited map
	- add the starting vertex to the queue & visited map
	- while queue is not empty:
	  - dequeue current vertex
	  - push current vertex to result array
	  - loop thru current vertex adjacency list:
	    - for each adjacent vertex, if vertex is unvisited:
	    	- add vertex to visited map
	    	- enqueue vertex
	- return result array
*/
```

#### Code

```javascript
// code:
function bfs(node) {
	const result = [];
	const queue = [node];
	const visited = {};
	visited[start] = true;

	while (queue.length) {
		let currVertex = queue.pop();
		result.push(currVertex);

		adjacencyList[currVertex].forEach(edges => {
			if (!visited[edges]) {
				visited[edges] = true;
				queue.unshift(edges);
			}
		});
	}
	return results;
}
```

### Depth First Search

DFS visits the nodes depth wise so we will use a **Stack** in order to process Last In First Out fashion.

Starting from a vertex, we'll push the neighboring vertices to our stack.  Whenever a vertex is popped, it is marked visited in our visited object. Its neighboring vertices are pushed to the stack.  Since we are always popping a new adjacent vertex, our algorithm will always explore a new level.

We can also use the intrinsic stack calls to implement DFS recursively.

The time complexity is the same as BFS, **O(v+e)**.

#### Pseudocode

```javascript
/*
	pcode:
	- create a stack array
	- create a result array
	- create a visited map
	- push the starting vertex to the stack & visited map
	- while the stack is not empty:
		- pop and store the vertex
		- push current vertex to result array
		- loop thru current vertex adjacency list:
			- for each adjacent vertex, if vertex is unvisited:
				- add vertex to visited map
				- push vertex to stack
	- return result array
*/
```

#### Code

```javascript
// code:
function dfsRecursively(node) {
	const result = [];
	const visited = {};

	function dfs(vertex) {
		// base case
		if (!vertex) return null;

		// set visited
		visited[vertex] = true;
		result.push(vertex);

		// recursive action
		adjacencyList[vertex].forEach(edge => {
			if (!visited[edge]) {
				return dfs(edge);
			}
		});
	}

	dfs(node);

	return result;
}

function dfsIterative(node) {
	const result = [];
	const stack = [node];
	const visited = {};
	visited[start] = true;

	while (stack.length) {
		let currVertex = stack.pop();
		result.push(currVertex);

		adjacencyList[currVertex].forEach(edge => {
			if (!visited[edge]) {
				visited[edge] = true;
				stack.push(edge);
			}
		});
	}

	return result;
}
```

There it is, now let's see how to use this to solve problems.
