---
title: "Algorithm toolbox: Bubble Sort"
date: 2021-05-30
hero: /images/bubble.jpg
excerpt: "Bubble sort is a simple comparison algorithm with a quadratic runtime of **O(n²)** time. This algorithm is simple and easy to implement, however it is important to note that it is the most inefficient sorting algorithm in our arsenal."
timeToRead: 3
authors:
  - Cesar Jimenez
draft: false
---

# Bubble Sort

In this article we'll focus on undertanding **bubble sort**.

Bubble sort is a simple comparison algorithm with a quadratic runtime of **O(n²)** time. This algorithm is simple and easy to implement, however it is important to note that it is the most inefficient sorting algorithm in our arsenal.

Bubble sort compares every pair of adjacent values and swap positions if the first value is greater than the second. During each pass through the array, the largest value “bubbles up” to the top, and after each pass the elements furthest to the right are in the correct order.

Here’s an example:

With array of [5,3,1,4,6] let's use bubble sort to sort in ascending order. Bubble sort first compares the first pair of values, 5 & 3. Since 3 is smaller than 5, it swaps the values and moves on to compare the next two pairs, 5 & 1. It continues until the array is fully sorted.

First pass: [**5**,**3**,1,4,6] → [3,**5**,**1**,4,6] → [3,1,**5**,**4**,6] → [3,1,4,**5**,**6**] → [3,1,4,5,6]

Second pass: [**3**,**1**,4,5,6] → [1,**3**,**4**,5,6] → [1,3,**4**,**5**,6] → [1,3,4,**5**,**6**] → [1,3,4,5,6]

Third pass: [**1**,**3**,4,5,6] → [1,**3**,**4**,5,6] → [1,3,**4**,**5**,6] → [1,3,4,**5**,**6**] → [1,3,4,5,6]

Please note how the array was already sorted by the second pass. This is what makes it the most inefficient sorting algorithm.  Bubble sort needs a final pass through the entire array to make sure no other swaps are necessary.

## Implementing Bubble sort

Let’s look at the code:

```javascript
function bubbleSort(input){
  // set a swap variable
  let swap;
  let endIndex = input.length;
  while (endIndex--){
    // set the swap method to false
    swap = false;
    // loop thru the array
    for (let i = 0; i < endIndex; i++) {
      // if the element to the right is less
      // than the element to the left
      if (input[i] > input[i + 1]) {
        // swap then
        [input[i], input[i + 1]] = [input[i + 1], input[i]];
        // and set the swap variable to tru
        swap = true;
      }
    }
    // if there is no need to swap then break.
    if (!swap) { break; }
  }

  // return sorted array
  return input;
}

```

That’s bubble sort, a good algorithm to understand and know when to implement. Mostly never.