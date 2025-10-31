---
tags:
  - C
  - Pointer
---

# Bài giảng: Nắm vững Con trỏ (Pointers) trong C

## Mục lục (Table of Contents)

### Phần 1: Con trỏ cơ bản
- [1. Con trỏ là gì?](#1-con-trỏ-là-gì)
- [2. Biến Thường vs. Biến Con Trỏ](#2-biến-thường-vs-biến-con-trỏ)
- [3. Tại sao phải dùng con trỏ?](#3-tại-sao-phải-dùng-con-trỏ)
- [4. Các toán tử quan trọng](#4-các-toán-tử-quan-trọng)
- [5. Ví dụ tổng hợp: Các thao tác cơ bản](#5-ví-dụ-tổng-hợp-các-thao-tác-cơ-bản)

### Phần 2: Con trỏ trỏ đến Con trỏ
- [1. Khái niệm](#1-khái-niệm-1)
- [2. Phân tích chi tiết](#2-phân-tích-chi-tiết)
- [3. Ví dụ Code tổng hợp](#3-ví-dụ-code-tổng-hợp)
- [4. Ứng dụng thực tế của `**`](#4-ứng-dụng-thực-tế-của-)
- [5. Tổng kết](#5-tổng-kết)

---

## 1. Con trỏ là gì?

- Hãy tưởng tượng bộ nhớ máy tính (RAM) của bạn là một dãy phố dài vô tận, và mỗi ngôi nhà trên đó có một địa chỉ duy nhất.
-   Khi bạn khai báo một biến, ví dụ: `int a = 10;`:
    -   Bạn đang nói với máy tính: "Hãy tìm một ngôi nhà trống (một ô nhớ), đặt tên nó là `a`, và cất số `10` vào bên trong đó."
    -   Giả sử ngôi nhà đó có địa chỉ là `123 Phố Chính`.

**Con trỏ (Pointer)** đơn giản là một loại biến đặc biệt. Thay vì chứa một giá trị như số `10`, nó lại chứa **địa chỉ** của một biến khác.

-   Ví dụ: Một con trỏ `p` có thể chứa giá trị `123 Phố Chính`.
-   Ta nói rằng "con trỏ `p` đang **trỏ tới** biến `a`".3

```c
#include <stdio.h>
int main(void) {
    int ThienAn = 0;
    int *Jack;
    Jack = &ThienAn;
    // do áp lực từ cộng đồng mạng 
    // nên mỗi tháng ảnh phải gởi 5tr cho Thiên An
    *Jack = 5000000;
    printf("\nSố Tiền của Thiên An nhận dc mỗi tháng là: %d", ThienAn);
    return 0;
}
```


---

## 2. Biến Thường vs. Biến Con Trỏ

Để hiểu rõ con trỏ, hãy so sánh nó với một biến thông thường.

```c
#include <stdio.h>

int main(void)
{
    int aNormalVariable = 100;
    // Nhắc lại bài bữa trước
    // Khi nhắn tới 1 biến thông thường thì có 2 thứ ta cần đề caafp
    // Giá trị 
    printf("%d\n", aNormalVariable);
    // và địa chỉ
    printf("%p\n", &aNormalVariable);
    // Còn khi ta nói về biến con trỏ
    // thì có tới tận 3 thứ ta cần đề cập
    int* aPointerVariable = &aNormalVariable;
    // giá trị 
    printf("%p\n", aPointerVariable);
    // địa chỉ 
    printf("%p\n", &aPointerVariable);
    // nơi nó trỏ về 
    printf("%d\n", *aPointerVariable);
    return 0;
}

```
### a. Biến thông thường (`int a = 1;`)

Khi nói về một biến thông thường, chúng ta có 2 thứ cần quan tâm:

- **Giá trị (Value):** Là dữ liệu mà biến đó chứa.
  - Ví dụ: `a` có giá trị là `1`.
  - Truy cập bằng cách dùng **tên biến**: `printf("%d", a);`
- **Địa chỉ (Address):** Là vị trí của biến đó trong bộ nhớ RAM.
  - Truy cập bằng cách dùng toán tử **`&`** (address-of): `printf("%p", &a);`

### b. Biến con trỏ (`int *pt; pt = &a;`)

Khi nói về một biến con trỏ, chúng ta có **3** thứ cần quan tâm:

- **Giá trị (Value):** Là nội dung mà _chính biến con trỏ_ lưu trữ. Giá trị này là **địa chỉ của một biến khác** (vùng nhớ mà nó trỏ tới).
  - Ví dụ: `pt` có giá trị là địa chỉ của `a` (giả sử là `0x7ffc1234abcd`).
  - Truy cập bằng cách dùng **tên biến**: `printf("%p", pt);`
- **Địa chỉ (Address):** Là vị trí của _chính biến con trỏ_ trong bộ nhớ. Bản thân con trỏ cũng là một biến, nên nó cũng phải có địa chỉ riêng.
  - Truy cập bằng cách dùng toán tử **`&`**: `printf("%p", &pt);` (Địa chỉ này sẽ khác với địa chỉ của `a`).
- **Giá trị tại vùng nhớ trỏ tới (Value at Address):** Đây là giá trị của biến mà con trỏ đang trỏ đến.
  - Ví dụ: Giá trị tại vùng nhớ mà `pt` trỏ tới là `1` (vì `pt` trỏ đến `a`).
  - Truy cập bằng cách dùng toán tử **`*`** (dereference): `printf("%d", *pt);`

---

## 3. Tại sao phải dùng con trỏ?

Con trỏ là một trong những khái niệm mạnh mẽ nhất nhưng cũng "khó nhằn" nhất trong C. Chúng ta dùng chúng vì:

1. **Thay đổi giá trị "gốc"**: Cho phép một hàm có thể thay đổi giá trị của biến được truyền vào (gọi là "truyền tham chiếu" - pass-by-reference).
2. **Quản lý bộ nhớ động**: Cho phép bạn yêu cầu và giải phóng bộ nhớ khi chương trình đang chạy (sử dụng `malloc` và `free`).
3. **Hiệu suất**: Làm việc với mảng và chuỗi hiệu quả hơn nhiều.
4. **Các cấu trúc dữ liệu phức tạp**: Rất cần thiết để xây dựng danh sách liên kết (linked lists), cây (trees), v.v.

---

## 4. Các toán tử quan trọng

Bạn chỉ cần nhớ 2 toán tử: `&` và `*`.

### a. Toán tử `&` (Address-of / "Địa chỉ của")

- Toán tử này lấy **địa chỉ** của một biến.
- Cách dùng: `&ten_bien`

```c
int a = 10;
// &a sẽ trả về địa chỉ của ngôi nhà tên "a" (ví dụ: 0x7ffc1234abcd)
printf("Địa chỉ của biến a là: %p\n", &a);
// %p là định dạng đặc biệt để in địa chỉ (dưới dạng hệ 16 - hexadecimal)
```

### b. Toán tử `*` (Dereference / "Giá trị tại")

Toán tử này có 2 ý nghĩa tùy thuộc vào ngữ cảnh:

**1. Khi khai báo (Declaration):**
- Nó dùng để **khai báo** một biến là con trỏ.    
- Cách dùng: `kieu_du_lieu *ten_con_tro;`

```c
int *ptr; // "ptr" là một con trỏ, nó sẽ chứa địa chỉ của một biến kiểu "int"
char *c_ptr; // "c_ptr" là một con trỏ, nó sẽ chứa địa chỉ của một biến kiểu "char"
```

**2. Khi sử dụng (Dereferencing):**

- Nó dùng để **lấy giá trị** tại địa chỉ mà con trỏ đang trỏ tới.
- Cách dùng: `*ten_con_tro`
- Bạn có thể đọc là: "giá trị tại địa chỉ mà `ptr` đang giữ".


```c
// *ptr nghĩa là "giá trị tại địa chỉ ptr đang trỏ tới"
printf("Giá trị mà ptr trỏ tới là: %d\n", *ptr);
```

---

## 5. Ví dụ tổng hợp: Các thao tác cơ bản

Hãy xem một ví dụ đầy đủ kết hợp mọi thứ.

```c
#include <stdio.h>

int main() {
    // 1. Khai báo một biến thông thường
    int var = 25;

    // 2. Khai báo một con trỏ kiểu int
    // "ptr" có thể lưu giữ địa chỉ của một biến int
    int *ptr;

    // 3. Gán địa chỉ:
    // Gán địa chỉ của 'var' cho con trỏ 'ptr'
    ptr = &var;

    // 4. In ra các giá trị và địa chỉ
    printf("--- Thông tin biến 'var' ---\n");
    printf("Giá trị của var: %d\n", var);
    printf("Địa chỉ của var (&var): %p\n", &var);

    printf("\n--- Thông tin con trỏ 'ptr' ---\n");
    // In giá trị của con trỏ (chính là địa chỉ của var)
    printf("Giá trị của ptr (địa chỉ nó giữ): %p\n", ptr);
    // In địa chỉ của chính con trỏ
    printf("Địa chỉ của chính con trỏ ptr (&ptr): %p\n", &ptr);

    // 5. Truy xuất giá trị (Dereferencing)
    // Dùng * để lấy giá trị tại địa chỉ mà ptr đang trỏ tới
    printf("Giá trị tại địa chỉ mà ptr trỏ tới (*ptr): %d\n", *ptr);

    // 6. Thay đổi giá trị "gốc" thông qua con trỏ
    printf("\n--- Thay đổi giá trị qua con trỏ ---\n");
    *ptr = 50; // "Đặt giá trị 50 vào ngôi nhà tại địa chỉ ptr"

    // Biến 'var' gốc đã bị thay đổi!
    printf("Giá trị mới của var: %d\n", var);
    printf("Giá trị mới tại *ptr: %d\n", *ptr);

    return 0;
}
```

**Kết quả chạy (địa chỉ sẽ khác trên máy của bạn):**

```
--- Thông tin biến 'var' ---
Giá trị của var: 25
Địa chỉ của var (&var): 0x7ffc1234abcd

--- Thông tin con trỏ 'ptr' ---
Giá trị của ptr (địa chỉ nó giữ): 0x7ffc1234abcd
Địa chỉ của chính con trỏ ptr (&ptr): 0x7ffc1234abc0
Giá trị tại địa chỉ mà ptr trỏ tới (*ptr): 25

--- Thay đổi giá trị qua con trỏ ---
Giá trị mới của var: 50
Giá trị mới tại *ptr: 50
```

---
# Phần 2: Con trỏ trỏ đến Con trỏ (Pointer to Pointer - `**`)

## 1. Khái niệm

Bạn đã biết con trỏ (`*`) là một biến lưu **địa chỉ** của một biến khác.

Vậy, **con trỏ cấp 2 (`**`)** đơn giản là một biến lưu **địa chỉ của một con trỏ khác**.

### Phép ẩn dụ (Tiếp nối)

1. **Biến thường (`int var`)**: Là "ngôi nhà" chứa một giá trị (ví dụ: số 10).
   - Địa chỉ nhà: `&var` (ví dụ: `0x100`)
2. **Con trỏ cấp 1 (`int *ptr`)**: Là "tờ giấy A" ghi lại **địa chỉ của ngôi nhà** (`0x100`).
   - Địa chỉ của tờ giấy A: `&ptr` (ví dụ: `0x200`)
3. **Con trỏ cấp 2 (`int **pptr`)**: Là "tờ giấy B" ghi lại **địa chỉ của tờ giấy A** (`0x200`).
   - Địa chỉ của tờ giấy B: `&pptr` (ví dụ: `0x300`)

> **Câu truyện tỏ tình với crush**

```c
#include <stdio.h>

int main(void)
{
    // tui đi học tui có crush 1 bạn nữ ở lớp kế bên
    // vẫn đề là tui ko có thông tin của cô ấy
    // vậy thì tui phải làm sao để tiếp cẩn cổ đây
    int myDearCrush = 2005;
    int** me;
    // tui chợt nhận ra tui ko có info của ẻm
    // nhưng tui có info của bạn thân của ẻm 
    int* banThanCuaCrush;
    // và bạn thân của ẻm thì chắc chắc có info của ẻm 
    banThanCuaCrush = &myDearCrush;
    // thông qua ban thân để tiếp cận ẻm
    me = &banThanCuaCrush;
    printf("%d\n", **me);
    return 0;
}

```


## 2. Phân tích chi tiết

Hãy xem sơ đồ các biến sau:

```c
int var = 10;
int *ptr;
int **pptr;

ptr = &var;    // ptr lưu địa chỉ của var
pptr = &ptr;   // pptr lưu địa chỉ của ptr
```

Bây giờ, chúng ta hãy "mổ xẻ" 3 biến này:

### a. Biến thường (`var`)

- **Giá trị (`var`)**: `10`
- **Địa chỉ (`&var`)**: `0x100` (giả sử)

### b. Con trỏ cấp 1 (`ptr`)

- **Giá trị (`ptr`)**: `0x100` (vì nó lưu địa chỉ của `var`)
- **Địa chỉ (`&ptr`)**: `0x200` (giả sử)
- **Giá trị trỏ tới (`*ptr`)**: `10` (lấy giá trị tại địa chỉ `0x100`, chính là `var`)
    

### c. Con trỏ cấp 2 (`pptr`)

- **Giá trị (`pptr`)**: `0x200` (vì nó lưu địa chỉ của `ptr`)
- **Địa chỉ (`&pptr`)**: `0x300` (giả sử)
- **Giá trị trỏ tới 1 lần (`*pptr`)**:
  - "Lấy giá trị tại địa chỉ `0x200`"
  - Giá trị đó chính là nội dung của `ptr`, tức là `0x100`. 
  - Vậy: `*pptr == ptr` (cả hai đều có giá trị là `0x100`)
- **Giá trị trỏ tới 2 lần (`**pptr`)**:
  - Chính là `*(*pptr)`.
  - Vì `*pptr` là `ptr`, nên `**pptr` cũng là `*ptr`.
  - "Lấy giá trị tại địa chỉ mà `*pptr` đang giữ" (tức là `0x100`).
  - Giá trị đó chính là `10`.
  - Vậy: `**pptr == *ptr == var` (cả ba đều có giá trị là `10`)

---


## 3. Ví dụ Code tổng hợp

Đoạn code này sẽ in ra tất cả các giá trị và địa chỉ để làm rõ sơ đồ trên.



```c
#include <stdio.h>

int main() {
    int var = 10;
    int *ptr = &var;
    int **pptr = &ptr;

    // In thông tin của var
    printf("--- Biến 'var' ---\n");
    printf("Giá trị của var: %d\n", var);
    printf("Địa chỉ của var (&var): %p\n", &var);

    // In thông tin của con trỏ cấp 1 (ptr)
    printf("\n--- Con trỏ 'ptr' (cấp 1) ---\n");
    printf("Giá trị của ptr (lưu địa chỉ của var): %p\n", ptr);
    printf("Địa chỉ của chính ptr (&ptr): %p\n", &ptr);
    printf("Giá trị mà ptr trỏ tới (*ptr): %d\n", *ptr);

    // In thông tin của con trỏ cấp 2 (pptr)
    printf("\n--- Con trỏ 'pptr' (cấp 2) ---\n");
    printf("Giá trị của pptr (lưu địa chỉ của ptr): %p\n", pptr);
    printf("Địa chỉ của chính pptr (&pptr): %p\n", &pptr);
    printf("Giá trị mà pptr trỏ tới 1 lần (*pptr): %p\n", *pptr); // Sẽ bằng giá trị của ptr
    printf("Giá trị mà pptr trỏ tới 2 lần (**pptr): %d\n", **pptr); // Sẽ bằng giá trị của var

    // Thay đổi giá trị 'var' bằng con trỏ cấp 2
    printf("\n--- Thay đổi giá trị qua pptr ---\n");
    **pptr = 99; // Tương đương *(*pptr) = 99
    
    printf("Giá trị mới của **pptr: %d\n", **pptr);
    printf("Giá trị mới của *ptr: %d\n", *ptr);
    printf("Giá trị mới của var: %d\n", var); // var đã bị thay đổi!

    return 0;
}
```

**Kết quả chạy (địa chỉ sẽ khác trên máy của bạn):**

```
--- Biến 'var' ---
Giá trị của var: 10
Địa chỉ của var (&var): 0x7ffc...b3a4

--- Con trỏ 'ptr' (cấp 1) ---
Giá trị của ptr (lưu địa chỉ của var): 0x7ffc...b3a4
Địa chỉ của chính ptr (&ptr): 0x7ffc...b3a8
Giá trị mà ptr trỏ tới (*ptr): 10

--- Con trỏ 'pptr' (cấp 2) ---
Giá trị của pptr (lưu địa chỉ của ptr): 0x7ffc...b3a8
Địa chỉ của chính pptr (&pptr): 0x7ffc...b3b0
Giá trị mà pptr trỏ tới 1 lần (*pptr): 0x7ffc...b3a4
Giá trị mà pptr trỏ tới 2 lần (**pptr): 10

--- Thay đổi giá trị qua pptr ---
Giá trị mới của **pptr: 99
Giá trị mới của *ptr: 99
Giá trị mới của var: 99
```

---

## 4. Ứng dụng thực tế của `**`

Câu hỏi lớn nhất là: "Tại sao lại cần phức tạp như vậy?"

**Lý do chính:** Khi bạn muốn viết một hàm có khả năng **thay đổi chính con trỏ** được truyền vào.

Hãy nhớ lại: để thay đổi biến `int x` trong hàm, bạn phải truyền địa chỉ của nó (`&x`), tức là dùng `int *`. Tương tự: để thay đổi biến `int *ptr` trong hàm, bạn phải truyền địa chỉ của nó (`&ptr`), tức là dùng `int **`.

### Ví dụ: Hàm cấp phát bộ nhớ

Đây là một ví dụ kinh điển. Giả sử bạn muốn viết một hàm để cấp phát bộ nhớ cho một con trỏ.

**Cách làm SAI (dùng `*`):**


```c
#include <stdlib.h> // cho malloc

// Hàm này CHỈ nhận được một BẢN SAO của con trỏ p
void allocate_fail(int *p) {
    p = (int*)malloc(sizeof(int)); // p ở đây là bản sao
    *p = 100;
    // Khi hàm kết thúc, bản sao 'p' bị hủy. Con trỏ 'p' ở hàm main vẫn là NULL.
}

int main() {
    int *p = NULL;
    allocate_fail(p);
    // p vẫn là NULL!
    // printf("%d", *p); // SẼ GÂY LỖI SEGMENTATION FAULT
    return 0;
}
```

**Cách làm ĐÚNG (dùng `**`):** Chúng ta truyền vào **địa chỉ của con trỏ** (`&p`).


```c
#include <stdio.h>
#include <stdlib.h>

// Hàm này nhận vào địa chỉ của con trỏ p (tức là con trỏ cấp 2)
void allocate_success(int **pp) {
    // *pp chính là con trỏ p "gốc" ở hàm main
    *pp = (int*)malloc(sizeof(int)); 
    
    // Kiểm tra xem malloc có thành công không
    if (*pp != NULL) {
        **pp = 100; // Gán giá trị 100 vào vùng nhớ vừa cấp phát
    }
}

int main() {
    int *p = NULL; // Khởi tạo con trỏ là NULL
    
    // Truyền địa chỉ của p (tức là &p) vào hàm
    allocate_success(&p); 
    
    if (p != NULL) {
        printf("Cấp phát thành công!\n");
        printf("Giá trị tại vùng nhớ p trỏ tới: %d\n", *p); // In ra 100
        free(p); // Nhớ giải phóng bộ nhớ
    } else {
        printf("Cấp phát thất bại!\n");
    }
    
    return 0;
}
```

### Bàn về NULL trong C

- Trong ngôn ngữ lập trình C, NULL là một hằng đặc biệt dùng để biểu diễn rằng một con trỏ không trỏ đến bất kỳ vùng nhớ hợp lệ nào.
- Nói cách khác, NULL là cách để nói với trình biên dịch và lập trình viên rằng:

 
 > Con trỏ này hiện tại chưa trỏ tới đâu cả.

#### 1. Nguồn gốc của NULL

- NULL không phải là từ khóa của C, mà là một macro được định nghĩa trong các thư viện chuẩn như:


```c
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>
```


- Nếu bạn mở các file header này ra, bạn sẽ thấy định nghĩa tương tự như sau:

```c
#define NULL ((void*)0)
```


- Nghĩa là NULL thực chất là một con trỏ kiểu void* trỏ đến địa chỉ 0.

#### 2. Ý nghĩa và mục đích sử dụng

- Trong C, số 0 có thể đại diện cho số 0 hoặc con trỏ rỗng.
- Tuy nhiên, để tránh nhầm lẫn giữa hai khái niệm này, người ta định nghĩa NULL như một cách viết rõ ràng hơn.

- Khi một con trỏ được gán giá trị NULL, điều đó có nghĩa là:

> Con trỏ này không chứa địa chỉ hợp lệ nào, và không được phép dereference (*p).

Ví dụ:

```c
int* p = NULL;

if (p == NULL) {
    printf("Con trỏ p chưa trỏ tới đâu hết!\n");
}
```

#### 3. Tại sao lại là (void*)0 mà không chỉ là 0?

- 0 là một số nguyên, còn (void*)0 là một con trỏ null.
- C chuẩn yêu cầu rằng mọi con trỏ null phải có thể được biểu diễn bởi một hằng số bằng 0, nhưng để rõ ràng về kiểu dữ liệu, ta dùng (void*)0.
- Điều này giúp trình biên dịch hiểu chính xác kiểu dữ liệu, và giúp code dễ đọc hơn.

Ví dụ:

```c
int* p = (void*)0;   // tương đương với NULL
void* q = NULL;      // hoàn toàn hợp lệ
```

#### 4. **So sánh nhanh các cách biểu diễn**

| Biểu thức  | Nghĩa                | Kiểu dữ liệu | An toàn           |
| ---------- | -------------------- | ------------ | ----------------- |
| `0`        | Số 0                 | `int`        | ⚠️ Dễ nhầm        |
| `(void*)0` | Con trỏ null         | `void*`      | ✅ Rõ ràng         |
| `NULL`     | Macro cho `(void*)0` | Tùy header   | ✅ Chuẩn & rõ nhất |

#### 5. **Lưu ý khi sử dụng**

Không được dereference (*p) con trỏ NULL, vì sẽ gây lỗi segmentation fault.

Luôn khởi tạo con trỏ bằng NULL nếu bạn chưa biết nó sẽ trỏ tới đâu.

> Khi không còn dùng một con trỏ nữa, gán nó về NULL để tránh lỗi truy cập bộ nhớ

---

## 5. Tổng kết

- Con trỏ cấp 2 (`**pptr`) lưu **địa chỉ của con trỏ cấp 1** (`&ptr`).
- `*pptr` cho phép bạn truy cập và thay đổi giá trị của con trỏ cấp 1 (`ptr`).
- `**pptr` cho phép bạn truy cập và thay đổi giá trị của biến gốc (`var`).
- Công dụng quan trọng nhất là dùng làm tham số cho hàm, khi bạn muốn hàm đó có khả năng **thay đổi con trỏ gốc** (ví dụ: cấp phát bộ nhớ, trỏ con trỏ sang vùng nhớ khác).