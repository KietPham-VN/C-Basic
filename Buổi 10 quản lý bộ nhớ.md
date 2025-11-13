# Quản Lý bộ nhớ trong C

## 1. Các Vùng Bộ Nhớ (Memory Segments)

### 1.1 📝 Vùng Code/Text (Text Segment)

- **Chức năng**: Lưu trữ mã máy (machine code) thực thi của chương trình.
- **Đặc điểm**: Thường là chỉ đọc (read-only). Kích thước cố định.

### 2. 📊 Vùng Data (Data Segment)

#### 2.1. Vùng Initialized Data Segment

- **Chức năng**: Lưu trữ các biến toàn cục (global) và tĩnh (static) đã được khởi tạo bằng một giá trị khác 0.
- **Đặc điểm**: Dữ liệu này được tải từ file thực thi. Kích thước cố định.

#### 2.2 Vùng BSS (Block Started by Symbol)

- **Chức năng**: Lưu trữ các biến toàn cục và tĩnh chưa được khởi tạo hoặc được khởi tạo bằng 0 một cách rõ ràng.
- **Đặc điểm**: Không chiếm dung lượng trong file thực thi. Hệ điều hành cấp phát và khởi tạo tất cả bằng 0 lúc chương trình chạy.

### 3. 📚 Vùng Stack (Ngăn Xếp)

- **Chức năng**: Dành cho cấp phát tự động (Automatic Allocation). Lưu trữ biến cục bộ và thông tin lời gọi hàm.
- **Đặc điểm**: Kích thước linh hoạt, tăng trưởng về phía địa chỉ thấp hơn (trên hầu hết các kiến trúc). Bộ nhớ tự động giải phóng khi hàm kết thúc.

### 4. 📈 Vùng Heap (Bộ Nhớ Động)

- **Chức năng**: Dành cho cấp phát bộ nhớ động (Dynamic Allocation) bằng các hàm `malloc()`, `calloc()`, và `realloc()`.
- **Đặc điểm**: Kích thước linh hoạt, tăng trưởng về phía địa chỉ cao hơn. Phải được giải phóng thủ công bằng `free()`.

> Trong nhiều tài liệu, người ta thường nhóm Vùng Dữ liệu Khởi tạo và Vùng BSS lại thành một Vùng Dữ liệu (Data Segment) chung, từ đó tạo ra 4 khu vực chính: Text/Code, Data (gồm BSS và Initialized Data), Heap, Stack.

---

```c
#include <stdio.h>
#include <stdlib.h> // Cần thiết cho malloc và free

// 1. Vùng DỮ LIỆU KHỞI TẠO (Initialized Data Segment)
// Biến toàn cục được khởi tạo khác 0
int global_initialized_var = 100;

// Biến tĩnh toàn cục được khởi tạo
static const char *const_string = "Vùng Text (Read-Only) và Data";

// 2. Vùng BSS (Block Started by Symbol - Uninitialized Data Segment)
// Biến toàn cục không khởi tạo (mặc định là 0)
int global_uninitialized_var; // Hệ thống tự khởi tạo là 0

// Mảng toàn cục lớn không khởi tạo (tối ưu kích thước file thực thi)
char bss_array[1024]; // 1KB trong BSS

// 3. Vùng CODE/TEXT (Text Segment)
// Mã máy của hàm main() và func_stack_example() sẽ nằm ở đây.

void func_stack_example(int param_a, int param_b) {
    // 4. Vùng STACK (Stack Segment)
    // Biến cục bộ (local variables) - Tự động cấp phát/giải phóng
    int stack_local_var = param_a + param_b;
    char stack_buffer[64]; // Một buffer nhỏ trên Stack

    printf("\n--- Vùng STACK ---\n");
    printf("Địa chỉ biến cục bộ (stack_local_var): %p (Địa chỉ thấp)\n", &stack_local_var);
    printf("Địa chỉ tham số hàm (param_a):         %p\n", &param_a);
    printf("Biến cục bộ = %d\n", stack_local_var);

    // Khi hàm này kết thúc, stack_local_var và stack_buffer sẽ bị giải phóng.
}

int main() {
    // Biến cục bộ của main() cũng nằm trên Stack
    int stack_main_var = 42;

    // 5. Vùng HEAP (Heap Segment)
    // Con trỏ sẽ lưu trữ trên Stack, nhưng vùng nhớ trỏ tới là trên Heap
    int *heap_ptr_int = NULL;
    char *heap_ptr_char = NULL;
    int array_size = 5;

    // Cấp phát động
    heap_ptr_int = (int*) malloc(array_size * sizeof(int));
    heap_ptr_char = (char*) calloc(20, sizeof(char));

    // --- KIỂM TRA LỖI CẤP PHÁT ---
    if (heap_ptr_int == NULL || heap_ptr_char == NULL) {
        printf("Lỗi cấp phát bộ nhớ động (Heap)!\n");
        return 1;
    }

    // --- SỬ DỤNG VÀ IN ĐỊA CHỈ ---

    printf("--- Vùng CODE/TEXT ---\n");
    printf("Địa chỉ hàm main:             %p\n", (void *)main);
    printf("Địa chỉ hàm func_stack_example: %p\n", (void *)func_stack_example);

    printf("\n--- Vùng DATA (Initialized) ---\n");
    printf("Địa chỉ biến global_initialized_var: %p\n", &global_initialized_var);
    printf("Giá trị: %d\n", global_initialized_var);
    printf("Địa chỉ hằng chuỗi:                  %p\n", const_string); // Con trỏ ở Data, chuỗi ở Text/Read-Only

    printf("\n--- Vùng BSS (Uninitialized) ---\n");
    printf("Địa chỉ biến global_uninitialized_var: %p\n", &global_uninitialized_var);
    printf("Giá trị mặc định (đã khởi tạo 0): %d\n", global_uninitialized_var);
    printf("Địa chỉ mảng BSS:                     %p\n", bss_array);

    printf("\n--- Vùng HEAP ---\n");
    // Ghi dữ liệu vào Heap
    heap_ptr_int[0] = 99;
    printf("Địa chỉ khối malloc (Heap): %p\n", heap_ptr_int);
    printf("Giá trị đầu tiên (malloc): %d\n", heap_ptr_int[0]);
    printf("Địa chỉ khối calloc (Heap): %p\n", heap_ptr_char);
    printf("Giá trị đầu tiên (calloc, mặc định 0): %d\n", heap_ptr_char[0]);

    // Gọi hàm để minh họa Stack
    func_stack_example(10, 20);

    printf("\n--- Vùng STACK (main) ---\n");
    printf("Địa chỉ biến cục bộ main (stack_main_var): %p (Địa chỉ cao)\n", &stack_main_var);

    // --- QUAN TRỌNG: GIẢI PHÓNG HEAP ---
    free(heap_ptr_int);
    printf("\n* Đã giải phóng heap_ptr_int.\n");
    free(heap_ptr_char);
    printf("* Đã giải phóng heap_ptr_char.\n");

    // Tránh con trỏ lơ lửng
    heap_ptr_int = NULL;
    heap_ptr_char = NULL;

    return 0;
}
```
