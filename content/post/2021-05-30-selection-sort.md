---
title: "Algorithm toolbox: Selection Sort"
date: 2021-05-29
hero: /images/vending.jpg
excerpt: "Selection sort is a simple comparison algorithm with a quadratic runtime of **O(n²)** time. This algorithm is simple and easy to implement, however it is also very inefficient though not more so than bubble sort!"
timeToRead: 3
authors:
  - Cesar Jimenez
draft: false
---

# Selection Sort

In this article we'll focus in undertanding **selection sort**.

Selection sort is a simple comparison algorithm with a quadratic runtime of **O(n²)** time. This algorithm is simple and easy to implement, however it is also very inefficient though not more so than bubble sort!

Selection sort works by looping through the array linearly, selecting the smallest element, and then swapping it to the first position. Then loop again linearly and get the second smallest element, swapping it to the second position, and so on and so forth until the array is completely sorted.

## Implementing Selection sort
Let’s look at the code:

```javascript
function selectionSort(input) {
  // loop thru the array
  for (let i = 0; i < input.length; i++) {
  	// create min variable
    let min = input[i];
    // keep track of the min index
    let minIndex = i;
    // loop thru every other element
    for (let j = i + 1; j < input.length; j++) {
      // and find a smaller element
      if (input[j] < min) {
        // once you do, update your min & minIndex variables
        min = input[j];
        minIndex = j;
      }
    }
    // after going thru every element you should've found
    // the smallest amount and you swap the larger first
    // then the smallest.
    input[minIndex] = input[i];
    input[i] = min;
  }
  // return your sorted array.
  return input;
}
```

It's a pretty simple sorting algorithm to understand and implement.