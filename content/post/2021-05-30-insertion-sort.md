---
title: "Algorithm toolbox: Insertion Sort"
date: 2021-05-30
hero: /images/enter-too.jpg
excerpt: "Some implementations of more advanced algorithms will even switch from using their more advanced methodology to insertion sort when the list gets small enough."
timeToRead: 5
authors:
  - Cesar Jimenez
draft: false
---

# Insertion Sort

In this article we'll focus in undertanding **insertion sort**.

There are benefits of using insertion sort. Though is not very efficient when sorting large arrays (or lists), in smaller arrays because of their low constant value it usually outperforms more advanced algorithms such as quick sort and/or merge sort.

Some implementations of those advanced algorithms will even switch from using their more advanced methodology to insertion sort when the list gets small enough. In practice, insertion sort is also usually more efficient than other quadratic sorting algorithms such as bubble sort or selection sort.

In the worst case, insertion sort runs in **O(n²)**, or quadratic, time. It also sorts in place for a space complexity of **O(1)**. Insertion sort is a great example of a time-space tradeoff, sacrificing speed in order to conserve memory.

Insertion sort is also stable. A stable sorting algorithm is any algorithm that won’t change the relative order of items in a list that have the same value.

Insertion sort is also adaptive, meaning it works well with arrays that are already partially or fully sorted, reducing it's run time to **O(nk)** where each element in the list is no more than k elements away from it’s sorted position.

## Implementing Insertion sort

Insertion sort works by moving from left to right over an array. If the item to the left is smaller than the index it inserts the smaller number in the left side. It then moves the pointer to that previously inserted number and checks whether it is smaller than the previous one and so on.

```javascript
function insertionSort(input) {
  for (let i = 0; i < input.length; i++) {
  	// keep a temporary pointer to the number to sort
    let temp = input[i];
    let pointer = i;
    // if the temp is less than the previous one
    while (pointer > 0 && temp < input[pointer - 1]) {
      // make the current pointer the previous one
      input[pointer] = input[pointer - 1];
      // move back and check again
      pointer--;
    }
    // once the number is not less anymore
    // set the pointer to the temp variable
    input[pointer] = temp;
  }
  // return the sorted array
  return input;
}
```

That is insertion sort. Now you are able to implement it yourself!