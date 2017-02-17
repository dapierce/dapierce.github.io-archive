---
layout: post
title: "Notes on Sorting"
date: 2017-02-17 12:12:48 -0800
published: true
---

Recently, I had an assignment to create and test various sorting algorithms with input ranges from $$ n=10^2 $$ to $$ n=10^6 $$. Thinking that the larger sets of data might get unwieldy otherwise, I selected C++ to run the tests, hoping speed would carry on to the more inefficient brute force algorithms.

I didn't realize how much of a difference decrease and conquer made compared to brute force. Going over the basics of Big O notation you end up with simple terms like $$ O(n^2) $$ or $$ O(n \log n) $$ but the reality of these growth patterns doesn't really become obvious until you see a program chug all a of a core's cpu.

### The parameters

Our assignment had a few basic requirements:
1. Compares 4 sorting algorithms: BubbleSort, Selection Sort, Shellsort and Insertion Sort.
2. Runs through powers of ten input size, from $$ n=10^2 $$ to $$ n=10^6 $$.
3. At each power of ten input, three data sets are used: Random values, Increasing values (already sorted) and Decreasing values.

### My test

For the algorithms, I largely stuck to examples in the class textbook, *Introduction to the Design & Analysis of Algorithms* by Anany Levitin. Shellsort was described briefly in the textbook, but I found [pesudocode in Wikipedia](https://en.wikipedia.org/wiki/Shellsort#Pseudocode) and translated it to C++. The book described a step sequence for Shellsort, [ 1, 4, 13, 40, 121, ... ] so I used that in reverse, and expanded the sequence to accompany the test's largest dataset.

My versions of the four algorithms ended up like so:

``` c++
int * bubbleSort(int * A, int size) {
  for (int i = 0; i < size - 1; i++) {
    for (int j = 0; j < size - 1 - i; j++) {
      if (A[j + 1] < A[j]) {
        // swap
        int temp = A[j];
        A[j] = A[j + 1];
        A[j + 1] = temp;
      }
    }
  }
  return A;
}

int * selectionSort(int * A, int size) {
  for (int i = 0; i < size - 1; i++) {
    int min = i;
    for (int j = i + 1; j < size; j++) {
      if (A[j] < A[min]) {
        min = j;
      }
    }
    // swap
    int temp = A[i];
    A[i] = A[min];
    A[min] = temp;
  }
  return A;
}

int * insertionSort(int * A, int size) {
  for (int i = 1; i < size; i++) {
    int v = A[i];
    int j = i - 1;
    while (j >= 0 && A[j] > v) {
      A[j + 1] = A[j];
      j--;
    }
    A[j + 1] = v;
  }
  return A;
}

int * shellSort(int * A, int size) {
  int g = 0;
  int gaps[14] = { 2391484, 797161, 265720, 88573, 29524, 9841, 3280, 1093, 364, 121, 40, 13, 4, 1 };

  // check each gap, and find the first one relevant to current input size
  while (gaps[g] > size) {
    g++;
  }

  while ( g < 14 ) {
    // store current gap
    int gap = gaps[g];
    int i,j;
    // do sort with gap
    for ( i = gap; i < size; i ++) {
      int temp = A[i];
      for ( j = i; j >= gap && A[j - gap] > temp; j -= gap ) {
        A[j] = A[j - gap];
      }
      A[j] = temp;
    }
    g++;
  }
  return A;
}
```

### Results

Here are the results after running overnight (time in seconds, bold to emphasize badness!):

#### Random array

| Algorithm | 10^2 |   10^3 |   10^4 |   10^5 |   10^6 |
|---
|BubbleSort | 0.000 |  0.004 |  0.205 |  24.718 | **2513.573** |
|Selection Sort | 0.000 |  0.001 |  0.108 |  10.600 | **1063.195** |
|Shellsort | 0.000 |  0.000 |  0.000 |  0.003  | 0.040 |
|Insertion Sort | 0.000 |  0.000 |  0.000 |  0.000  | 0.003 |

#### Increasing array of values

| Algorithm | 10^2 |   10^3 |   10^4 |   10^5 |   10^6 |
|---
|BubbleSort | 0.000 |  0.002 |  0.100 |  9.910  | **1021.893** |
|Selection Sort | 0.000 |  0.001 |  0.111 |  10.598 | **1064.246** |
|Shellsort | 0.000 |  0.000 |  0.000 |  0.003  | 0.040 |
|Insertion Sort | 0.000 |  0.000 |  0.000 |  0.000  | 0.005 |

#### Decreasing array of values

| Algorithm | 10^2 |   10^3 |   10^4 |   10^5 |   10^6 |
|---
|BubbleSort | 0.000 |  0.002 |  0.099 |  9.895  | **1011.393** |
|Selection Sort | 0.000 |  0.001 |  0.110 |  10.609 | **1062.482** |
|Shellsort | 0.000 |  0.000 |  0.000 |  0.003  | 0.041 |
|Insertion Sort | 0.000 |  0.000 |  0.000 |  0.000  | 0.004 |

With the input size of $$ n=10^6 $$ the differences between algorithms becomes dramatic, taking BubbleSort and Selection Sort 15-30 minutes what Shell Sort and Insertion Sort can do in a tenth of a second.

A curious result keeps happening, regardless of input size, Insertion Sort always goes faster than Shellsort in my tests. This *seems* counter to [conventional wisdom](http://bigocheatsheet.com/) but perhaps C++ compiled code makes certain optimizations that improve how Insertion Sort works, or maybe the data sets I'm using give it certain advantages. In the future, I may look into different gap sequences for Shellsort, and see if by using the book's primary sequence, I actually chose a less efficient option.

### TL;DR

Don't use BubbleSort or Selection Sort. Why? There are other ways to sort with the same amount of code that will run exponentially faster.
