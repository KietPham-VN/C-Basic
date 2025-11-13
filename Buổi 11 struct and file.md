---
tags:
  - C
  - Struct
  - File-IO
---

# Bài giảng: Struct và File I/O trong C

## Mục lục (Table of Contents)

### Phần 1: Struct (Cấu trúc)

- [1. Struct là gì?](#1-struct-là-gì)
- [2. Khai báo và sử dụng Struct](#2-khai-báo-và-sử-dụng-struct)
- [3. Các cách khởi tạo Struct](#3-các-cách-khởi-tạo-struct)
- [4. Truy cập thành viên của Struct](#4-truy-cập-thành-viên-của-struct)
- [5. Struct lồng nhau (Nested Struct)](#5-struct-lồng-nhau-nested-struct)
- [6. Mảng của Struct](#6-mảng-của-struct)
- [7. Con trỏ và Struct](#7-con-trỏ-và-struct)
- [8. Struct và Function](#8-struct-và-function)
- [9. Typedef với Struct](#9-typedef-với-struct)
- [10. Kích thước của Struct (Size và Padding)](#10-kích-thước-của-struct-size-và-padding)

### Phần 2: File I/O (Input/Output với File)

- [1. Giới thiệu về File I/O](#1-giới-thiệu-về-file-io)
- [2. Con trỏ FILE](#2-con-trỏ-file)
- [3. Mở và đóng file](#3-mở-và-đóng-file)
- [4. Đọc và ghi file ở chế độ Text](#4-đọc-và-ghi-file-ở-chế-độ-text)
- [5. Đọc và ghi file ở chế độ Binary](#5-đọc-và-ghi-file-ở-chế-độ-binary)
- [6. Di chuyển con trỏ file (fseek, ftell, rewind)](#6-di-chuyển-con-trỏ-file-fseek-ftell-rewind)
- [7. Kiểm tra lỗi và End-of-File](#7-kiểm-tra-lỗi-và-end-of-file)
- [8. Ứng dụng: Quản lý dữ liệu Struct với File](#8-ứng-dụng-quản-lý-dữ-liệu-struct-với-file)

### Phần 3: Bài tập thực hành tổng hợp

- [1. Quản lý danh sách sinh viên](#1-quản-lý-danh-sách-sinh-viên)
- [2. Quản lý sản phẩm trong cửa hàng](#2-quản-lý-sản-phẩm-trong-cửa-hàng)
- [3. Hệ thống quản lý thư viện sách](#3-hệ-thống-quản-lý-thư-viện-sách)

---

# Phần 1: Struct (Cấu trúc)

## 1. Struct là gì?

**Struct** (structure - cấu trúc) là một kiểu dữ liệu do người dùng định nghĩa, cho phép bạn **nhóm nhiều biến có kiểu dữ liệu khác nhau** thành một đơn vị duy nhất.

### Tại sao cần Struct?

Giả sử bạn muốn quản lý thông tin của một sinh viên:

- Tên (string)
- Tuổi (int)
- Điểm trung bình (float)

**Cách làm KHÔNG dùng Struct** (rất rối):

```c
char name1[50] = "Nguyen Van A";
int age1 = 20;
float gpa1 = 3.5;

char name2[50] = "Tran Thi B";
int age2 = 21;
float gpa2 = 3.8;
// ... Nếu có 100 sinh viên thì sao???
```

**Cách làm DÙNG Struct** (rõ ràng và dễ quản lý):

```c
struct Student {
    char name[50];
    int age;
    float gpa;
};

struct Student student1 = {"Nguyen Van A", 20, 3.5};
struct Student student2 = {"Tran Thi B", 21, 3.8};
```

### Phép ẩn dụ

Hãy tưởng tượng bạn đang làm **hồ sơ nhân viên** trong một công ty:

- **Biến thông thường**: Mỗi thông tin là một tờ giấy riêng lẻ (tên một tờ, tuổi một tờ, địa chỉ một tờ).
- **Struct**: Tất cả thông tin được gom vào một **tập hồ sơ** duy nhất, dễ dàng mang theo và quản lý.

---

## 2. Khai báo và sử dụng Struct

### Cú pháp khai báo

```c
struct TenStruct {
    kieu_du_lieu thanh_vien_1;
    kieu_du_lieu thanh_vien_2;
    // ... thêm các thành viên khác
};
```

### Ví dụ cụ thể

```c
#include <stdio.h>
#include <string.h>

// Khai báo struct
struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    // Tạo biến kiểu struct
    struct Student sv1;

    // Gán giá trị cho từng thành viên
    strcpy(sv1.name, "Nguyen Van A");
    sv1.age = 20;
    sv1.gpa = 3.5;

    // In thông tin
    printf("Ten: %s\n", sv1.name);
    printf("Tuoi: %d\n", sv1.age);
    printf("Diem TB: %.2f\n", sv1.gpa);

    return 0;
}
```

**Kết quả:**

```
Ten: Nguyen Van A
Tuoi: 20
Diem TB: 3.50
```

---

## 3. Các cách khởi tạo Struct

### Cách 1: Khởi tạo từng thành viên

```c
struct Student sv1;
strcpy(sv1.name, "Nguyen Van A");
sv1.age = 20;
sv1.gpa = 3.5;
```

### Cách 2: Khởi tạo bằng danh sách (List initialization)

```c
struct Student sv1 = {"Nguyen Van A", 20, 3.5};
```

### Cách 3: Khởi tạo theo tên thành viên (Designated initialization - C99)

```c
struct Student sv1 = {
    .name = "Nguyen Van A",
    .age = 20,
    .gpa = 3.5
};
```

**Lợi ích:** Không cần theo thứ tự khai báo.

```c
struct Student sv2 = {
    .gpa = 3.8,        // Có thể đổi thứ tự
    .name = "Tran Thi B",
    .age = 21
};
```

### Cách 4: Khởi tạo một phần

```c
struct Student sv3 = {"Le Van C", 19};  // gpa sẽ là 0.0 (mặc định)
```

### Ví dụ tổng hợp

```c
#include <stdio.h>
#include <string.h>

struct Point {
    int x;
    int y;
};

int main() {
    // Cách 1
    struct Point p1;
    p1.x = 10;
    p1.y = 20;

    // Cách 2
    struct Point p2 = {30, 40};

    // Cách 3
    struct Point p3 = {.y = 60, .x = 50};

    printf("p1: (%d, %d)\n", p1.x, p1.y);
    printf("p2: (%d, %d)\n", p2.x, p2.y);
    printf("p3: (%d, %d)\n", p3.x, p3.y);

    return 0;
}
```

---

## 4. Truy cập thành viên của Struct

### Toán tử `.` (Dot operator)

Dùng để truy cập thành viên của struct qua **biến struct**.

```c
struct Student sv1 = {"Nguyen Van A", 20, 3.5};
printf("%s\n", sv1.name);    // Truy cập name
printf("%d\n", sv1.age);     // Truy cập age
```

### Toán tử `->` (Arrow operator)

Dùng để truy cập thành viên của struct qua **con trỏ struct**.

```c
struct Student sv1 = {"Nguyen Van A", 20, 3.5};
struct Student *ptr = &sv1;

// Cách 1: Dùng dereference và dot
printf("%s\n", (*ptr).name);

// Cách 2: Dùng arrow (ngắn gọn hơn)
printf("%s\n", ptr->name);    // Tương đương (*ptr).name
printf("%d\n", ptr->age);
```

### So sánh `.` và `->`

| Toán tử | Sử dụng với    | Ví dụ       |
| ------- | -------------- | ----------- |
| `.`     | Biến struct    | `sv1.name`  |
| `->`    | Con trỏ struct | `ptr->name` |

**Quy tắc nhớ:**

- **Dấu chấm (.)**: "Tôi có cái đó, cho tôi xem."
- **Mũi tên (->)**: "Tôi biết địa chỉ của nó, đưa tôi đến đó."

---

## 5. Struct lồng nhau (Nested Struct)

Một struct có thể chứa struct khác bên trong.

### Ví dụ

```c
#include <stdio.h>
#include <string.h>

// Struct địa chỉ
struct Address {
    char street[50];
    char city[30];
    int zipcode;
};

// Struct sinh viên chứa struct địa chỉ
struct Student {
    char name[50];
    int age;
    struct Address addr;  // Struct lồng nhau
};

int main() {
    struct Student sv1;

    strcpy(sv1.name, "Nguyen Van A");
    sv1.age = 20;

    // Truy cập struct lồng nhau
    strcpy(sv1.addr.street, "123 Le Loi");
    strcpy(sv1.addr.city, "Ho Chi Minh");
    sv1.addr.zipcode = 70000;

    // In thông tin
    printf("Ten: %s\n", sv1.name);
    printf("Tuoi: %d\n", sv1.age);
    printf("Dia chi: %s, %s - %d\n",
           sv1.addr.street,
           sv1.addr.city,
           sv1.addr.zipcode);

    return 0;
}
```

**Kết quả:**

```
Ten: Nguyen Van A
Tuoi: 20
Dia chi: 123 Le Loi, Ho Chi Minh - 70000
```

---

## 6. Mảng của Struct

Bạn có thể tạo mảng chứa nhiều struct.

```c
#include <stdio.h>
#include <string.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    // Khai báo mảng 3 sinh viên
    struct Student students[3];

    // Khởi tạo sinh viên 1
    strcpy(students[0].name, "Nguyen Van A");
    students[0].age = 20;
    students[0].gpa = 3.5;

    // Khởi tạo sinh viên 2
    strcpy(students[1].name, "Tran Thi B");
    students[1].age = 21;
    students[1].gpa = 3.8;

    // Khởi tạo sinh viên 3
    strcpy(students[2].name, "Le Van C");
    students[2].age = 19;
    students[2].gpa = 3.2;

    // In danh sách sinh viên
    printf("Danh sach sinh vien:\n");
    for (int i = 0; i < 3; i++) {
        printf("%d. %s - Tuoi: %d - GPA: %.2f\n",
               i+1,
               students[i].name,
               students[i].age,
               students[i].gpa);
    }

    return 0;
}
```

### Khởi tạo mảng struct ngắn gọn

```c
struct Student students[3] = {
    {"Nguyen Van A", 20, 3.5},
    {"Tran Thi B", 21, 3.8},
    {"Le Van C", 19, 3.2}
};
```

---

## 7. Con trỏ và Struct

### Khai báo con trỏ struct

```c
struct Student sv1 = {"Nguyen Van A", 20, 3.5};
struct Student *ptr = &sv1;
```

### Truy cập thông qua con trỏ

```c
#include <stdio.h>
#include <string.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    struct Student sv1 = {"Nguyen Van A", 20, 3.5};
    struct Student *ptr = &sv1;

    // Cách 1: Dùng dereference
    printf("Ten: %s\n", (*ptr).name);

    // Cách 2: Dùng arrow (khuyến khích)
    printf("Ten: %s\n", ptr->name);
    printf("Tuoi: %d\n", ptr->age);
    printf("GPA: %.2f\n", ptr->gpa);

    // Thay đổi giá trị qua con trỏ
    ptr->age = 21;
    ptr->gpa = 3.7;

    printf("\nSau khi thay doi:\n");
    printf("Tuoi: %d\n", sv1.age);
    printf("GPA: %.2f\n", sv1.gpa);

    return 0;
}
```

### Cấp phát động cho Struct

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    // Cấp phát bộ nhớ động cho 1 sinh viên
    struct Student *ptr = (struct Student*)malloc(sizeof(struct Student));

    if (ptr == NULL) {
        printf("Khong du bo nho!\n");
        return 1;
    }

    // Gán giá trị
    strcpy(ptr->name, "Nguyen Van A");
    ptr->age = 20;
    ptr->gpa = 3.5;

    // In thông tin
    printf("Ten: %s\n", ptr->name);
    printf("Tuoi: %d\n", ptr->age);
    printf("GPA: %.2f\n", ptr->gpa);

    // Giải phóng bộ nhớ
    free(ptr);
    ptr = NULL;

    return 0;
}
```

---

## 8. Struct và Function

### Truyền Struct theo giá trị (Pass by value)

Khi truyền struct theo giá trị, **bản sao** của struct được tạo ra.

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
};

// Nhận struct theo giá trị
void printPoint(struct Point p) {
    printf("Point: (%d, %d)\n", p.x, p.y);

    // Thay đổi bản sao, không ảnh hưởng đến biến gốc
    p.x = 100;
    p.y = 100;
}

int main() {
    struct Point p1 = {10, 20};

    printPoint(p1);

    // Giá trị gốc không thay đổi
    printf("After function: (%d, %d)\n", p1.x, p1.y);

    return 0;
}
```

**Kết quả:**

```
Point: (10, 20)
After function: (10, 20)
```

### Truyền Struct theo con trỏ (Pass by reference)

**Khuyến khích** dùng cách này vì hiệu quả hơn (không tạo bản sao).

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
};

// Nhận con trỏ struct
void movePoint(struct Point *p, int dx, int dy) {
    p->x += dx;
    p->y += dy;
}

void printPoint(const struct Point *p) {
    printf("Point: (%d, %d)\n", p->x, p->y);
}

int main() {
    struct Point p1 = {10, 20};

    printf("Truoc khi di chuyen: ");
    printPoint(&p1);

    movePoint(&p1, 5, -3);

    printf("Sau khi di chuyen: ");
    printPoint(&p1);

    return 0;
}
```

**Kết quả:**

```
Truoc khi di chuyen: Point: (10, 20)
Sau khi di chuyen: Point: (15, 17)
```

### Hàm trả về Struct

```c
#include <stdio.h>

struct Point {
    int x;
    int y;
};

// Hàm trả về struct
struct Point createPoint(int x, int y) {
    struct Point p;
    p.x = x;
    p.y = y;
    return p;
}

struct Point addPoints(struct Point p1, struct Point p2) {
    struct Point result;
    result.x = p1.x + p2.x;
    result.y = p1.y + p2.y;
    return result;
}

int main() {
    struct Point p1 = createPoint(10, 20);
    struct Point p2 = createPoint(5, 15);

    struct Point sum = addPoints(p1, p2);

    printf("p1: (%d, %d)\n", p1.x, p1.y);
    printf("p2: (%d, %d)\n", p2.x, p2.y);
    printf("Sum: (%d, %d)\n", sum.x, sum.y);

    return 0;
}
```

---

## 9. Typedef với Struct

`typedef` cho phép bạn tạo **tên mới** (alias) cho một kiểu dữ liệu.

### Không dùng typedef (phải viết `struct` mỗi lần)

```c
struct Student {
    char name[50];
    int age;
};

struct Student sv1;  // Phải viết "struct"
struct Student sv2;
```

### Dùng typedef (ngắn gọn hơn)

```c
typedef struct {
    char name[50];
    int age;
} Student;

Student sv1;  // Không cần viết "struct"
Student sv2;
```

### Cú pháp typedef

**Cách 1:**

```c
typedef struct Student {
    char name[50];
    int age;
} Student;

// Bây giờ có thể dùng cả 2 cách:
struct Student sv1;  // Cách cũ
Student sv2;         // Cách mới (ngắn gọn)
```

**Cách 2 (phổ biến nhất):**

```c
typedef struct {
    char name[50];
    int age;
} Student;

// Chỉ dùng được:
Student sv1;
```

### Ví dụ so sánh

```c
#include <stdio.h>
#include <string.h>

// Không dùng typedef
struct Point {
    int x;
    int y;
};

// Dùng typedef
typedef struct {
    int x;
    int y;
} Point2D;

int main() {
    // Cách cũ - phải viết "struct"
    struct Point p1 = {10, 20};

    // Cách mới - ngắn gọn hơn
    Point2D p2 = {30, 40};

    printf("p1: (%d, %d)\n", p1.x, p1.y);
    printf("p2: (%d, %d)\n", p2.x, p2.y);

    return 0;
}
```

---

## 10. Kích thước của Struct (Size và Padding)

### Kích thước Struct

Kích thước của struct **không đơn giản** là tổng kích thước các thành viên.

```c
#include <stdio.h>

struct Example {
    char c;      // 1 byte
    int i;       // 4 bytes
    short s;     // 2 bytes
};

int main() {
    printf("Size of char: %zu\n", sizeof(char));
    printf("Size of int: %zu\n", sizeof(int));
    printf("Size of short: %zu\n", sizeof(short));
    printf("Sum: %zu\n", sizeof(char) + sizeof(int) + sizeof(short));

    printf("\nSize of struct Example: %zu\n", sizeof(struct Example));

    return 0;
}
```

**Kết quả (trên hệ thống 64-bit):**

```
Size of char: 1
Size of int: 4
Size of short: 2
Sum: 7

Size of struct Example: 12  ← Lớn hơn 7!
```

### Tại sao lại 12 bytes?

Đó là do **structure padding** (đệm cấu trúc). Trình biên dịch thêm các byte trống để căn chỉnh bộ nhớ (memory alignment), giúp CPU truy cập nhanh hơn.

### Minh họa padding

```
struct Example {
    char c;     // 1 byte
    [3 bytes padding]
    int i;      // 4 bytes
    short s;    // 2 bytes
    [2 bytes padding]
};

Tổng: 1 + 3 + 4 + 2 + 2 = 12 bytes
```

### Tối ưu hóa kích thước Struct

**Không tối ưu:**

```c
struct Bad {
    char c;      // 1 byte
    int i;       // 4 bytes (+ 3 padding)
    char d;      // 1 byte
};
// Tổng: 12 bytes
```

**Đã tối ưu:**

```c
struct Good {
    int i;       // 4 bytes
    char c;      // 1 byte
    char d;      // 1 byte
    [2 bytes padding]
};
// Tổng: 8 bytes
```

**Quy tắc:** Sắp xếp các thành viên **từ lớn đến nhỏ** để giảm padding.

---

# Phần 2: File I/O (Input/Output với File)

## 1. Giới thiệu về File I/O

**File I/O** (Input/Output) là khả năng đọc và ghi dữ liệu vào file trên ổ cứng.

### Tại sao cần File I/O?

- **Lưu trữ dữ liệu lâu dài**: Dữ liệu trong RAM sẽ mất khi tắt máy. File giúp lưu trữ vĩnh viễn.
- **Xử lý dữ liệu lớn**: Không thể nhập tay hàng ngàn dòng dữ liệu.
- **Trao đổi dữ liệu**: Chia sẻ dữ liệu giữa các chương trình.

### Các loại file

1. **Text File** (File văn bản):

   - Lưu dữ liệu dưới dạng ký tự có thể đọc được
   - Ví dụ: `.txt`, `.csv`, `.log`
   - Có thể mở bằng Notepad

2. **Binary File** (File nhị phân):
   - Lưu dữ liệu dưới dạng nhị phân (0 và 1)
   - Ví dụ: `.exe`, `.jpg`, `.dat`
   - Không thể đọc trực tiếp bằng Notepad
   - Hiệu quả hơn với dữ liệu phức tạp (struct)

---

## 2. Con trỏ FILE

Trong C, mọi thao tác với file đều thông qua **con trỏ FILE**.

```c
FILE *fp;
```

`FILE` là một struct được định nghĩa trong `<stdio.h>`, chứa thông tin về file:

- Vị trí hiện tại trong file
- Chế độ mở file (đọc/ghi)
- Buffer (bộ đệm)

**Phép ẩn dụ:**

- **Con trỏ FILE**: Như một "chiếc bookmark" đánh dấu vị trí bạn đang đọc trong cuốn sách (file).

---

## 3. Mở và đóng file

### Hàm `fopen()` - Mở file

**Cú pháp:**

```c
FILE *fopen(const char *filename, const char *mode);
```

- `filename`: Tên file (có thể có đường dẫn)
- `mode`: Chế độ mở file
- **Trả về**: Con trỏ FILE nếu thành công, `NULL` nếu thất bại

### Các chế độ mở file (mode)

| Mode   | Ý nghĩa           | File không tồn tại | File đã tồn tại       |
| ------ | ----------------- | ------------------ | --------------------- |
| `"r"`  | Read (đọc)        | Lỗi                | Đọc từ đầu            |
| `"w"`  | Write (ghi)       | Tạo mới            | **Xóa nội dung cũ**   |
| `"a"`  | Append (ghi thêm) | Tạo mới            | Ghi vào cuối          |
| `"r+"` | Read + Write      | Lỗi                | Đọc/ghi từ đầu        |
| `"w+"` | Write + Read      | Tạo mới            | **Xóa nội dung cũ**   |
| `"a+"` | Append + Read     | Tạo mới            | Đọc toàn bộ, ghi cuối |

**Lưu ý:** Thêm `b` vào mode để làm việc với binary file:

- `"rb"`: Đọc file nhị phân
- `"wb"`: Ghi file nhị phân
- `"ab"`: Ghi thêm vào file nhị phân

### Hàm `fclose()` - Đóng file

**Cú pháp:**

```c
int fclose(FILE *fp);
```

**Tại sao phải đóng file?**

- Giải phóng tài nguyên hệ thống
- Đảm bảo dữ liệu được ghi hoàn toàn (flush buffer)
- Tránh mất dữ liệu

### Ví dụ mở và đóng file

```c
#include <stdio.h>

int main() {
    FILE *fp;

    // Mở file để ghi
    fp = fopen("test.txt", "w");

    // Kiểm tra xem mở file có thành công không
    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    printf("Mo file thanh cong!\n");

    // Đóng file
    fclose(fp);

    return 0;
}
```

---

## 4. Đọc và ghi file ở chế độ Text

### Ghi file văn bản

#### `fprintf()` - Ghi có định dạng

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("output.txt", "w");

    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    // Ghi dữ liệu vào file (giống printf)
    fprintf(fp, "Hello, File I/O!\n");
    fprintf(fp, "So nguyen: %d\n", 42);
    fprintf(fp, "So thuc: %.2f\n", 3.14);

    fclose(fp);
    printf("Da ghi file thanh cong!\n");

    return 0;
}
```

**Nội dung file `output.txt`:**

```
Hello, File I/O!
So nguyen: 42
So thuc: 3.14
```

#### `fputs()` - Ghi chuỗi

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("text.txt", "w");

    if (fp == NULL) return 1;

    fputs("Dong 1\n", fp);
    fputs("Dong 2\n", fp);
    fputs("Dong 3\n", fp);

    fclose(fp);

    return 0;
}
```

#### `fputc()` - Ghi từng ký tự

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("chars.txt", "w");

    if (fp == NULL) return 1;

    fputc('A', fp);
    fputc('B', fp);
    fputc('C', fp);
    fputc('\n', fp);

    fclose(fp);

    return 0;
}
```

### Đọc file văn bản

#### `fscanf()` - Đọc có định dạng

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("data.txt", "r");

    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    int number;
    float value;
    char name[50];

    // Giả sử file có dạng: "Alice 25 3.5"
    fscanf(fp, "%s %d %f", name, &number, &value);

    printf("Ten: %s\n", name);
    printf("So nguyen: %d\n", number);
    printf("So thuc: %.2f\n", value);

    fclose(fp);

    return 0;
}
```

#### `fgets()` - Đọc từng dòng

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("lines.txt", "r");

    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    char line[100];

    // Đọc từng dòng cho đến hết file
    while (fgets(line, sizeof(line), fp) != NULL) {
        printf("%s", line);
    }

    fclose(fp);

    return 0;
}
```

#### `fgetc()` - Đọc từng ký tự

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("text.txt", "r");

    if (fp == NULL) return 1;

    char ch;

    // Đọc từng ký tự cho đến EOF (End of File)
    while ((ch = fgetc(fp)) != EOF) {
        putchar(ch);
    }

    fclose(fp);

    return 0;
}
```

### Ví dụ tổng hợp: Copy file

```c
#include <stdio.h>

int main() {
    FILE *source, *dest;
    char ch;

    // Mở file nguồn để đọc
    source = fopen("source.txt", "r");
    if (source == NULL) {
        printf("Khong the mo file nguon!\n");
        return 1;
    }

    // Mở file đích để ghi
    dest = fopen("destination.txt", "w");
    if (dest == NULL) {
        printf("Khong the mo file dich!\n");
        fclose(source);
        return 1;
    }

    // Copy từng ký tự
    while ((ch = fgetc(source)) != EOF) {
        fputc(ch, dest);
    }

    printf("Copy file thanh cong!\n");

    fclose(source);
    fclose(dest);

    return 0;
}
```

---

## 5. Đọc và ghi file ở chế độ Binary

File binary hiệu quả hơn khi làm việc với struct và dữ liệu phức tạp.

### `fwrite()` - Ghi dữ liệu nhị phân

**Cú pháp:**

```c
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
```

- `ptr`: Con trỏ đến dữ liệu cần ghi
- `size`: Kích thước của mỗi phần tử (bytes)
- `nmemb`: Số lượng phần tử
- `stream`: Con trỏ FILE

**Ví dụ:**

```c
#include <stdio.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    FILE *fp = fopen("students.dat", "wb");

    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    struct Student sv1 = {"Nguyen Van A", 20, 3.5};

    // Ghi struct vào file
    fwrite(&sv1, sizeof(struct Student), 1, fp);

    fclose(fp);
    printf("Da ghi file thanh cong!\n");

    return 0;
}
```

### `fread()` - Đọc dữ liệu nhị phân

**Cú pháp:**

```c
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
```

**Ví dụ:**

```c
#include <stdio.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    FILE *fp = fopen("students.dat", "rb");

    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return 1;
    }

    struct Student sv1;

    // Đọc struct từ file
    fread(&sv1, sizeof(struct Student), 1, fp);

    printf("Ten: %s\n", sv1.name);
    printf("Tuoi: %d\n", sv1.age);
    printf("GPA: %.2f\n", sv1.gpa);

    fclose(fp);

    return 0;
}
```

### Ví dụ: Ghi và đọc nhiều struct

```c
#include <stdio.h>

typedef struct {
    char name[50];
    int age;
    float gpa;
} Student;

int main() {
    // ===== GHI FILE =====
    FILE *fp = fopen("students.dat", "wb");
    if (fp == NULL) return 1;

    Student students[3] = {
        {"Nguyen Van A", 20, 3.5},
        {"Tran Thi B", 21, 3.8},
        {"Le Van C", 19, 3.2}
    };

    // Ghi mảng struct vào file
    fwrite(students, sizeof(Student), 3, fp);
    fclose(fp);

    printf("Da ghi 3 sinh vien vao file!\n\n");

    // ===== ĐỌC FILE =====
    fp = fopen("students.dat", "rb");
    if (fp == NULL) return 1;

    Student readStudents[3];

    // Đọc mảng struct từ file
    fread(readStudents, sizeof(Student), 3, fp);
    fclose(fp);

    printf("Danh sach sinh vien doc tu file:\n");
    for (int i = 0; i < 3; i++) {
        printf("%d. %s - Tuoi: %d - GPA: %.2f\n",
               i+1,
               readStudents[i].name,
               readStudents[i].age,
               readStudents[i].gpa);
    }

    return 0;
}
```

---

## 6. Di chuyển con trỏ file (fseek, ftell, rewind)

### `ftell()` - Lấy vị trí hiện tại

```c
long ftell(FILE *stream);
```

Trả về vị trí hiện tại của con trỏ file (tính từ đầu file, đơn vị byte).

### `fseek()` - Di chuyển con trỏ file

```c
int fseek(FILE *stream, long offset, int whence);
```

- `offset`: Số byte cần dịch chuyển
- `whence`: Điểm tham chiếu
  - `SEEK_SET` (0): Từ đầu file
  - `SEEK_CUR` (1): Từ vị trí hiện tại
  - `SEEK_END` (2): Từ cuối file

### `rewind()` - Về đầu file

```c
void rewind(FILE *stream);
```

Tương đương `fseek(fp, 0, SEEK_SET)`.

### Ví dụ

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("test.txt", "w+");
    if (fp == NULL) return 1;

    // Ghi dữ liệu
    fputs("Hello World", fp);

    // Lấy vị trí hiện tại
    long pos = ftell(fp);
    printf("Vi tri hien tai: %ld\n", pos);  // 11

    // Về đầu file
    rewind(fp);
    printf("Vi tri sau rewind: %ld\n", ftell(fp));  // 0

    // Di chuyển đến byte thứ 6
    fseek(fp, 6, SEEK_SET);

    // Đọc phần còn lại
    char buffer[20];
    fgets(buffer, sizeof(buffer), fp);
    printf("Doc tu byte 6: %s\n", buffer);  // "World"

    fclose(fp);

    return 0;
}
```

### Ví dụ: Đọc struct ở vị trí bất kỳ

```c
#include <stdio.h>

typedef struct {
    char name[50];
    int age;
} Student;

int main() {
    FILE *fp = fopen("students.dat", "rb");
    if (fp == NULL) return 1;

    // Di chuyển đến sinh viên thứ 3 (index 2)
    fseek(fp, 2 * sizeof(Student), SEEK_SET);

    Student sv;
    fread(&sv, sizeof(Student), 1, fp);

    printf("Sinh vien thu 3: %s - %d tuoi\n", sv.name, sv.age);

    fclose(fp);

    return 0;
}
```

---

## 7. Kiểm tra lỗi và End-of-File

### `feof()` - Kiểm tra hết file

```c
int feof(FILE *stream);
```

Trả về **giá trị khác 0** nếu đã đến cuối file.

### `ferror()` - Kiểm tra lỗi

```c
int ferror(FILE *stream);
```

Trả về **giá trị khác 0** nếu có lỗi xảy ra.

### Ví dụ

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("data.txt", "r");
    if (fp == NULL) {
        perror("Loi mo file");
        return 1;
    }

    char ch;
    while ((ch = fgetc(fp)) != EOF) {
        putchar(ch);

        // Kiểm tra lỗi
        if (ferror(fp)) {
            printf("\nLoi khi doc file!\n");
            break;
        }
    }

    // Kiểm tra đã hết file chưa
    if (feof(fp)) {
        printf("\nDa doc het file!\n");
    }

    fclose(fp);

    return 0;
}
```

---

## 8. Ứng dụng: Quản lý dữ liệu Struct với File

### Chương trình quản lý sinh viên đơn giản

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    int id;
    char name[50];
    float gpa;
} Student;

// Lưu sinh viên vào file
void saveStudent(const char *filename, Student sv) {
    FILE *fp = fopen(filename, "ab");  // append binary
    if (fp == NULL) {
        printf("Khong the mo file!\n");
        return;
    }

    fwrite(&sv, sizeof(Student), 1, fp);
    fclose(fp);

    printf("Da luu sinh vien vao file!\n");
}

// Hiển thị tất cả sinh viên
void displayAllStudents(const char *filename) {
    FILE *fp = fopen(filename, "rb");
    if (fp == NULL) {
        printf("Chua co du lieu!\n");
        return;
    }

    Student sv;
    int count = 1;

    printf("\n===== DANH SACH SINH VIEN =====\n");
    while (fread(&sv, sizeof(Student), 1, fp) == 1) {
        printf("%d. ID: %d | Ten: %s | GPA: %.2f\n",
               count++, sv.id, sv.name, sv.gpa);
    }

    fclose(fp);
}

// Tìm sinh viên theo ID
void findStudentByID(const char *filename, int id) {
    FILE *fp = fopen(filename, "rb");
    if (fp == NULL) {
        printf("Chua co du lieu!\n");
        return;
    }

    Student sv;
    int found = 0;

    while (fread(&sv, sizeof(Student), 1, fp) == 1) {
        if (sv.id == id) {
            printf("\nTim thay sinh vien:\n");
            printf("ID: %d\n", sv.id);
            printf("Ten: %s\n", sv.name);
            printf("GPA: %.2f\n", sv.gpa);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Khong tim thay sinh vien co ID %d\n", id);
    }

    fclose(fp);
}

int main() {
    const char *filename = "students.dat";
    int choice;

    while (1) {
        printf("\n===== QUAN LY SINH VIEN =====\n");
        printf("1. Them sinh vien\n");
        printf("2. Hien thi danh sach\n");
        printf("3. Tim sinh vien theo ID\n");
        printf("4. Thoat\n");
        printf("Lua chon: ");
        scanf("%d", &choice);

        if (choice == 1) {
            Student sv;
            printf("Nhap ID: ");
            scanf("%d", &sv.id);
            printf("Nhap ten: ");
            getchar();  // Xóa newline
            fgets(sv.name, sizeof(sv.name), stdin);
            sv.name[strcspn(sv.name, "\n")] = '\0';  // Xóa newline
            printf("Nhap GPA: ");
            scanf("%f", &sv.gpa);

            saveStudent(filename, sv);

        } else if (choice == 2) {
            displayAllStudents(filename);

        } else if (choice == 3) {
            int id;
            printf("Nhap ID can tim: ");
            scanf("%d", &id);
            findStudentByID(filename, id);

        } else if (choice == 4) {
            printf("Tam biet!\n");
            break;

        } else {
            printf("Lua chon khong hop le!\n");
        }
    }

    return 0;
}
```

---

# Phần 3: Bài tập thực hành tổng hợp

## 1. Quản lý danh sách sinh viên

**Yêu cầu:**

- Tạo struct `Student` với các thông tin: ID, Tên, Tuổi, GPA
- Viết chương trình cho phép:
  1. Thêm sinh viên mới
  2. Hiển thị danh sách sinh viên
  3. Tìm sinh viên theo ID
  4. Xóa sinh viên theo ID
  5. Cập nhật thông tin sinh viên
  6. Lưu và đọc dữ liệu từ file

**Gợi ý:**

- Dùng file binary để lưu trữ
- Dùng mảng tạm để xóa/cập nhật sinh viên

---

## 2. Quản lý sản phẩm trong cửa hàng

**Yêu cầu:**

- Tạo struct `Product` với: Mã SP, Tên, Giá, Số lượng
- Chức năng:
  1. Thêm sản phẩm
  2. Hiển thị danh sách sản phẩm
  3. Tìm sản phẩm theo mã
  4. Cập nhật giá và số lượng
  5. Tính tổng giá trị kho hàng
  6. Lưu vào file CSV (text file)

**Ví dụ file CSV:**

```
P001,Laptop,15000000,10
P002,Mouse,200000,50
P003,Keyboard,500000,30
```

---

## 3. Hệ thống quản lý thư viện sách

**Yêu cầu:**

- Tạo struct `Book` với: ISBN, Tên sách, Tác giả, Năm xuất bản, Trạng thái (đang mượn/có sẵn)
- Tạo struct `Borrower` với: ID người mượn, Tên, ISBN sách mượn, Ngày mượn
- Chức năng:
  1. Thêm sách mới
  2. Hiển thị danh sách sách
  3. Mượn sách (cập nhật trạng thái)
  4. Trả sách
  5. Xem lịch sử mượn sách
  6. Lưu dữ liệu vào 2 file: `books.dat` và `borrowers.dat`

---

## Tổng kết

### Key Takeaways về Struct

1. **Struct nhóm nhiều biến khác kiểu thành một đơn vị**
2. **Truy cập thành viên:** Dùng `.` với biến, dùng `->` với con trỏ
3. **Typedef giúp code ngắn gọn hơn**
4. **Truyền struct vào hàm:** Nên dùng con trỏ (pass by reference) để hiệu quả
5. **Structure padding** làm kích thước struct lớn hơn tổng các thành viên

### Key Takeaways về File I/O

1. **Luôn kiểm tra `fopen()` có trả về `NULL` không**
2. **Luôn đóng file bằng `fclose()`**
3. **Text file:** Dùng `fprintf`, `fscanf`, `fgets`, `fputs`
4. **Binary file:** Dùng `fread`, `fwrite` (hiệu quả với struct)
5. **Các mode quan trọng:**
   - `"r"`: Chỉ đọc
   - `"w"`: Ghi (xóa nội dung cũ)
   - `"a"`: Ghi thêm vào cuối
   - Thêm `+` để đọc và ghi
   - Thêm `b` cho binary

### Bảng tham khảo nhanh

| Hàm         | Công dụng             | Ví dụ                            |
| ----------- | --------------------- | -------------------------------- |
| `fopen()`   | Mở file               | `fp = fopen("file.txt", "r")`    |
| `fclose()`  | Đóng file             | `fclose(fp)`                     |
| `fprintf()` | Ghi text có định dạng | `fprintf(fp, "%d", num)`         |
| `fscanf()`  | Đọc text có định dạng | `fscanf(fp, "%d", &num)`         |
| `fgets()`   | Đọc dòng              | `fgets(line, 100, fp)`           |
| `fputs()`   | Ghi chuỗi             | `fputs("Hello", fp)`             |
| `fread()`   | Đọc binary            | `fread(&sv, sizeof(sv), 1, fp)`  |
| `fwrite()`  | Ghi binary            | `fwrite(&sv, sizeof(sv), 1, fp)` |
| `fseek()`   | Di chuyển con trỏ     | `fseek(fp, 0, SEEK_SET)`         |
| `ftell()`   | Lấy vị trí hiện tại   | `pos = ftell(fp)`                |
| `rewind()`  | Về đầu file           | `rewind(fp)`                     |
| `feof()`    | Kiểm tra EOF          | `if (feof(fp))`                  |
| `ferror()`  | Kiểm tra lỗi          | `if (ferror(fp))`                |

---

**Chúc bạn học tốt và thực hành nhiều để thành thạo Struct và File I/O trong C!** 🚀
