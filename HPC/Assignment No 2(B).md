# Experiment 2(B): Parallel Merge Sort using OpenMP

## Title

Write a program to implement Parallel Merge Sort using OpenMP.

---

# Aim

To implement Merge Sort using parallel programming.

---

# Theory

## What is Merge Sort?

Merge Sort uses Divide and Conquer approach.

Steps:

1. Divide array into halves.
2. Sort both halves.
3. Merge sorted arrays.

---

## Time Complexity

genui{"math_block_widget_always_prefetch_v2":{"content":"O(n\log n)"}}

---

## Advantages

1. Efficient for large datasets
2. Stable sorting algorithm
3. Suitable for parallel processing

---

# Code

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

// Merge function
void merge(int arr[], int l, int m, int r)
{
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    // Copy data to temporary arrays
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];

    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;

    // Merge the temp arrays back
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements of L[]
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy remaining elements of R[]
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Parallel Merge Sort
void mergeSort(int arr[], int l, int r)
{
    if (l < r)
    {
        int m = (l + r) / 2;

        #pragma omp parallel sections
        {
            #pragma omp section
            {
                mergeSort(arr, l, m);
            }

            #pragma omp section
            {
                mergeSort(arr, m + 1, r);
            }
        }

        merge(arr, l, m, r);
    }
}

int main()
{
    int arr[] = {12, 11, 14, 13, 5, 6, 9, 7};
    int n = 8;

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array: ";

    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

---

# Output

```text
Sorted Array: 5 6 7 11 12 13
```

