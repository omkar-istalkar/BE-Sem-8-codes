# Experiment 4(A): CUDA Vector Addition

## Title

Write a CUDA Program for Addition of two large vectors.

---

# Aim

To implement vector addition using CUDA GPU programming.

---

# Objective

1. To understand CUDA programming.
2. To understand GPU parallelism.
3. To perform vector addition on GPU.
4. To compare CPU and GPU execution.

---

# Theory

## What is CUDA?

CUDA (Compute Unified Device Architecture) is NVIDIA's parallel computing platform.

CUDA allows developers to use GPU for general purpose computing.

---

## Why GPU is Faster?

GPU contains:

* thousands of cores
* parallel execution units

CPU contains fewer cores.

Hence GPU performs large computations faster.

---

## Vector Addition

For two vectors:

genui{"math_block_widget_always_prefetch_v2":{"content":"C[i]=A[i]+B[i]"}}

Each thread computes one element.

---

# CUDA Keywords

## **global**

Defines kernel function executed on GPU.

## threadIdx.x

Gives thread number.

## cudaMalloc()

Allocates GPU memory.

## cudaMemcpy()

Copies data between CPU and GPU.

---

# Code

```cpp
#include <iostream>
#include <cuda.h>

using namespace std;

__global__ void vectorAdd(int *A, int *B, int *C, int n) {

    int i = threadIdx.x;

    if (i < n) {
        C[i] = A[i] + B[i];
    }
}

int main() {

    int n = 5;

    int A[] = {1, 2, 3, 4, 5};
    int B[] = {10, 20, 30, 40, 50};
    int C[5];

    int *d_A, *d_B, *d_C;

    // Allocate GPU memory
    cudaMalloc((void**)&d_A, n * sizeof(int));
    cudaMalloc((void**)&d_B, n * sizeof(int));
    cudaMalloc((void**)&d_C, n * sizeof(int));

    // Copy data from CPU to GPU
    cudaMemcpy(d_A, A, n * sizeof(int), cudaMemcpyHostToDevice);
    cudaMemcpy(d_B, B, n * sizeof(int), cudaMemcpyHostToDevice);

    // Launch kernel
    vectorAdd<<<1, n>>>(d_A, d_B, d_C, n);

    // Copy result back to CPU
    cudaMemcpy(C, d_C, n * sizeof(int), cudaMemcpyDeviceToHost);

    cout << "Vector Addition Result:" << endl;

    for (int i = 0; i < n; i++) {
        cout << C[i] << " ";
    }

    // Free GPU memory
    cudaFree(d_A);
    cudaFree(d_B);
    cudaFree(d_C);

    return 0;
}
```

---

# Compilation

```bash
nvcc vector_add.cu -o vector
```

---

# Execution

```bash
./vector
```

---

# Output

```text
Vector Addition Result:
11 22 33 44 55
```

---

# Viva Questions

1. What is CUDA?
2. Difference between CPU and GPU?
3. What is kernel function?
4. What is thread in CUDA?
5. What is cudaMalloc?
6. What is cudaMemcpy?
7. Why GPU programming is faster?
8. Applications of CUDA?
