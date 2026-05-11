# Experiment 3: Parallel Reduction (Min, Max, Sum, Average)

## Title

Implement Min, Max, Sum and Average operations using Parallel Reduction.

---

# Aim

To perform mathematical operations using parallel reduction.

---

# Theory

## What is Parallel Reduction?

Parallel reduction combines multiple values into a single result using parallel computation.

Examples:

* Sum
* Minimum
* Maximum
* Average

---

## Advantages

1. Faster processing
2. Better CPU utilization
3. Efficient for large arrays

---

# Code

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {

    int arr[5] = {10, 20, 30, 40, 50};

    int sum = 0;
    int minVal = arr[0];
    int maxVal = arr[0];

    #pragma omp parallel for reduction(+:sum)
    for (int i = 0; i < 5; i++) {
        sum += arr[i];
    }

    #pragma omp parallel for reduction(min:minVal)
    for (int i = 0; i < 5; i++) {
        if (arr[i] < minVal)
            minVal = arr[i];
    }

    #pragma omp parallel for reduction(max:maxVal)
    for (int i = 0; i < 5; i++) {
        if (arr[i] > maxVal)
            maxVal = arr[i];
    }

    float avg = (float)sum / 5;

    cout << "Sum = " << sum << endl;
    cout << "Minimum = " << minVal << endl;
    cout << "Maximum = " << maxVal << endl;
    cout << "Average = " << avg << endl;

    return 0;
}
```

---

# Output

```text
Sum = 150
Minimum = 10
Maximum = 50
Average = 30
```

---

# Viva Questions

1. What is reduction?
2. What is reduction clause?
3. Difference between min and max reduction?
4. Applications of reduction?
5. Why OpenMP is useful?
