---
title: "Intermediate Graph: Principles of Dijkstra's and Bellman Ford's Algorithm"
date: 2021-06-13T20:10:55-07:00
hero: /images/connection.jpg
excerpt: "In this article we will look at two very important graph algorithms, Djiktra’s algorithm as well as Bellman Ford’s algorithm."
timeToRead: 20
authors:
  - Cesar Jimenez
draft: false
---

In this article we will look at two very important graph algorithms, Djiktra’s algorithm as well as Bellman Ford’s algorithm.

> Find a path between two nodes in a graph such that the sum of the weights of its constituent edges is minimized.

Though both of these algorithms are used to find the shortest path, they have a subtle difference. Bellman Ford finds the shortest path from a single source to all the other nodes, whereas Djistra’s finds the shortest path to every other node.  Another important difference is that Djisktra’s doesn’t always find the shortest path when the weighted edges are negative, whereas Bellman Ford does.

Let’s start with Dijkstra’s algorithm.


## Dijkstra’s algorithm.

For Dijkstra’s algorithm we will use BFS approach with a priority queue. Now since we don’t have those types in Javascript we will need to create them.
Let’s create the priority queue.

```javascript
class QueueItem {
	constructor(node, weight) {
		this.node = node;
		this.weight = weight;
	}
}

class PriorityQueue {
	constructor() {
		this.queue = [];
		this.size = this.queue.length;
	}

	enqueue(node, weight) {
		let item = new QueueItem(node, weight);
		let isPriority = false;

		for (let i = 0; i < this.queue.length; i++) {
			if (this.queue[i].weight > item.weight) {
				this.queue.splice(i, 0, item);
				isPriority = true;
				break;
			}
		}

		if (!isPriority) {
			this.queue.push(item);
		}
	}

	dequeue() {
		return this.queue.pop();
	}
}
```

Next let’s create our Graph class.

```javascript
class Graph {
	constructor() {
		this.adjLst = {};
	}

	addVertex(v) {
		this.adjList[v] = [];
	}

	addEdges(vertex, node, weight) {
		this.adjList[vertex].push({ node, weight })
	}
}
```

Now we have all the pieces in place to build Djikstra’s Algorithm.
Let’s go over the pseudocode to make sure we understand how it all fits in.

```javascript
/*
pcode:
- create distance map
- create adjancency list for all nodes
- mark all node’s distances to infinity
- load weighted edge list into adjacency list
- create queue
- add starting node to priority queue with weight of 0
- set distance of starting node to 0
- while queue is not empty
	- dequeue node and weight
	- for all node’s neighbors
		- if the distance of current node + neighbor weight is less than the distance of the neighbors node
			- set the distance of the neighbor node to current node + neighbor weight
			- enqueue the neighbor node with updated weight
- return distance map to return all the shortest path per node
*/
```

That is it for Djikstra’s Algorithm.  Let’s code it up.

```javascript
Input:
	- weightedEdgeList = [[2,1,1],[2,3,1],[3,4,1]], // [vertex, edge, weight]
	- n = 4 // number of vertices starting at 1
	- k = 2 // starting node

function findShortestPath(weightedEdgeList, n, k) {
	let distance = {};
	let graph = new Graph();

	for (let i = 1; i < N; i++) {
		graph.addVertex(i);
		distance[i] = Infinity;
	}

	for (let i = 0; i < weightedEdgeList.length; i++) {
		let [vertex, edge, weight] = weightedEdgeList[i];
		graph.addEdges(vertex, edge, weight);
	}

	let qp = new PriorityQueue();
	distance[k] = 0;
	qp.enqueue(k, 0);

	while(qp.size !== 0) {
		let { node } = qp.dequeue();
		graph[node].forEach(neighbor => {
			let { node: _n, weight: _w } = neighbor;
			let d = distance[currNode] + _w
			if (d < distance[_n]) {
				distance[_n] = d;
				pq.enqueue(_n, d);
			}
		});
	}

	return distance;
}
```

This algorithm is very useful! Hope it serves you well.  Now let’s take a look at Bellman Ford’s algorithm.

## Bellman Ford

For Bellman Ford’s algorithm things are a little different.  We don’t necessarily need the priority queue nor do we need the graph. Since we already have a weighted edge list, we can use it to make our calculation directly.

Djikstra’s Algorithm relies on only visiting the nodes once. And since we only visit them once we only update them once. Bellman Ford’s algorithm has a different approach.  Bellman Ford says to visit all the nodes Vertex - 1 times. Meaning for all the N nodes visit each one N - 1 times.
We are still leveraging a distance map however. And we will set all the nodes to infinity except the starting one.

Let’s go over the pseudocode to understand it better.

```javascript
/*
pcode:
 - create a distance array variable
 - set the distance of all nodes to Infinity
 - set the start node in the distance node to 0
 - loop thru nodes
	 - for each of the weightedEdgeList => [source, target, weight]
		 - if the distance of the source node is Infinity continue the loop
		 - let d = distance[source] + weight
		 - if d < distance[target]
			 - distance[target] = d
- return distance array
*/
```

That’s it for Bellman Ford. Let’s code it up.

```javascript
Input:
	- weightedEdgeList = [[2,1,1],[2,3,1],[3,4,1]], // [source, target, weight]
	- n = 4 // number of vertices starting at 1
	- k = 2 // starting node

function BellmanFord(weightedEdgeList, n, k) {
	let distance = new Array(n + 1).fill(Infinity);
	distance[k] = 0;

	for (let i = 0; i < n; i++) {
		for (let j = 0; j < weightedEdgeList.length; j++) {
			let [source, target, weight] = weightedEdgeList[i];
			if (distance[source] === Infinity) continue;
			let d = distance[source] + weight;
			if (d < distance[target]) {
				distance[target] = d;
			}
		}
	}

	return distance;
}
```

In here we found the shortest path from the starting node to all the other nodes.

Hope you found this useful!
