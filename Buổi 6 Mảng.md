# Lecture Overview

Target Audience: Students familiar with pointers, functions, if-else, and loops
Duration: 90-120 minutes
Prerequisites: Basic C syntax, pointers, functions, control structures

## Part 1: Introduction to Arrays (15 minutes)

### What is an Array?

- Definition: An array is a collection of elements of the same data type stored
in contiguous memory locations.
- Why do we need arrays?

```c
// Without arrays - managing 5 student scores
int score1 = 85;
int score2 = 90;
int score3 = 78;
int score4 = 92;
int score5 = 88;
// With arrays - much cleaner!
int scores[5] = {85, 90, 78, 92, 88};
```

- Key Characteristics:

  - Fixed size (determined at declaration)
  - Contiguous memory allocation
  - Zero-indexed (first element is at index 0)
  - All elements must be the same type

## Part 2: Array Declaration and Initialization (20 minutes)

- Basic Declaration Syntax

```c
// datatype arrayName[size];
```

- Examples of Declaration:

```c
int numbers[10];        // Array of 10 integers (uninitialized)
float prices[5];        // Array of 5 floats
char name[20];          // Array of 20 characters (string)
```

- Initialization Methods
  - Method 1: Initialize at declaration

  ```c
  int ages[5] = {18, 21, 19, 22, 20};
  ```

  - Method 2: Partial initialization

  ```c
  int values[5] = {1, 2};  // Rest are automatically 0
  // Result: {1, 2, 0, 0, 0}
  ```

  - Method 3: Size inference

  ```c
  int data[] = {10, 20, 30, 40};  // Compiler calculates size = 4
  ```

  - Method 4: Initialize after declaration

  ```c
  int scores[3];
  scores[0] = 95;
  scores[1] = 87;
  scores[2] = 91;
  ```

- ⚠️ Common Mistakes

```c
int arr[5];
// arr = {1, 2, 3, 4, 5};  // ❌ ERROR: Cannot assign entire array after declaration

int wrong[];  // ❌ ERROR: Size must be specified (unless initialized immediately)
```

## Part 3: Accessing Array Elements (15 minutes)

- Index-Based Access

```c
int marks[5] = {88, 92, 76, 85, 90};

printf("First student: %d\n", marks[0]);   // 88
printf("Third student: %d\n", marks[2]);   // 76
printf("Last student: %d\n", marks[4]);    // 90
```

- Index Range: 0 to (size - 1)

```c
int arr[5];  // Valid indices: 0, 1, 2, 3, 4
// arr[5] is OUT OF BOUNDS! ⚠️
```

- Practical Example: Using Loops

```c
int numbers[5] = {10, 20, 30, 40, 50};

// Reading array elements
for (int i = 0; i < 5; i++) {
    printf("Element at index %d: %d\n", i, numbers[i]);
}

// Modifying array elements
for (int i = 0; i < 5; i++) {
    numbers[i] = numbers[i] * 2;  // Double each element
}
```

- Exercise: Find Maximum

```c
int scores[5] = {78, 92, 65, 88, 95};
int max = scores[0];

for (int i = 1; i < 5; i++) {
    if (scores[i] > max) {
        max = scores[i];
    }
}
printf("Highest score: %d\n", max);
```

## Part 4: Arrays and Memory (25 minutes)

- Memory Layout

```c
int arr[5] = {10, 20, 30, 40, 50};
```

**Visual representation in memory:**

```bash
Memory Address:  1000   1004   1008   1012   1016
                 [10]   [20]   [30]   [40]   [50]
Index:            0      1      2      3      4
```

- Note: Each int typically occupies 4 bytes
- Calculating Memory Size

```c
int arr[5];
printf("Size of entire array: %lu bytes\n", sizeof(arr));      // 20 bytes
printf("Size of one element: %lu bytes\n", sizeof(arr[0]));    // 4 bytes
printf("Number of elements: %lu\n", sizeof(arr)/sizeof(arr[0])); // 5
```

- Arrays and Pointers Connection 🔗
- Key Concept: Array name is a pointer to the first element!

```c
int arr[5] = {10, 20, 30, 40, 50};
printf("%p\n", arr);       // Address of first element
printf("%p\n", &arr[0]);   // Same address!

// These are equivalent:
printf("%d\n", arr[0]);    // 10
printf("%d\n", *arr);      // 10 (dereferencing the pointer)

printf("%d\n", arr[2]);    // 30
printf("%d\n", *(arr + 2)); // 30 (pointer arithmetic)
```

- Pointer Arithmetic with Arrays

```c
int data[4] = {100, 200, 300, 400};
int *ptr = data;  // ptr points to first element

printf("%d\n", *ptr);       // 100
printf("%d\n", *(ptr + 1)); // 200
printf("%d\n", *(ptr + 3)); // 400

// Moving the pointer
ptr++;  // Now points to second element
printf("%d\n", *ptr);  // 200
Important Differences
cint arr[5] = {1, 2, 3, 4, 5};
int *ptr = arr;

// Array name is a CONSTANT pointer
// arr++;     // ❌ ERROR: Cannot modify array name

// Regular pointer is modifiable
ptr++;        // ✅ OK: Can move the pointer
```

## Part 5: Passing Arrays to Functions (20 minutes)

- Why Pass Arrays?
- Functions make code reusable and organized. Arrays are commonly passed to
functions for processing.
  - Method 1: Array Notation

  ```c
  void printArray(int arr[], int size) {
      for (int i = 0; i < size; i++) {
          printf("%d ", arr[i]);
      }
      printf("\n");
  }

  int main() {
      int numbers[5] = {1, 2, 3, 4, 5};
      printArray(numbers, 5);
      return 0;
  }
  ```

- Method 2: Pointer Notation

```c
void printArray(int *arr, int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", *(arr + i));
    }
    printf("\n");
}
```

- ⚠️ Critical Concept: Arrays are Passed by Reference!

```c
void modifyArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = arr[i] * 2;  // Modifies the original array!
    }
}

int main() {
    int nums[3] = {1, 2, 3};
    modifyArray(nums, 3);
    // nums is now {2, 4, 6} - changed!
    return 0;
}
```

> Why? The array name is a pointer, so you're passing the address of the first element.
>>Cannot Determine Size Inside Function

```c
void someFunction(int arr[]) {
    int size = sizeof(arr) / sizeof(arr[0]);  // ❌ WRONG!
    // arr is just a pointer here, not the actual array
}
```

- Solution: Always pass the size as a separate parameter!
  - Practical Examples
    - Example 1: Calculate Sum

    ```c
      int sumArray(int arr[], int size) {
          int sum = 0;
          for (int i = 0; i < size; i++) {
              sum += arr[i];
          }
          return sum;
      }
    ```

    - Example 2: Find Element

    ```c
    int findElement(int arr[], int size, int target) {
        for (int i = 0; i < size; i++) {
            if (arr[i] == target) {
                return i;  // Return index if found
            }
        }
        return -1;  // Not found
    }
    ```

    - Example 3: Reverse Array

    ```c
    void reverseArray(int arr[], int size) {
        int start = 0;
        int end = size - 1;

        while (start < end) {
            // Swap elements
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;

            start++;
            end--;
        }
    }
    ```

## Part 6: Multi-Dimensional Arrays (15 minutes)

- 2D Arrays: Arrays of Arrays

```c
int matrix[3][4];  // 3 rows, 4 columns
```

- **Visualization:**

```bash
        Col0  Col1  Col2  Col3
Row 0:  [ ]   [ ]   [ ]   [ ]
Row 1:  [ ]   [ ]   [ ]   [ ]
Row 2:  [ ]   [ ]   [ ]   [ ]
```

- Initialization

```c
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Or in one line
int matrix2[2][3] = {1, 2, 3, 4, 5, 6};
```

- Accessing Elements

```c
printf("%d\n", matrix[0][0]);  // 1 (first row, first column)
printf("%d\n", matrix[1][2]);  // 6 (second row, third column)
```

- Traversing 2D Arrays: Nested Loops

```c
int grid[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Print all elements
for (int i = 0; i < 3; i++) {           // Rows
    for (int j = 0; j < 3; j++) {       // Columns
        printf("%d ", grid[i][j]);
    }
    printf("\n");
}
```

- Memory Layout
  - 2D arrays are stored in row-major order in memory:

  ```c
  int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
  // Memory: [1][2][3][4][5][6]
  ```

  - Passing 2D Arrays to Functions

  ```c
  // Column size MUST be specified!
  void print2DArray(int arr[][3], int rows) {
      for (int i = 0; i < rows; i++) {
          for (int j = 0; j < 3; j++) {
              printf("%d ", arr[i][j]);
          }
          printf("\n");
      }
  }

  int main() {
      int matrix[2][3] = {{1, 2, 3}, {4, 5, 6}};
      print2DArray(matrix, 2);
      return 0;
  }


Part 7: Common Pitfalls and Best Practices (10 minutes)

- ⚠️ Common Mistakes
  - **1.** Array Index Out of Bounds

  ```c
  int arr[5] = {1, 2, 3, 4, 5};
  printf("%d\n", arr[5]);  // ❌ Undefined behavior!
  // Valid indices: 0-4 only
  ```

  - **2.** Not Initializing Arrays

  ```c
  int arr[5];
  printf("%d\n", arr[0]);  // ❌ Garbage value!
  ```

  - **3.** Forgetting Array Size in Functions

  ```c
  void process(int arr[]) {
      // Cannot determine size here!
      // Always pass size as parameter
  }
  ```

  - **4.** Trying to Return Arrays Directly

  ```c
  int[] createArray() {  // ❌ ERROR!
      int arr[5] = {1, 2, 3, 4, 5};
      return arr;  // ❌ Returns local address
  }
  ```

- ✅ Best Practices

  - Always initialize arrays

  ```c
  int arr[5] = {0};  // All elements = 0
  ```

  - Use constants for sizes

  ```c
  #define SIZE 10
  int arr[SIZE];

  // Or:
  const int SIZE = 10;
  ```

  - Check bounds when necessary

  ```c
  int index;
  scanf("%d", &index);
  if (index >= 0 && index < SIZE) {
      printf("%d\n", arr[index]);
  }
  ```

  - Pass size to functions

  ```c
  void process(int arr[], int size) {
      // Now you know the size!
  }
  ```

## Part 8: Hands-On Exercises (10-15 minutes)

- Exercise 1: Basic Operations
  - Write a program that:
    - Creates an array of 5 integers
    - Takes input from user
    - Finds and prints the sum and average

- Exercise 2: Search and Replace
  - Write a function that:
    - Takes an array and two integers (old value, new value)
    - Replaces all occurrences of old value with new value
    - Returns the count of replacements made

- Exercise 3: 2D Array Matrix
  - Create a 3x3 matrix and:
    - Take input from user
    - Calculate the sum of each row
    - Print the results

Summary and Key Takeaways
What we learned:

✅ Arrays store multiple values of the same type
✅ Arrays are zero-indexed (0 to size-1)
✅ Array name is a constant pointer to the first element
✅ Arrays are passed by reference to functions
✅ Always pass array size to functions
✅ 2D arrays use nested loops for traversal
