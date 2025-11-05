---
tags:
  - C
  - Array
  - TimeComplexity
  - SpaceComplexity
  - Algorithm
---
# Time & Space Complexity through Arrays

**Target:** Students who know C Arrays | **Duration:** 60-90 minutes

---

## Part 1: Why Complexity Matters (10 min)

### The Problem: Which Search is Better?

**Linear Search** vs **Binary Search** (on sorted array):

|Array Size|Linear|Binary|
|---|---|---|
|100|~100|~7|
|1,000|~1,000|~10|
|1,000,000|~1M|~20|

**We need a systematic way to compare algorithms!**

---

## Part 2: Big O Notation (10 min)

### What is Complexity?

- **Time:** How operations grow with input size
- **Space:** How memory usage grows with input size
- Focus on **worst-case** and **growth rate** (not exact time/memory)

### Common Complexities (fastest → slowest)

```md
O(1)         Constant      - Array access, variable assignment
O(log n)     Logarithmic   - Binary search, tree operations
O(n)         Linear        - Single loop, linear search
O(n log n)   Linearithmic  - Merge sort, quick sort
O(n²)        Quadratic     - Nested loops, bubble sort
O(2ⁿ)        Exponential   - Recursive fibonacci
```

### Growth Comparison

```md
n = 1,000:
O(1)      = 1
O(log n)  = 10
O(n)      = 1,000
O(n log n)= 10,000
O(n²)     = 1,000,000
```

---

## Part 3: O(1) - Constant (5 min)

### **Runtime/space doesn't depend on input size**

```c
int getElement(int arr[], int index) {
    return arr[index];  // Always 1 operation
}
// Time: O(1), Space: O(1)

void swap(int arr[], int i, int j) {
    int temp = arr[i];      // Fixed number of
    arr[i] = arr[j];        // operations regardless
    arr[j] = temp;          // of array size
}
// Time: O(1), Space: O(1) - only 1 temp variable
```

**Key:** Fixed operations, no matter how large the input!

---

## Part 4: O(n) - Linear (10 min)

### **Runtime/space grows linearly with input**

```c
// Print all elements
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {     // n times
        printf("%d ", arr[i]);            // O(1)
    }
}
// Time: O(n), Space: O(1)

// Find sum
int sumArray(int arr[], int size) {
    int sum = 0;                         // O(1) space
    for (int i = 0; i < size; i++) {     // O(n) time
        sum += arr[i];
    }
    return sum;
}
// Time: O(n), Space: O(1)

// Copy array (uses extra space!)
int* copyArray(int arr[], int size) {
    int* copy = malloc(size * sizeof(int));  // O(n) space!
    for (int i = 0; i < size; i++) {
        copy[i] = arr[i];
    }
    return copy;
}
// Time: O(n), Space: O(n) - new array created
```

### Multiple Sequential Loops

```c
void process(int arr[], int size) {
    for (int i = 0; i < size; i++) { }     // O(n)
    for (int i = 0; i < size; i++) { }     // O(n)
    for (int i = 0; i < size; i++) { }     // O(n)
}
// Total: O(n) + O(n) + O(n) = O(3n) = O(n)
// Drop constants!
```

---

## Part 5: O(n²) - Quadratic (10 min)

**Nested loops = multiplication!**

```c
// Print all pairs
void printAllPairs(int arr[], int size) {
    for (int i = 0; i < size; i++) {         // n times
        for (int j = 0; j < size; j++) {     // n times each
            printf("(%d,%d) ", arr[i], arr[j]);
        }
    }
}
// Time: O(n × n) = O(n²), Space: O(1)

// Bubble Sort
void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];           // O(1) space
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
// Time: O(n²), Space: O(1) - sorts in-place!

// Find duplicates (naive)
void findDuplicates(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        for (int j = i + 1; j < size; j++) {
            if (arr[i] == arr[j]) {
                printf("Dup: %d\n", arr[i]);
            }
        }
    }
}
// Time: O(n²), Space: O(1)
```

**Growth:** If n doubles, runtime increases 4x!

---

## Part 6: O(log n) - Logarithmic (10 min)

### **Halves the problem each step**

### Binary Search (sorted array required!)

```c
int binarySearch(int arr[], int size, int target) {
    int left = 0, right = size - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;      // Eliminate left half
        else right = mid - 1;                       // Eliminate right half
    }
    return -1;
}
// Time: O(log n), Space: O(1)
```

**How it works:** Find 7 in `[1, 3, 5, 7, 9, 11, 13, 15]`

```markdown
Step 1: Check mid(9)  → 7 < 9, search left
Step 2: Check mid(3)  → 7 > 3, search right
Step 3: Check mid(7)  → Found! (3 steps for 8 elements)
```

**Why fast?** log₂(1,000,000) ≈ 20 steps!

---

## Part 7: O(n log n) - Linearithmic (10 min)

### **Efficient sorting algorithms**

```c
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);           // Divide
        mergeSort(arr, mid + 1, right);      // Divide
        merge(arr, left, mid, right);        // Conquer - O(n)
    }
}
// Time: O(n log n), Space: O(n) - needs temp arrays

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    int L[n1], R[n2];  // O(n) space for merging!
    // ... merge logic
}
```

### Why O(n log n)?

- **Levels of division:** log n levels (keeps halving)
- **Work per level:** O(n) (merging)
- **Total:** O(n) × O(log n) = O(n log n)

### Sorting Comparison

|Algorithm|Time|Space|Best For|
|---|---|---|---|
|Bubble|O(n²)|O(1)|Small/teaching|
|Selection|O(n²)|O(1)|Small arrays|
|Merge|O(n log n)|O(n)|Large/stable|
|Quick|O(n log n)|O(log n)|Large/in-place|

---

## Part 8: Space-Time Tradeoffs (8 min)

**Often: More space → Faster time!**

### Example: Finding Duplicates

#### **Method 1: O(1) space, O(n²) time**

```c
void findDups1(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        for (int j = i + 1; j < size; j++) {
            if (arr[i] == arr[j])
                printf("Dup: %d\n", arr[i]);
        }
    }
}
// Time: O(n²), Space: O(1)
```

#### **Method 2: O(n) space, O(n) time**

```c
void findDups2(int arr[], int size) {
    int seen[1000] = {0};  // Extra space!

    for (int i = 0; i < size; i++) {
        if (seen[arr[i]])
            printf("Dup: %d\n", arr[i]);
        seen[arr[i]] = 1;
    }
}
// Time: O(n), Space: O(n) - MUCH faster!
```

### Recursive Call Stack

```c
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// Time: O(n), Space: O(n) - call stack depth!
```

**Recursion uses stack space!** Each call adds a frame.

---

## Part 9: Analysis Rules & Examples (10 min)

### Key Rules

1. **Sequential → Add:** `O(n) + O(n) = O(n)`
2. **Nested → Multiply:** `O(n) × O(n) = O(n²)`
3. **Drop constants:** `O(5n) = O(n)`
4. **Keep dominant term:** `O(n² + n) = O(n²)`
5. **Different inputs → Different variables:** `O(n + m)`

### Practice Problems

**Problem A:**

```c
void mysteryA(int arr[], int size) {
    for (int i = 0; i < size; i++) {      // n times
        for (int j = 0; j < 1000; j++) {  // Constant!
            printf("%d ", arr[i]);
        }
    }
}
// Answer: O(n × 1000) = O(n), Space: O(1)
```

**Problem B:**

```c
void mysteryB(int arr[], int size) {
    int i = size;
    while (i > 1) {
        printf("%d\n", arr[i]);
        i = i / 2;  // Dividing by 2!
    }
}
// Answer: O(log n), Space: O(1)
```

**Problem C:**

```c
void mysteryC(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        for (int j = i; j < size; j++) {
            printf("%d %d\n", arr[i], arr[j]);
        }
    }
}
// Answer: n + (n-1) + ... + 1 = n(n+1)/2 = O(n²), Space: O(1)
```

---

## Part 10: Real-World Scenarios (8 min)

### Scenario 1: Auto-complete Search

**Problem:** Find names starting with "Jo" in 10,000 contacts

```c
// Linear: O(n) - check all contacts
void search1(char contacts[][50], int n, char prefix[]) {
    for (int i = 0; i < n; i++) {
        if (startsWith(contacts[i], prefix))
            printf("%s\n", contacts[i]);
    }
}

// Binary: O(log n + k) - k matches found
void search2(char contacts[][50], int n, char prefix[]) {
    int start = binarySearchStart(contacts, n, prefix);
    for (int i = start; startsWith(contacts[i], prefix); i++)
        printf("%s\n", contacts[i]);
}
```

### Scenario 2: Finding Common Elements

```c
// O(n × m) - nested loops
void findCommon1(int arr1[], int n, int arr2[], int m) {
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (arr1[i] == arr2[j])
                printf("%d ", arr1[i]);
}

// O(n log n + m log m) - sort then two pointers
void findCommon2(int arr1[], int n, int arr2[], int m) {
    mergeSort(arr1, 0, n-1);
    mergeSort(arr2, 0, m-1);

    int i = 0, j = 0;
    while (i < n && j < m) {
        if (arr1[i] == arr2[j]) {
            printf("%d ", arr1[i]);
            i++; j++;
        } else if (arr1[i] < arr2[j]) i++;
        else j++;
    }
}
```

---

## Part 11: Summary & Quick Reference (5 min)

### Complexity Cheat Sheet

|Operation|Unsorted|Sorted|
|---|---|---|
|Access[i]|O(1)|O(1)|
|Search|O(n)|O(log n)|
|Insert end|O(1)|O(n)|
|Delete|O(n)|O(n)|
|Find min/max|O(n)|O(1)|

### Decision Guide

```c
Is n < 100?       → O(n²) is fine
Is n < 10,000?    → Use O(n log n)
Is n > 10,000?    → Must use O(n log n) or better
```

### Common Mistakes

❌ Ignoring that loops = O(n), not O(1)
❌ Forgetting worst-case analysis
❌ Confusing time and space complexity
❌ Missing hidden operations (strlen in loop)
❌ Premature optimization on small data

### Key Takeaways

1. **Sequential ops → Add:** O(n) + O(n) = O(n)
2. **Nested ops → Multiply:** O(n) × O(n) = O(n²)
3. **Drop constants & lower terms:** O(3n + 5) = O(n)
4. **More space often → Faster time** (tradeoff)
5. **Always test with realistic sizes!**

---

## Hands-On Lab

**Benchmark duplicate finding algorithms:**

```c
#include <stdio.h>
#include <time.h>

int main() {
    int sizes[] = {100, 1000, 5000};

    for (int s = 0; s < 3; s++) {
        int size = sizes[s];
        // Fill array with random data

        // Time O(n²) version
        clock_t start = clock();
        findDuplicatesSlow(arr, size);
        double time1 = (double)(clock() - start) / CLOCKS_PER_SEC;

        // Time O(n) version
        start = clock();
        findDuplicatesFast(arr, size);
        double time2 = (double)(clock() - start) / CLOCKS_PER_SEC;

        printf("Size %d: Slow=%.4fs, Fast=%.4fs, Speedup=%.1fx\n",
               size, time1, time2, time1/time2);
    }
}
```

**Practice:** Implement both versions and observe the difference!

---

**Remember:** Don't just memorize—understand WHY algorithms have their complexity!
