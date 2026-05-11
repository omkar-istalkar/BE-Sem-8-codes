# Experiment 2(A): Parallel Bubble Sort using OpenMP

## Title

Write a program to implement Parallel Bubble Sort using OpenMP.

---

# Aim

To sort elements using Parallel Bubble Sort and compare performance.

---

# Objective

1. To understand sorting algorithms.
2. To learn Bubble Sort.
3. To implement parallel sorting.
4. To improve sorting speed.

---

# Theory

## What is Bubble Sort?

Bubble Sort repeatedly compares adjacent elements and swaps them if they are in wrong order.

Largest element moves to end after each pass.

---

## Time Complexity

genui{"math_block_widget_always_prefetch_v2":{"content":"O(n^2)"}}

---

## Parallel Bubble Sort

In parallel bubble sort:

* comparisons occur simultaneously.
* multiple threads perform swapping.

This reduces execution time.

---

# Algorithm

1. Take array input.
2. Compare adjacent elements.
3. Swap if needed.
4. Repeat for all passes.
5. Use OpenMP for parallel loops.

---

# Code

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

void bubbleSort(int arr[], int n) {

    for (int i = 0; i < n - 1; i++) {

        #pragma omp parallel for
        for (int j = 0; j < n - i - 1; j++) {

            if (arr[j] > arr[j + 1]) {

                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {

    int arr[] = {5, 1, 4, 2, 8};
    int n = 5;

    bubbleSort(arr, n);

    cout << "Sorted Array: ";

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

---

# Compilation

```bash
g++ -fopenmp bubble.cpp -o bubble
```

---

# Output

```text
Sorted Array: 1 2 4 5 8
```

---

# Viva Questions

1. What is Bubble Sort?
2. Why called Bubble Sort?
3. Time complexity?
4. What is parallel sorting?
5. Advantages of OpenMP?

