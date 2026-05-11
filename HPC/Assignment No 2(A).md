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

// Regular Bubble Sort Function
void bubbleSort(int arr[], int start, int end)
{
    for(int i = start; i < end; i++)
    {
        for(int j = start; j < end - (i - start); j++)
        {
            if(arr[j] > arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

// Merge Two Sorted Parts
void merge(int arr[], int low, int mid, int high)
{
    int n1 = mid - low + 1;
    int n2 = high - mid;

    int left[n1], right[n2];

    // Copy data
    for(int i = 0; i < n1; i++)
        left[i] = arr[low + i];

    for(int j = 0; j < n2; j++)
        right[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = low;

    // Merge arrays
    while(i < n1 && j < n2)
    {
        if(left[i] <= right[j])
        {
            arr[k] = left[i];
            i++;
        }
        else
        {
            arr[k] = right[j];
            j++;
        }
        k++;
    }

    // Remaining elements
    while(i < n1)
    {
        arr[k] = left[i];
        i++;
        k++;
    }

    while(j < n2)
    {
        arr[k] = right[j];
        j++;
        k++;
    }
}

int main()
{
    int arr[] = {9, 7, 5, 3, 1, 2, 4, 6, 8, 0};

    int n = 10;

    int mid = n / 2;

    // Parallel Region
    #pragma omp parallel sections
    {
        // Thread 1 sorts first half
        #pragma omp section
        {
            bubbleSort(arr, 0, mid - 1);
        }

        // Thread 2 sorts second half
        #pragma omp section
        {
            bubbleSort(arr, mid, n - 1);
        }
    }

    // Merge both sorted halves
    merge(arr, 0, mid - 1, n - 1);

    cout << "Sorted Array:\n";

    for(int i = 0; i < n; i++)
    {
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

