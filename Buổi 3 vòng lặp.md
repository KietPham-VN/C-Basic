---
tags:
  - C
  - Loop
---


# Bài Giảng: Vòng Lặp Trong Lập Trình C

## 1. Tổng Quan Về Vòng Lặp

### 1.1 Vòng lặp là gì?

Vòng lặp (Loop) là cấu trúc điều khiển cho phép thực hiện một khối lệnh nhiều lần cho đến khi thỏa mãn điều kiện dừng. Trong C, có 3 loại vòng lặp chính:

- `for` loop
- `while` loop
- `do-while` loop

### 1.2 Tại sao cần vòng lặp?

- Giảm thiểu việc viết code lặp lại
- Xử lý dữ liệu lớn hiệu quả
- Tạo ra các chương trình linh hoạt và mạnh mẽ

---

## 2. Vòng Lặp FOR

### 2.1 Cú pháp

```c
for (khởi_tạo; điều_kiện; cập_nhật) {
    // Khối lệnh thực thiểu

	//fsadf
}
```

### 2.2 Cách hoạt động

1. **Khởi tạo**: Thực hiện 1 lần duy nhất khi bắt đầu vòng lặp
2. **Kiểm tra điều kiện**: Nếu đúng thì thực hiện khối lệnh, sai thì thoát
3. **Thực thi khối lệnh**
4. **Cập nhật**: Thay đổi biến điều khiển
5. **Lặp lại từ bước 2**

### 2.3 Ví dụ cơ bản

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    // In số từ 1 đến 10
    for (int i = 1; i <= 10; i++) {
        printf("%d ", i);
    }
    printf("\n");
    return 0;
}
```

### 2.4 Ví dụ nâng cao

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    // Tính tổng các số từ 1 đến n
    int n, sum = 0;
    printf("Nhập n: ");
    scanf("%d", &n);
    
    for (int i = 1; i <= n; i++) {
        sum += i;
    }

    printf("Tổng từ 1 đến %d là: %d\n", n, sum);
    return 0;
}
```

### 2.5 Biến thể của vòng for

#### 2.5.1 For với nhiều biến

```c
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i = %d, j = %d\n", i, j);
}
```

#### 2.5.2 For vô hạn

```c
for (;;) {
    // Vòng lặp vô hạn
    printf("Nhấn Ctrl+C để dừng\n");
}
```

#### 2.5.3 For với bước nhảy

```c
// In các số chẵn từ 0 đến 20
for (int i = 0; i <= 20; i += 2) {
    printf("%d ", i);
}
```

---

## 3. Vòng Lặp WHILE

### 3.1 Cú pháp

```c
while (điều_kiện) {
    // Khối lệnh thực thi
}
```

### 3.2 Cách hoạt động

1. **Kiểm tra điều kiện**: Nếu đúng thì thực hiện khối lệnh, sai thì thoát
2. **Thực thi khối lệnh**
3. **Lặp lại từ bước 1**

### 3.3 Ví dụ cơ bản

```c
#include <stdio.h>

int main() {
    int i = 1;

    // In số từ 1 đến 5
    while (i <= 5) {
        printf("%d ", i);
        i++; // Quan trọng: phải cập nhật biến điều khiển
    }
    printf("\n");
    return 0;
}
```

### 3.4 Ví dụ thực tế - Nhập số đến khi hợp lệ

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int number;

    printf("Nhập một số dương: ");
    scanf("%d", &number);

    while (number <= 0) {
        printf("Số không hợp lệ! Nhập lại: ");
        scanf("%d", &number);
    }

    printf("Bạn đã nhập: %d\n", number);
    return 0;
}
```

### 3.5 Khi nào sử dụng while

- Không biết trước số lần lặp
- Điều kiện phức tạp
- Xử lý input từ người dùng

---

## 4. Vòng Lặp DO-WHILE

### 4.1 Cú pháp

```c
do {
    // Khối lệnh thực thi
} while (điều_kiện);
```

### 4.2 Đặc điểm

- **Thực hiện ít nhất 1 lần** (khác với while)
- Kiểm tra điều kiện sau khi thực thi khối lệnh

### 4.3 Ví dụ

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int choice;

    do {
        printf("\n=== MENU ===\n");
        printf("1. Option 1\n");
        printf("2. Option 2\n");
        printf("0. Exit\n");
        printf("Lựa chọn: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                printf("Bạn chọn Option 1\n");
                break;
            case 2:
                printf("Bạn chọn Option 2\n");
                break;
            case 0:
                printf("Tạm biệt!\n");
                break;
            default:
                printf("Lựa chọn không hợp lệ!\n");
        }
    } while (choice != 0);

    return 0;
}
```

### 4.4 Khi nào sử dụng do-while

- Menu chương trình
- Validation input (phải thực hiện ít nhất 1 lần)
- Game loop

---

## 5. So Sánh Các Loại Vòng Lặp

| Đặc điểm                  | for             | while                 | do-while                     |
| ------------------------- | --------------- | --------------------- | ---------------------------- |
| Số lần thực thi tối thiểu | 0               | 0                     | 1                            |
| Kiểm tra điều kiện        | Đầu vòng lặp    | Đầu vòng lặp          | Cuối vòng lặp                |
| Phù hợp khi               | Biết số lần lặp | Không biết số lần lặp | Phải thực hiện ít nhất 1 lần |
| Khởi tạo biến             | Trong cú pháp   | Bên ngoài             | Bên ngoài                    |


> Câu hỏi trong đề thi FE


---

## 6. Lệnh Điều Khiển Vòng Lặp

### 6.1 BREAK - Thoát vòng lặp ngay lập tức

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    for (int i = 1; i <= 10; i++) {
        if (i == 5) {
            break; // Thoát vòng lặp khi i = 5
        }
        printf("%d ", i);
    }
    printf("\nVòng lặp kết thúc\n");
    return 0;
}
// Output: 1 2 3 4
```

### 6.2 CONTINUE - Bỏ qua lần lặp hiện tại

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue; // Bỏ qua số chẵn
        }
        printf("%d ", i);
    }
    printf("\n");
    return 0;
}
// Output: 1 3 5 7 9
```

---

## 7. Vòng Lặp Lồng Nhau (Nested Loops)

### 7.1Ví dụ - In bảng cửu chương

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    printf("BẢNG CỬU CHƯƠNG\n");
    printf("================\n");

    for (int i = 1; i <= 9; i++) {
        printf("Bảng %d:\n", i);
        for (int j = 1; j <= 10; j++) {
            printf("%d x %d = %d\n", i, j, i * j);
        }
        printf("\n");
    }
    return 0;
}
```

### 7.2 Ví dụ - Vẽ hình tam giác

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;
    printf("Nhập chiều cao tam giác: ");
    scanf("%d", &n);

    for (int i = 1; i <= n; i++) {
        // In khoảng trắng
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        // In dấu *
        for (int k = 1; k <= 2 * i - 1; k++) {
            printf("*");
        }
        printf("\n");
    }
    return 0;
}
```

---

## 8. Các Lỗi Thường Gặp Và Cách Khắc Phục

### 8.1 Lỗi 1: Vòng lặp vô hạn

```c
// SAI
int i = 1;
while (i <= 10) {
    printf("%d ", i);
    // Quên cập nhật i
}

// ĐÚNG
int i = 1;
while (i <= 10) {
    printf("%d ", i);
    i++; // Nhớ cập nhật biến điều khiển
}
```

### 8.2 Lỗi 2: Off-by-one error

```c
// SAI - chỉ in 9 số
for (int i = 1; i < 10; i++) {
    printf("%d ", i);
}

// ĐÚNG - in đủ 10 số
for (int i = 1; i <= 10; i++) {
    printf("%d ", i);
}
```

### 8.3 Lỗi 3: Sử dụng = thay vì ==

```c
// SAI
for (int i = 1; i = 10; i++) { // Gán thay vì so sánh
    printf("%d ", i);
}

// ĐÚNG
for (int i = 1; i <= 10; i++) {
    printf("%d ", i);
}
```

---

## 9. Bài Tập Thực Hành

### 9.1 Bài tập cơ bản

#### 9.1.1 Bài 1: Tính giai thừa

**Đề bài:** Viết chương trình tính n! (n factorial)
Ví dụ: 5! = 5 × 4 × 3 × 2 × 1 = 120

**Lời giải:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;
    long long factorial = 1;

    printf("Nhập n: ");
    scanf("%d", &n);

    // Kiểm tra input hợp lệ
    if (n < 0) {
        printf("Giai thừa không xác định với số âm!\n");
        return 1;
    }

    // Tính giai thừa bằng for loop
    for (int i = 1; i <= n; i++) {
        factorial *= i;
    }

    printf("%d! = %lld\n", n, factorial);

    return 0;
}
```

**Cách giải khác với while:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, i = 1;
    long long factorial = 1;

    printf("Nhập n: ");
    scanf("%d", &n);

    if (n < 0) {
        printf("Giai thừa không xác định với số âm!\n");
        return 1;
    }

    // Tính giai thừa bằng while loop
    while (i <= n) {
        factorial *= i;
        i++;
    }

    printf("%d! = %lld\n", n, factorial);
    return 0;
}
```

#### 9.1.2 Bài 2: Kiểm tra số nguyên tố

**Đề bài:** Viết chương trình kiểm tra một số có phải số nguyên tố không
Số nguyên tố là số chỉ chia hết cho 1 và chính nó

**Lời giải:**

```c
#include <stdio.h>
#include <math.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, isPrime = 1;

    printf("Nhập số cần kiểm tra: ");
    scanf("%d", &n);

    // Số <= 1 không phải số nguyên tố
    if (n <= 1) {
        isPrime = 0;
    } else {
        // Kiểm tra từ 2 đến căn bậc 2 của n
        for (int i = 2; i <= sqrt(n); i++) {
            if (n % i == 0) {
                isPrime = 0;
                break; // Thoát sớm khi tìm thấy ước số
            }
        }
    }

    if (isPrime) {
        printf("%d là số nguyên tố\n", n);
    } else {
        printf("%d không phải là số nguyên tố\n", n);
    }

    return 0;
}
```

**Cách tối ưu hơn:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, isPrime = 1;

    printf("Nhập số cần kiểm tra: ");
    scanf("%d", &n);

    if (n <= 1) {
        isPrime = 0;
    } else if (n == 2) {
        isPrime = 1; // 2 là số nguyên tố chẵn duy nhất
    } else if (n % 2 == 0) {
        isPrime = 0; // Các số chẵn khác không phải nguyên tố
    } else {
        // Chỉ kiểm tra các số lẻ từ 3 đến sqrt(n)
        for (int i = 3; i * i <= n; i += 2) {
            if (n % i == 0) {
                isPrime = 0;
                break;
            }
        }
    }

    if (isPrime) {
        printf("%d là số nguyên tố\n", n);
    } else {
        printf("%d không phải là số nguyên tố\n", n);
    }

    return 0;
}
```

#### 9.1.3 Bài 3: Tìm số lớn nhất

**Đề bài:** Nhập n số và tìm số lớn nhất trong n số đó

**Lời giải:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, number, max;

    printf("Nhập số lượng số: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Số lượng không hợp lệ!\n");
        return 1;
    }

    // Nhập số đầu tiên làm max ban đầu
    printf("Nhập số thứ 1: ");
    scanf("%d", &max);

    // Nhập và so sánh các số còn lại
    for (int i = 2; i <= n; i++) {
        printf("Nhập số thứ %d: ", i);
        scanf("%d", &number);

        if (number > max) {
            max = number;
        }
    }

    printf("Số lớn nhất là: %d\n", max);
    return 0;
}
```

**Cách khác - lưu tất cả số vào mảng:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, numbers[100]; // Giả sử tối đa 100 số

    printf("Nhập số lượng số (tối đa 100): ");
    scanf("%d", &n);

    if (n <= 0 || n > 100) {
        printf("Số lượng không hợp lệ!\n");
        return 1;
    }

    // Nhập các số
    for (int i = 0; i < n; i++) {
        printf("Nhập số thứ %d: ", i + 1);
        scanf("%d", &numbers[i]);
    }

    // Tìm số lớn nhất
    int max = numbers[0];
    for (int i = 1; i < n; i++) {
        if (numbers[i] > max) {
            max = numbers[i];
        }
    }

    printf("Số lớn nhất là: %d\n", max);
    return 0;
}
```

### 9.2 Bài tập nâng cao

#### 9.2.1 Bài 4: Dãy Fibonacci

**Đề bài:** In ra n số đầu tiên của dãy Fibonacci
Dãy Fibonacci: 0, 1, 1, 2, 3, 5, 8, 13, 21, ...

**Lời giải:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;
    long long first = 0, second = 1, next;

    printf("Nhập số lượng số Fibonacci: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Số lượng không hợp lệ!\n");
        return 1;
    }

    printf("Dãy Fibonacci gồm %d số đầu tiên:\n", n);

    if (n >= 1) {
        printf("%lld ", first);
    }
    if (n >= 2) {
        printf("%lld ", second);
    }

    // Tính và in các số tiếp theo
    for (int i = 3; i <= n; i++) {
        next = first + second;
        printf("%lld ", next);

        // Cập nhật cho lần lặp tiếp theo
        first = second;
        second = next;
    }

    printf("\n");
    return 0;
}
```

**Cách khác với while:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n, count = 1;
    long long first = 0, second = 1, next;

    printf("Nhập số lượng số Fibonacci: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Số lượng không hợp lệ!\n");
        return 1;
    }

    printf("Dãy Fibonacci: ");

    while (count <= n) {
        if (count == 1) {
            printf("%lld ", first);
        } else if (count == 2) {
            printf("%lld ", second);
        } else {
            next = first + second;
            printf("%lld ", next);
            first = second;
            second = next;
        }
        count++;
    }

    printf("\n");
    return 0;
}
```

#### 9.2.2 Bài 5: Đảo ngược số

**Đề bài:** Viết chương trình đảo ngược một số
Ví dụ: 12345 → 54321

**Lời giải:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int number, reversed = 0, digit;

    printf("Nhập số cần đảo ngược: ");
    scanf("%d", &number);

    // Lưu số gốc để in kết quả
    int original = number;

    // Xử lý số âm
    int isNegative = 0;
    if (number < 0) {
        isNegative = 1;
        number = -number; // Chuyển thành số dương để xử lý
    }

    // Đảo ngược số
    while (number > 0) {
        digit = number % 10;      // Lấy chữ số cuối
        reversed = reversed * 10 + digit; // Thêm vào số đảo ngược
        number /= 10;             // Bỏ chữ số cuối
    }

    // Khôi phục dấu âm nếu cần
    if (isNegative) {
        reversed = -reversed;
    }

    printf("Số ban đầu: %d\n", original);
    printf("Số đảo ngược: %d\n", reversed);

    return 0;
}
```

**Cách khác với for (khi biết số chữ số):**

```c
#include <stdio.h>
#include <math.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int number, reversed = 0, temp;

    printf("Nhập số cần đảo ngược: ");
    scanf("%d", &number);

    int original = number;
    int isNegative = number < 0 ? 1 : 0;
    number = abs(number);
    temp = number;

    // Đếm số chữ số
    int digits = 0;
    if (number == 0) digits = 1;
    else {
        while (temp > 0) {
            digits++;
            temp /= 10;
        }
    }

    // Đảo ngược
    for (int i = 0; i < digits; i++) {
        int digit = number % 10;
        reversed = reversed * 10 + digit;
        number /= 10;
    }

    if (isNegative) reversed = -reversed;

    printf("Số ban đầu: %d\n", original);
    printf("Số đảo ngược: %d\n", reversed);

    return 0;
}
```

#### 9.2.3 Bài 6: Vẽ kim cương

**Đề bài:** Vẽ hình kim cương bằng dấu \* với chiều cao n

```bash
Ví dụ với n = 5:
   *
  ***
 *****
  ***
   *
```

**Lời giải:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;

    printf("Nhập chiều cao kim cương (số lẻ): ");
    scanf("%d", &n);

    // Đảm bảo n là số lẻ
    if (n % 2 == 0) {
        n++; // Tăng lên 1 để thành số lẻ
        printf("Đã điều chỉnh thành %d (số lẻ)\n", n);
    }

    int mid = n / 2; // Vị trí giữa

    // Vẽ nửa trên (bao gồm hàng giữa)
    for (int i = 0; i <= mid; i++) {
        // In khoảng trắng
        for (int j = 0; j < mid - i; j++) {
            printf(" ");
        }
        // In dấu *
        for (int k = 0; k < 2 * i + 1; k++) {
            printf("*");
        }
        printf("\n");
    }

    // Vẽ nửa dưới
    for (int i = mid - 1; i >= 0; i--) {
        // In khoảng trắng
        for (int j = 0; j < mid - i; j++) {
            printf(" ");
        }
        // In dấu *
        for (int k = 0; k < 2 * i + 1; k++) {
            printf("*");
        }
        printf("\n");
    }

    return 0;
}
```

**Cách khác - dùng một vòng lặp:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;

    printf("Nhập chiều cao kim cương: ");
    scanf("%d", &n);

    if (n % 2 == 0) {
        n++;
        printf("Đã điều chỉnh thành %d\n", n);
    }

    int mid = n / 2;

    for (int i = 0; i < n; i++) {
        int spaces, stars;

        if (i <= mid) {
            // Nửa trên
            spaces = mid - i;
            stars = 2 * i + 1;
        } else {
            // Nửa dưới
            spaces = i - mid;
            stars = 2 * (n - i - 1) + 1;
        }

        // In khoảng trắng
        for (int j = 0; j < spaces; j++) {
            printf(" ");
        }

        // In dấu *
        for (int k = 0; k < stars; k++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

**Bonus - Kim cương rỗng:**

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int n;

    printf("Nhập chiều cao kim cương rỗng: ");
    scanf("%d", &n);

    if (n % 2 == 0) n++;

    int mid = n / 2;

    for (int i = 0; i < n; i++) {
        int spaces, stars;

        if (i <= mid) {
            spaces = mid - i;
            stars = 2 * i + 1;
        } else {
            spaces = i - mid;
            stars = 2 * (n - i - 1) + 1;
        }

        // In khoảng trắng đầu
        for (int j = 0; j < spaces; j++) {
            printf(" ");
        }

        // In kim cương rỗng
        if (stars == 1) {
            printf("*"); // Đỉnh và đáy
        } else {
            printf("*"); // Cạnh trái
            for (int k = 1; k < stars - 1; k++) {
                printf(" "); // Khoảng trống giữa
            }
            printf("*"); // Cạnh phải
        }

        printf("\n");
    }

    return 0;
}
```

---

## 10. Lời Khuyên Và Best Practices

### 10.1 Nguyên tắc viết vòng lặp tốt

1. **Luôn đảm bảo điều kiện dừng**: Tránh vòng lặp vô hạn
2. **Khởi tạo biến đúng cách**: Đặt giá trị ban đầu phù hợp
3. **Cập nhật biến điều khiển**: Đừng quên thay đổi biến trong vòng lặp
4. **Chọn loại vòng lặp phù hợp**:
   - `for`: khi biết số lần lặp
   - `while`: khi không biết số lần lặp
   - `do-while`: khi phải thực hiện ít nhất 1 lần

### 10.2 Tối ưu hóa hiệu suất

- Tránh tính toán không cần thiết trong vòng lặp
- Sử dụng prefix increment (++i) thay vì postfix (i++)
- Thoát sớm với break khi có thể

### 10.3 Coding style

- Indentation rõ ràng cho vòng lặp lồng nhau
- Đặt tên biến có ý nghĩa
- Comment giải thích logic phức tạp

---

## 11. Tóm tắt

Vòng lặp là công cụ mạnh mẽ trong lập trình C, giúp:

- Giảm thiểu code trùng lặp
- Xử lý dữ liệu hiệu quả
- Tạo ra các chương trình linh hoạt

**Ghi nhớ:**

- `for`: Biết trước số lần lặp
- `while`: Kiểm tra điều kiện trước khi thực thi
- `do-while`: Thực thi trước, kiểm tra sau
- `break`: Thoát vòng lặp
- `continue`: Bỏ qua lần lặp hiện tại

**Luyện tập thường xuyên** là chìa khóa để thành thạo vòng lặp!
