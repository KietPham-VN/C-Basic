# Buổi 2: Cấu trúc rẽ nhánh

## 1. Khái niệm

Cấu trúc rẽ nhánh trong C cho phép chương trình quyết định thực hiện một đoạn mã khác nhau dựa vào điều kiện.

> Nói vui: giống như đi đến ngã ba đường – tùy biển chỉ dẫn mà rẽ trái hay rẽ phải.

## 2. Syntax

### 2.1 If đơn lẻ (rẽ nhánh đơn)

```c
if (x > 0) {
    printf("x là số dương");
}
```

### 2.2 If-Else (rẽ nhánh hai)

```c
if (x % 2 == 0) {
    printf("x là số chẵn");
} else {
    printf("x là số lẻ");
}
```

### 2.3 Đầy đủ (rẽ nhánh nhiều)

```c
if (score >= 8) {
    printf("Giỏi");
} else if (score >= 5) {
    printf("Trung bình");
} else {
    printf("Yếu");
}
```

## 2.4 If lồng nhau

```c
if (x > 0) {
    if (x % 2 == 0) {
        printf("x là số dương chẵn");
    } else {
        printf("x là số dương lẻ");
    }
}
```

## 3. Toán tử

### 3.1 Toán tử logic

- **`&&` (AND)**: Đúng khi tất cả điều kiện đều đúng.

  | A     | B     | A && B |
  | ----- | ----- | ------ |
  | false | false | false  |
  | false | true  | false  |
  | true  | false | false  |
  | true  | true  | true   |

  Ví dụ: `(a > 0 && b > 0)`

- **`||` (OR)**: Đúng khi ít nhất một điều kiện đúng.

  | A     | B     | A \|\| B |
  | ----- | ----- | -------- |
  | false | false | false    |
  | false | true  | true     |
  | true  | false | true     |
  | true  | true  | true     |

  Ví dụ: `(x == 0 || y == 0)`

- **`!` (NOT)**: Đảo ngược giá trị logic.

  | A     | !A    |
  | ----- | ----- |
  | false | true  |
  | true  | false |

  Ví dụ: `!(x > 0)`

### 3.2 Toán tử so sánh

giá trị giả sử a = 5, b = 3

| Biểu thức | Kết quả |
| --------- | ------- |
| a == b    | false   |
| a != b    | true    |
| a > b     | true    |
| a < b     | false   |
| a >= b    | true    |
| a <= b    | false   |

> Trong C thì chỉ có số `0` là biểu thị cho `false` thôi còn lại là `true` hết

-> trò vui từ cơ chế này

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int a = 5, b = 3;

    if (a - b) {
        printf("a khác b\n");
    } else {
        printf("a bằng b\n");
    }

    return 0;
}
```

## 4. Stwich-Case

```c
#include <stdio.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    int ngay;
    printf("Nhap so ngay (1-7): ");
    scanf("%d", &ngay);

    switch (ngay) {
        case 1: printf("Chu Nhat\n"); break;
        case 2: printf("Thu Hai\n"); break;
        case 3: printf("Thu Ba\n"); break;
        case 4: printf("Thu Tu\n"); break;
        case 5: printf("Thu Nam\n"); break;
        case 6: printf("Thu Sau\n"); break;
        case 7: printf("Thu Bay\n"); break;
        default: printf("Khong hop le.\n");
    }

    return 0;
}
```

**_Lưu ý quan trọng khi dùng switch_**

- Mỗi case phải có `break` để tránh rơi vào case tiếp theo.
- Nếu không có `break`, chương trình sẽ tiếp tục thực hiện các case sau đó cho đến khi gặp `break` hoặc kết thúc switch.
- switch chỉ làm việc với các giá trị nguyên (int, char) hoặc enum, không hỗ trợ kiểu dữ liệu float hay double.

> Mình có thể hiểu là switch-case nó sẽ tiện hơn if-else và nhìn nó sẽ gọn hơn khi 1 biến có nhiều mốc giá trị cần theo dõi

## 5. Ternary Operator

```c
int max = (a > b) ? a : b;
```

## 6. Bài tập

### Bài tập 1: Kiểm tra tam giác là tam giác gì?

```c
#include <stdio.h>
#include <math.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);

    float a, b, c;
    printf("Nhập độ dài 3 cạnh tam giác: ");
    scanf("%f %f %f", &a, &b, &c);

    if (a <= 0 || b <= 0 || c <= 0 ||
        a + b <= c || a + c <= b || b + c <= a) {
        printf("Không phải tam giác.\n");
    } else {
        if (a == b && b == c) {
            printf("Tam giác đều.\n");
        }
        else if (a == b || b == c || a == c) {
            if (a*a + b*b == c*c || a*a + c*c == b*b || b*b + c*c == a*a) {
                printf("Tam giác vuông cân.\n");
            } else {
                printf("Tam giác cân.\n");
            }
        }
        else if (a*a + b*b == c*c || a*a + c*c == b*b || b*b + c*c == a*a) {
            printf("Tam giác vuông.\n");
        }
        else {
            printf("Tam giác thường.\n");
        }
    }

    return 0;
}
```

> Một số thập phân đơn giản như 0.1 có thể không chính xác do cách lưu trữ trong máy tính, nên khi so sánh với số thực, bạn nên dùng một khoảng sai số nhỏ (epsilon) để kiểm tra.

```c
double x = 0.1 + 0.2;
if (x == 0.3)
    printf("Bằng nhau\n");
else
    printf("Không bằng nhau, x = %.17f\n", x);

return 0;
```

```c
#include <stdio.h>
#include <math.h>
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001);
    double x = 0.1 + 0.2;
    double eps = 1e-9;
    if (fabs(x - 0.3) < eps)
        printf("Bằng nhau\n");
    else
        printf("Không bằng nhau, x = %.17f\n", x);

    return 0;
}
```

> Trong bài này thì vẫn có 1 chuyện nếu người dùng nhập sai thì chương trình kết thúc luôn, không có thông báo gì cả. Mình sẽ cải thiện trong các bài sau bằng cách kiểm tra lại dữ liệu nhập vào và thông báo cho người dùng. Ngoài ra mình còn có thể ép nhập người dùng nhập lại nếu nhập sai.
