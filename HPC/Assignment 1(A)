# High Performance Computing (HPC) Practicals – Complete Notes, Theory and Codes

## Experiment 1(A): Parallel Breadth First Search (BFS) using OpenMP

### Title

Design and implement Parallel Breadth First Search based on existing algorithms using OpenMP. Use a Tree or an undirected graph for BFS.

---

# Aim

To implement Breadth First Search (BFS) traversal in parallel using OpenMP and understand graph traversal using parallel computing.

---

# Objective

1. To understand Breadth First Search traversal.
2. To understand the concept of graph traversal.
3. To learn parallel programming using OpenMP.
4. To compare sequential and parallel execution.
5. To improve traversal performance using multithreading.

---

# Theory

## What is BFS?

Breadth First Search (BFS) is a graph traversal algorithm that visits all neighboring nodes first before moving to the next level.

BFS uses a Queue data structure.

The algorithm starts from a source node and explores:

* first all adjacent vertices,
* then vertices at next level,
* and continues until all nodes are visited.

---

## Applications of BFS

1. Shortest path finding
2. Social network analysis
3. Web crawling
4. GPS navigation systems
5. Broadcasting in networks
6. AI search problems

---

## What is OpenMP?

OpenMP (Open Multi-Processing) is an API used for parallel programming in:

* C
* C++
* Fortran

It allows execution of code using multiple CPU threads.

OpenMP works on shared memory architecture.

---

## Important OpenMP Directives

### Parallel Region

```cpp
#pragma omp parallel
```

Creates multiple threads.

### Parallel For Loop

```cpp
#pragma omp parallel for
```

Divides loop iterations among threads.

---

## How Parallel BFS Works

In Parallel BFS:

* multiple threads process neighboring nodes simultaneously.
* nodes at same level can be explored in parallel.

Advantages:

* Faster execution
* Better CPU utilization
* Efficient for large graphs

Limitations:

* Synchronization overhead
* Race conditions may occur

---

# Algorithm

1. Create graph.
2. Initialize visited array.
3. Push source node into queue.
4. Mark source as visited.
5. While queue is not empty:

   * Remove front node.
   * Print node.
   * Visit all unvisited neighbors.
   * Add neighbors into queue.
6. Use OpenMP for parallel traversal.

---

# Code (C++ with OpenMP)

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <omp.h>

using namespace std;

class Graph {
    int vertices;
    vector<vector<int>> adj;

public:
    Graph(int v) {
        vertices = v;
        adj.resize(v);
    }

    // Function to add edge
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Parallel BFS function
    void parallelBFS(int start) {

        vector<bool> visited(vertices, false);
        queue<int> q;

        visited[start] = true;
        q.push(start);

        cout << "BFS Traversal: ";

        while (!q.empty()) {

            int node = q.front();
            q.pop();

            cout << node << " ";

            // Parallel processing of neighbors
            #pragma omp parallel for
            for (int i = 0; i < adj[node].size(); i++) {

                int neighbor = adj[node][i];

                if (!visited[neighbor]) {

                    #pragma omp critical
                    {
                        if (!visited[neighbor]) {
                            visited[neighbor] = true;
                            q.push(neighbor);
                        }
                    }
                }
            }
        }
    }
};

int main() {

    Graph g(6);

    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 5);

    g.parallelBFS(0);

    return 0;
}
```

---

# Code Explanation

## Header Files

```cpp
#include <omp.h>
```

Used for OpenMP functions.

---

## Graph Representation

```cpp
vector<vector<int>> adj;
```

Adjacency list representation.

---

## Parallel Section

```cpp
#pragma omp parallel for
```

Processes neighbors using multiple threads.

---

## Critical Section

```cpp
#pragma omp critical
```

Prevents multiple threads from modifying queue simultaneously.

---

# Compilation Command

```bash
g++ -fopenmp bfs.cpp -o bfs
```

---

# Execution Command

```bash
./bfs
```

---

# Sample Output

```text
BFS Traversal: 0 1 2 3 4 5
```

---

# Advantages

1. Faster graph traversal
2. Better processor utilization
3. Efficient for large datasets

---

# Disadvantages

1. Synchronization overhead
2. Complex debugging
3. Requires shared memory system

---

# Viva Questions

1. What is BFS?
2. Why queue is used in BFS?
3. Difference between BFS and DFS?
4. What is OpenMP?
5. What is parallelism?
6. What is thread?
7. What is race condition?
8. Why critical section is used?
9. Applications of BFS?
10. Difference between sequential and parallel BFS?
