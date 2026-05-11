# Experiment 1(B): Parallel Depth First Search (DFS) using OpenMP

## Title

Design and implement Parallel Depth First Search based on existing algorithms using OpenMP.

---

# Aim

To implement parallel DFS traversal using OpenMP.

---

# Objective

1. To understand DFS traversal.
2. To learn stack-based graph traversal.
3. To understand recursive graph exploration.
4. To implement parallel traversal using OpenMP.

---

# Theory

## What is DFS?

Depth First Search (DFS) is a graph traversal algorithm that explores one branch completely before backtracking.

DFS uses:

* Stack
  OR
* Recursion

---

## Applications of DFS

1. Cycle detection
2. Path finding
3. Maze solving
4. Topological sorting
5. Network analysis

---

## Working of DFS

1. Start from source node.
2. Mark node visited.
3. Visit adjacent unvisited node.
4. Repeat recursively.
5. Backtrack when no unvisited node remains.

---

# Algorithm

1. Create graph.
2. Mark all nodes unvisited.
3. Start DFS from source.
4. Visit node.
5. Explore neighbors recursively.
6. Use OpenMP sections for parallel calls.

---

# Code

```cpp
#include <iostream>
#include <vector>
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

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    void parallelDFSUtil(int node, vector<bool>& visited) {

        visited[node] = true;

        #pragma omp critical
        cout << node << " ";

        #pragma omp parallel for
        for (int i = 0; i < adj[node].size(); i++) {

            int neighbor = adj[node][i];

            if (!visited[neighbor]) {
                parallelDFSUtil(neighbor, visited);
            }
        }
    }

    void parallelDFS(int start) {

        vector<bool> visited(vertices, false);

        cout << "DFS Traversal: ";
        parallelDFSUtil(start, visited);
    }
};

int main() {

    Graph g(6);

    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 5);

    g.parallelDFS(0);

    return 0;
}
```

---

# Compilation

```bash
g++ -fopenmp dfs.cpp -o dfs
```

---

# Sample Output

```text
DFS Traversal: 0 1 3 4 2 5
```

---

# Viva Questions

1. What is DFS?
2. Difference between recursion and stack?
3. Why recursion is used in DFS?
4. What is backtracking?
5. Difference between BFS and DFS?
6. What is OpenMP?
7. What is critical section?
8. Applications of DFS?
