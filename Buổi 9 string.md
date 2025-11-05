# Strings in C - Comprehensive Lecture

## Table of Contents

1. [Introduction to Strings in C](#introduction)
2. [String Fundamentals](#fundamentals)
3. [String Declaration and Initialization](#declaration)
4. [String Input/Output](#input-output)
5. [Standard String Library Functions](#string-functions)
6. [String Manipulation Techniques](#manipulation)
7. [Common Pitfalls and Best Practices](#pitfalls)
8. [Practice Examples](#examples)

---

## 1. Introduction to Strings in C {#introduction}

### What is a String in C?

In C, a **string** is not a primitive data type like in many modern languages. Instead, a string is represented as:

- An **array of characters** (`char`)
- Terminated by a **null character** (`'\0'`)

This null terminator is crucial—it marks the end of the string and allows functions to determine where the string ends.

### Example

```c
char str[] = "Hello";
// Memory representation: ['H']['e']['l']['l']['o']['\0']
// Array size: 6 (5 characters + 1 null terminator)
```

---

## 2. String Fundamentals {#fundamentals}

### 2.1 Null Terminator (`'\0'`)

The null terminator is a character with ASCII value 0. It's **automatically added** when you initialize a string with double quotes.

```c
char str1[] = "Hello";        // Null terminator added automatically
char str2[] = {'H','e','l','l','o','\0'};  // Manual null terminator
```

**Important:** Without the null terminator, C functions won't know where the string ends, leading to undefined behavior.

### 2.2 String vs Character

```c
char ch = 'A';        // Single character (uses single quotes)
char str[] = "A";     // String with 2 bytes: 'A' and '\0'
```

---

## 3. String Declaration and Initialization {#declaration}

### 3.1 Declaration Methods

**Method 1: Character Array with Size**

```c
char str[50];  // Can hold up to 49 characters + null terminator
```

**Method 2: Initialize with String Literal**

```c
char str[] = "Hello World";  // Size calculated automatically (12 bytes)
```

**Method 3: Explicit Size with Initialization**

```c
char str[20] = "Hello";  // Uses 6 bytes, 14 bytes unused
```

**Method 4: Character-by-Character**

```c
char str[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

### 3.2 String Pointers

Since strings are arrays, you can use pointers:

```c
char *ptr = "Hello World";  // Pointer to string literal (read-only)
```

**Warning:** String literals are stored in read-only memory. Modifying them causes undefined behavior:

```c
char *ptr = "Hello";
ptr[0] = 'h';  // ❌ WRONG - Segmentation fault!

char str[] = "Hello";
str[0] = 'h';  // ✅ CORRECT - Result: "hello"
```

---

## 4. String Input/Output {#input-output}

### 4.1 Output Functions

**`printf()` with `%s`**

```c
char name[] = "Alice";
printf("Name: %s\n", name);
printf("First 3 chars: %.3s\n", name);  // Output: "Ali"
```

**`puts()`**

```c
char str[] = "Hello World";
puts(str);  // Automatically adds newline
```

### 4.2 Input Functions

**`scanf()` - Reads until whitespace**

```c
char name[50];
scanf("%s", name);  // Stops at space/tab/newline
// Input: "John Doe" → Stores only "John"
```

**`scanf()` with width specifier (safer)**

```c
char name[50];
scanf("%49s", name);  // Prevents buffer overflow
```

**`fgets()` - Reads entire line (RECOMMENDED)**

```c
char line[100];
fgets(line, sizeof(line), stdin);
// Reads up to 99 characters or until newline
// Includes newline character in the string
```

**Removing newline from `fgets()`:**

```c
char line[100];
fgets(line, sizeof(line), stdin);
line[strcspn(line, "\n")] = '\0';  // Remove newline
```

**`gets()` - DEPRECATED (Never use)**

```c
gets(str);  // ❌ Extremely dangerous - buffer overflow risk!
```

---

## 5. Standard String Library Functions {#string-functions}

Include the header: `#include <string.h>`

### 5.1 String Length

**`strlen()` - Returns string length (excluding null terminator)**

```c
char str[] = "Hello";
int len = strlen(str);  // len = 5
```

**Important:** `strlen()` counts characters until `'\0'`, not the array size:

```c
char str[100] = "Hi";
strlen(str);   // Returns 2
sizeof(str);   // Returns 100
```

### 5.2 String Copy

**`strcpy()` - Copy entire string**

```c
char src[] = "Hello";
char dest[20];
strcpy(dest, src);  // dest = "Hello"
```

**`strncpy()` - Copy n characters (safer)**

```c
char src[] = "Hello World";
char dest[20];
strncpy(dest, src, 5);
dest[5] = '\0';  // Must add null terminator manually!
// Result: dest = "Hello"
```

**Warning:** `strncpy()` doesn't add `'\0'` if source is longer than n.

### 5.3 String Concatenation

**`strcat()` - Concatenate strings**

```c
char dest[50] = "Hello";
char src[] = " World";
strcat(dest, src);  // dest = "Hello World"
```

**`strncat()` - Concatenate n characters (safer)**

```c
char dest[50] = "Hello";
char src[] = " World";
strncat(dest, src, 3);  // dest = "Hello Wo"
```

### 5.4 String Comparison

**`strcmp()` - Compare two strings**

```c
char str1[] = "Apple";
char str2[] = "Banana";
int result = strcmp(str1, str2);
// result < 0 if str1 < str2
// result = 0 if str1 == str2
// result > 0 if str1 > str2
```

**Common usage:**

```c
if (strcmp(str1, str2) == 0) {
    printf("Strings are equal\n");
}
```

**`strncmp()` - Compare first n characters**

```c
char str1[] = "Hello";
char str2[] = "Help";
int result = strncmp(str1, str2, 3);  // Compares "Hel" with "Hel"
// result = 0 (first 3 characters are equal)
```

**Important:** Never use `==` to compare strings:

```c
if (str1 == str2)  // ❌ WRONG - Compares addresses, not content!
if (strcmp(str1, str2) == 0)  // ✅ CORRECT
```

### 5.5 String Search

**`strchr()` - Find first occurrence of character**

```c
char str[] = "Hello World";
char *ptr = strchr(str, 'o');
if (ptr != NULL) {
    printf("Found at position: %ld\n", ptr - str);  // Position 4
}
```

**`strrchr()` - Find last occurrence of character**

```c
char str[] = "Hello World";
char *ptr = strrchr(str, 'o');  // Points to 'o' in "World"
```

**`strstr()` - Find substring**

```c
char str[] = "Hello World";
char *ptr = strstr(str, "World");
if (ptr != NULL) {
    printf("Substring found: %s\n", ptr);  // Output: "World"
}
```

### 5.6 String Tokenization

**`strtok()` - Split string into tokens**

```c
char str[] = "apple,banana,cherry";
char *token = strtok(str, ",");
while (token != NULL) {
    printf("%s\n", token);
    token = strtok(NULL, ",");
}
// Output:
// apple
// banana
// cherry
```

**Warning:** `strtok()` modifies the original string by replacing delimiters with `'\0'`.

---

## 6. String Manipulation Techniques {#manipulation}

### 6.1 Converting Case

**Manual approach:**

```c
#include <ctype.h>

void toUpperCase(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        str[i] = toupper(str[i]);
    }
}

void toLowerCase(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        str[i] = tolower(str[i]);
    }
}
```

### 6.2 Reversing a String

```c
void reverseString(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - 1 - i];
        str[len - 1 - i] = temp;
    }
}
```

### 6.3 Trimming Whitespace

**Trim leading and trailing spaces:**

```c
void trim(char *str) {
    // Trim leading spaces
    int i = 0;
    while (isspace(str[i])) i++;
    
    if (i > 0) {
        int j = 0;
        while (str[i] != '\0') {
            str[j++] = str[i++];
        }
        str[j] = '\0';
    }
    
    // Trim trailing spaces
    i = strlen(str) - 1;
    while (i >= 0 && isspace(str[i])) {
        str[i] = '\0';
        i--;
    }
}
```

### 6.4 Counting Words

```c
int countWords(char *str) {
    int count = 0;
    int inWord = 0;
    
    for (int i = 0; str[i] != '\0'; i++) {
        if (isspace(str[i])) {
            inWord = 0;
        } else if (inWord == 0) {
            inWord = 1;
            count++;
        }
    }
    return count;
}
```

### 6.5 Checking Palindrome

```c
int isPalindrome(char *str) {
    int left = 0;
    int right = strlen(str) - 1;
    
    while (left < right) {
        if (str[left] != str[right]) {
            return 0;  // Not a palindrome
        }
        left++;
        right--;
    }
    return 1;  // Is a palindrome
}
```

---

## 7. Common Pitfalls and Best Practices {#pitfalls}

### 7.1 Buffer Overflow

**Problem:**

```c
char str[5];
strcpy(str, "Hello World");  // ❌ Buffer overflow!
```

**Solution:**

```c
char str[20];
strncpy(str, "Hello World", sizeof(str) - 1);
str[sizeof(str) - 1] = '\0';  // Ensure null termination
```

### 7.2 Uninitialized Strings

**Problem:**

```c
char str[50];
strcat(str, "Hello");  // ❌ Undefined behavior - str not initialized
```

**Solution:**

```c
char str[50] = "";  // Initialize with empty string
strcat(str, "Hello");  // ✅ Now safe
```

### 7.3 Missing Null Terminator

**Problem:**

```c
char str[5] = {'H', 'e', 'l', 'l', 'o'};
printf("%s", str);  // ❌ No null terminator - undefined behavior
```

**Solution:**

```c
char str[6] = {'H', 'e', 'l', 'l', 'o', '\0'};  // ✅
// or
char str[] = "Hello";  // ✅ Automatic null terminator
```

### 7.4 Modifying String Literals

**Problem:**

```c
char *str = "Hello";
str[0] = 'h';  // ❌ Segmentation fault
```

**Solution:**

```c
char str[] = "Hello";
str[0] = 'h';  // ✅ Works fine
```

### 7.5 Returning Local Arrays

**Problem:**

```c
char* createString() {
    char str[50] = "Hello";
    return str;  // ❌ Returning pointer to local array
}
```

**Solution:** Use array parameter passed by caller:

```c
void createString(char *str, int size) {
    strncpy(str, "Hello", size - 1);
    str[size - 1] = '\0';
}

// Usage:
char str[50];
createString(str, sizeof(str));
```

---

## 8. Practice Examples {#examples}

### Example 1: String Copy Without Library Function

```c
void myStrcpy(char *dest, const char *src) {
    int i = 0;
    while (src[i] != '\0') {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0';
}
```

### Example 2: Count Character Occurrences

```c
int countChar(const char *str, char ch) {
    int count = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == ch) {
            count++;
        }
    }
    return count;
}
```

### Example 3: Remove All Spaces

```c
void removeSpaces(char *str) {
    int i = 0, j = 0;
    while (str[i] != '\0') {
        if (str[i] != ' ') {
            str[j++] = str[i];
        }
        i++;
    }
    str[j] = '\0';
}
```

### Example 4: String Contains Substring

```c
int contains(const char *str, const char *substr) {
    return strstr(str, substr) != NULL;
}
```

### Example 5: Complete Program - String Statistics

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char text[1000];
    int letters = 0, digits = 0, spaces = 0, others = 0;
    
    printf("Enter text: ");
    fgets(text, sizeof(text), stdin);
    
    for (int i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            letters++;
        } else if (isdigit(text[i])) {
            digits++;
        } else if (isspace(text[i])) {
            spaces++;
        } else {
            others++;
        }
    }
    
    printf("\nStatistics:\n");
    printf("Letters: %d\n", letters);
    printf("Digits: %d\n", digits);
    printf("Spaces: %d\n", spaces);
    printf("Others: %d\n", others);
    printf("Total length: %lu\n", strlen(text));
    
    return 0;
}
```

---

## Summary

### Key Takeaways

1. **Strings in C are arrays of characters terminated by `'\0'`**
2. **Always ensure proper null termination**
3. **Prefer safer functions:** `strncpy()`, `strncat()`, `fgets()` over their unsafe counterparts
4. **Use `strcmp()` for string comparison, never `==`**
5. **Watch out for buffer overflows** - always check array bounds
6. **String literals are read-only** - copy to array if modification needed
7. **Include `<string.h>` for standard string functions**
8. **Use `<ctype.h>` for character classification functions**

### Common String Functions Quick Reference

| Function | Purpose | Example |
|----------|---------|---------|
| `strlen()` | Get string length | `len = strlen(str)` |
| `strcpy()` | Copy string | `strcpy(dest, src)` |
| `strncpy()` | Copy n characters | `strncpy(dest, src, n)` |
| `strcat()` | Concatenate strings | `strcat(dest, src)` |
| `strcmp()` | Compare strings | `if (strcmp(s1, s2) == 0)` |
| `strchr()` | Find character | `ptr = strchr(str, 'c')` |
| `strstr()` | Find substring | `ptr = strstr(str, "sub")` |
| `strtok()` | Tokenize string | `token = strtok(str, ",")` |

---

**Practice makes perfect!** Work through the examples and create your own string manipulation programs to master C strings.
