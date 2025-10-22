# Buổi 5 Hàm (function)

## 1. Khái niệm về hàm (Function)

### 1.1 Định nghĩa
Hàm (Function) là một khối mã được đặt tên, có thể được gọi để thực hiện một tác vụ cụ thể. Hàm giúp:
- Chia chương trình thành các phần nhỏ, dễ quản lý (Modularity)
- Tái sử dụng mã (Code Reusability)
- Dễ debug và bảo trì (Maintainability)
- Tăng tính đọc hiểu của chương trình (Readability)

### 1.2 Cú pháp khai báo hàm
```c
kiểu_trả_về tên_hàm(danh_sách_tham_số) {
    // Thân hàm
    return giá_trị; // (nếu có)
}
```

### 1.3 Các thành phần của hàm (Function Components)
- **Kiểu trả về (Return Type)**: `int`, `float`, `char`, `void`, etc.
- **Tên hàm (Function Name)**: định danh duy nhất
- **Tham số (Parameters)**: dữ liệu đầu vào (có thể có hoặc không)
- **Thân hàm (Function Body)**: mã thực thi
- **Giá trị trả về (Return Value)**: kết quả của hàm

## 2. Phân loại hàm

### 2.1 Hàm có giá trị trả về (Function with Return Value)
```c
int tinhTong(int a, int b) {
    return a + b;
}

float tinhTrungBinh(float a, float b) {
    return (a + b) / 2.0;
}
```

### 2.2 Hàm không có giá trị trả về (Void Function)
```c
void inThongBao() {
    printf("Xin chao!\n");
}

void inSo(int n) {
    printf("So la: %d\n", n);
}
```

### 2.3 Hàm không có tham số (Function without Parameters)
```c
int laySoNgauNhien() {
    return rand() % 100;
}
```

### 2.4 Hàm có nhiều tham số (Function with Multiple Parameters)
```c
int timMax(int a, int b, int c) {
    int max = a;
    if (b > max) max = b;
    if (c > max) max = c;
    return max;
}
```

## 3. Khai báo và định nghĩa hàm

### 3.1 Prototype (Function Declaration - Khai báo hàm)
```c
// Khai báo hàm trước khi sử dụng
int tinhTong(int a, int b);
void inKetQua(int result);
float tinhCanBacHai(float x);
```

### 3.2 Định nghĩa hàm (Function Definition)
```c
// Định nghĩa hàm
int tinhTong(int a, int b) {
    return a + b;
}

void inKetQua(int result) {
    printf("Ket qua: %d\n", result);
}

float tinhCanBacHai(float x) {
    if (x < 0) {
        printf("Khong the tinh can bac hai cua so am!\n");
        return -1;
    }
    return sqrt(x);
}
```

## 4. Gọi hàm (Function Call)

### 4.1 Gọi hàm có giá trị trả về (Calling Function with Return Value)
```c
int main() {
    int a = 5, b = 3;
    int tong = tinhTong(a, b);  // Gọi hàm và lưu kết quả
    printf("Tong cua %d va %d la: %d\n", a, b, tong);
    
    // Gọi hàm trực tiếp trong printf
    printf("Tong: %d\n", tinhTong(10, 20));
    
    return 0;
}
```

### 4.2 Gọi hàm void (Calling Void Function)
```c
int main() {
    inThongBao();  // Gọi hàm không có tham số
    inSo(42);      // Gọi hàm có tham số
    
    return 0;
}
```

## 5. Tham số và đối số (Parameters and Arguments)

### 5.1 Truyền tham số theo giá trị (Pass by Value)
**Keywords**: Parameter, Argument, Pass by Value, Local Copy
```c
void tangGiaTri(int x) {
    x = x + 1;
    printf("Trong ham: x = %d\n", x);
}

int main() {
    int a = 5;
    printf("Truoc khi goi ham: a = %d\n", a);
    tangGiaTri(a);
    printf("Sau khi goi ham: a = %d\n", a);  // a vẫn là 5
    return 0;
}
```

### 5.2 Truyền tham số theo tham chiếu (Pass by Reference)
**Keywords**: Pass by Reference, Pointer, Address Operator (&), Dereference Operator (*)
```c
void tangGiaTri(int *x) {
    *x = *x + 1;
    printf("Trong ham: x = %d\n", *x);
}

int main() {
    int a = 5;
    printf("Truoc khi goi ham: a = %d\n", a);
    tangGiaTri(&a);
    printf("Sau khi goi ham: a = %d\n", a);  // a là 6
    return 0;
}
```

## 6. Scope và Lifetime của biến (Variable Scope and Lifetime)

### 6.1 Biến cục bộ (Local Variable)
**Keywords**: Local Scope, Block Scope, Function Scope
```c
void hamTest() {
    int x = 10;  // Biến cục bộ
    printf("Trong ham: x = %d\n", x);
}

int main() {
    int x = 5;   // Biến cục bộ khác
    printf("Trong main: x = %d\n", x);
    hamTest();
    printf("Trong main sau khi goi ham: x = %d\n", x);
    return 0;
}
```

### 6.2 Biến toàn cục (Global Variable)
**Keywords**: Global Scope, File Scope, External Linkage
```c
int bienToanCuc = 100;  // Biến toàn cục

void hamTest() {
    printf("Trong ham: bienToanCuc = %d\n", bienToanCuc);
    bienToanCuc = 200;
}

int main() {
    printf("Trong main: bienToanCuc = %d\n", bienToanCuc);
    hamTest();
    printf("Trong main sau khi goi ham: bienToanCuc = %d\n", bienToanCuc);
    return 0;
}
```

## 7. Hàm đệ quy (Recursive Function)
**Keywords**: Recursion, Recursive Call, Base Case, Recursive Case, Stack Overflow

### 7.1 Khái niệm
Hàm đệ quy (Recursive Function) là hàm gọi chính nó để giải quyết bài toán.
**Keywords**: Self-calling, Recursive Definition, Termination Condition

### 7.2 Ví dụ: Tính giai thừa (Factorial)
**Keywords**: Factorial, Base Case, Recursive Step
```c
long long giaiThua(int n) {
    // Điều kiện dừng
    if (n <= 1) {
        return 1;
    }
    // Bước đệ quy
    return n * giaiThua(n - 1);
}

int main() {
    int n;
    printf("Nhap n: ");
    scanf("%d", &n);
    printf("%d! = %lld\n", n, giaiThua(n));
    return 0;
}
```

### 7.3 Ví dụ: Dãy Fibonacci
**Keywords**: Fibonacci Sequence, Recursive Formula, Memoization
```c
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    printf("Nhap n: ");
    scanf("%d", &n);
    printf("So Fibonacci thu %d la: %d\n", n, fibonacci(n));
    return 0;
}
```

## 8. Một số hàm toán học thường dùng (Common Math Functions)
**Keywords**: Math Library, Standard Library, Header File (#include <math.h>)

```c
#include <math.h>

int main() {
    double x = 9.0;
    
    printf("sqrt(%.1f) = %.2f\n", x, sqrt(x));      // Căn bậc hai
    printf("pow(%.1f, 2) = %.2f\n", x, pow(x, 2));  // Lũy thừa
    printf("fabs(-%.1f) = %.2f\n", x, fabs(-x));    // Giá trị tuyệt đối
    printf("ceil(%.1f) = %.2f\n", x, ceil(x));      // Làm tròn lên
    printf("floor(%.1f) = %.2f\n", x, floor(x));    // Làm tròn xuống
    
    return 0;
}
```

## 9. Bài tập thực hành (Practice Exercises)
**Keywords**: Practice, Implementation, Code Examples, Problem Solving

### Bài tập 1: Hàm cơ bản (Basic Functions)
**Keywords**: Basic Operations, Arithmetic Functions, Input Validation
Viết các hàm sau:
1. Hàm tính tổng hai số nguyên
2. Hàm tính hiệu hai số nguyên
3. Hàm tính tích hai số nguyên
4. Hàm tính thương hai số thực
5. Hàm kiểm tra số chẵn/lẻ

**Gợi ý:**
```c
int tinhTong(int a, int b) {
    return a + b;
}

int tinhHieu(int a, int b) {
    return a - b;
}

int tinhTich(int a, int b) {
    return a * b;
}

float tinhThuong(float a, float b) {
    if (b == 0) {
        printf("Khong the chia cho 0!\n");
        return 0;
    }
    return a / b;
}

int kiemTraChanLe(int n) {
    return n % 2 == 0 ? 1 : 0;  // 1: chẵn, 0: lẻ
}
```

### Bài tập 2: Hàm kiểm tra (Validation Functions)
**Keywords**: Validation, Boolean Functions, Prime Number, Perfect Number, Palindrome
Viết các hàm kiểm tra:
1. Hàm kiểm tra số nguyên tố
2. Hàm kiểm tra số hoàn hảo
3. Hàm kiểm tra số đối xứng (palindrome)
4. Hàm kiểm tra năm nhuận

**Gợi ý:**
```c
int kiemTraSoNguyenTo(int n) {
    if (n < 2) return 0;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) return 0;
    }
    return 1;
}

int kiemTraSoHoanHao(int n) {
    int tong = 0;
    for (int i = 1; i < n; i++) {
        if (n % i == 0) {
            tong += i;
        }
    }
    return tong == n ? 1 : 0;
}

int kiemTraSoDoiXung(int n) {
    int temp = n, dao = 0;
    while (temp > 0) {
        dao = dao * 10 + temp % 10;
        temp /= 10;
    }
    return dao == n ? 1 : 0;
}

int kiemTraNamNhuan(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}
```

### Bài tập 3: Hàm tính toán (Calculation Functions)
**Keywords**: Summation, Iteration, Loop, Range Calculation
Viết các hàm tính:
1. Tính tổng các số từ 1 đến n
2. Tính tổng các số chẵn từ 1 đến n
3. Tính tổng các số lẻ từ 1 đến n
4. Tính tổng các số nguyên tố từ 1 đến n

**Gợi ý:**
```c
int tongTu1DenN(int n) {
    int tong = 0;
    for (int i = 1; i <= n; i++) {
        tong += i;
    }
    return tong;
}

int tongSoChan(int n) {
    int tong = 0;
    for (int i = 2; i <= n; i += 2) {
        tong += i;
    }
    return tong;
}

int tongSoLe(int n) {
    int tong = 0;
    for (int i = 1; i <= n; i += 2) {
        tong += i;
    }
    return tong;
}

int tongSoNguyenTo(int n) {
    int tong = 0;
    for (int i = 2; i <= n; i++) {
        if (kiemTraSoNguyenTo(i)) {
            tong += i;
        }
    }
    return tong;
}
```

### Bài tập 4: Hàm đệ quy (Recursive Functions)
**Keywords**: Recursive Implementation, Base Case, Recursive Call, Stack Management
Viết các hàm đệ quy:
1. Tính tổng các số từ 1 đến n
2. Tính lũy thừa a^n
3. Tìm ước chung lớn nhất (UCLN)
4. In các số từ n về 1

**Gợi ý:**
```c
int tongDeQuy(int n) {
    if (n == 1) return 1;
    return n + tongDeQuy(n - 1);
}

long long luyThua(int a, int n) {
    if (n == 0) return 1;
    if (n == 1) return a;
    return a * luyThua(a, n - 1);
}

int ucln(int a, int b) {
    if (b == 0) return a;
    return ucln(b, a % b);
}

void inNguoc(int n) {
    if (n == 0) return;
    printf("%d ", n);
    inNguoc(n - 1);
}
```

### Bài tập 5: Hàm với mảng (Array Functions)
**Keywords**: Array Processing, Array Manipulation, Sorting Algorithm, Search Algorithm
Viết các hàm:
1. Tìm phần tử lớn nhất trong mảng
2. Tìm phần tử nhỏ nhất trong mảng
3. Tính tổng các phần tử trong mảng
4. Đếm số phần tử chẵn trong mảng
5. Sắp xếp mảng tăng dần

**Gợi ý:**
```c
int timMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

int timMin(int arr[], int n) {
    int min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
    }
    return min;
}

int tongMang(int arr[], int n) {
    int tong = 0;
    for (int i = 0; i < n; i++) {
        tong += arr[i];
    }
    return tong;
}

int demSoChan(int arr[], int n) {
    int dem = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0) {
            dem++;
        }
    }
    return dem;
}

void sapXepTang(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}
```

### Bài tập 6: Hàm với chuỗi (String Functions)
**Keywords**: String Processing, String Manipulation, Character Array, Null Terminator
Viết các hàm:
1. Tính độ dài chuỗi
2. Đảo ngược chuỗi
3. Kiểm tra chuỗi đối xứng
4. Đếm số từ trong chuỗi
5. Chuyển đổi chuỗi thành chữ hoa

**Gợi ý:**
```c
int doDaiChuoi(char str[]) {
    int i = 0;
    while (str[i] != '\0') {
        i++;
    }
    return i;
}

void daoNguocChuoi(char str[]) {
    int len = doDaiChuoi(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - 1 - i];
        str[len - 1 - i] = temp;
    }
}

int kiemTraChuoiDoiXung(char str[]) {
    int len = doDaiChuoi(str);
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - 1 - i]) {
            return 0;
        }
    }
    return 1;
}

int demSoTu(char str[]) {
    int dem = 0;
    int i = 0;
    while (str[i] != '\0') {
        if (str[i] != ' ' && (str[i + 1] == ' ' || str[i + 1] == '\0')) {
            dem++;
        }
        i++;
    }
    return dem;
}

void chuyenThanhHoa(char str[]) {
    int i = 0;
    while (str[i] != '\0') {
        if (str[i] >= 'a' && str[i] <= 'z') {
            str[i] = str[i] - 32;
        }
        i++;
    }
}
```

## 10. Bài tập tổng hợp (Comprehensive Exercises)
**Keywords**: Complex Applications, Real-world Problems, System Design

### Bài tập 7: Chương trình quản lý sinh viên (Student Management System)
**Keywords**: Structure, Data Management, Grade Calculation, Classification
Viết chương trình với các hàm:
1. Nhập thông tin sinh viên
2. Tính điểm trung bình
3. Xếp loại học lực
4. In thông tin sinh viên
5. Tìm sinh viên có điểm cao nhất

**Gợi ý:**
```c
#include <stdio.h>
#include <string.h>

struct SinhVien {
    char hoTen[50];
    float diemToan, diemLy, diemHoa;
    float diemTB;
    char xepLoai[20];
};

void nhapSinhVien(struct SinhVien *sv) {
    printf("Nhap ho ten: ");
    fflush(stdin);
    gets(sv->hoTen);
    
    printf("Nhap diem toan: ");
    scanf("%f", &sv->diemToan);
    
    printf("Nhap diem ly: ");
    scanf("%f", &sv->diemLy);
    
    printf("Nhap diem hoa: ");
    scanf("%f", &sv->diemHoa);
}

float tinhDiemTB(struct SinhVien sv) {
    return (sv.diemToan + sv.diemLy + sv.diemHoa) / 3.0;
}

void xepLoaiHocLuc(struct SinhVien *sv) {
    if (sv->diemTB >= 8.0) {
        strcpy(sv->xepLoai, "Gioi");
    } else if (sv->diemTB >= 6.5) {
        strcpy(sv->xepLoai, "Kha");
    } else if (sv->diemTB >= 5.0) {
        strcpy(sv->xepLoai, "Trung binh");
    } else {
        strcpy(sv->xepLoai, "Yeu");
    }
}

void inSinhVien(struct SinhVien sv) {
    printf("Ho ten: %s\n", sv.hoTen);
    printf("Diem toan: %.2f\n", sv.diemToan);
    printf("Diem ly: %.2f\n", sv.diemLy);
    printf("Diem hoa: %.2f\n", sv.diemHoa);
    printf("Diem trung binh: %.2f\n", sv.diemTB);
    printf("Xep loai: %s\n", sv.xepLoai);
}

int main() {
    struct SinhVien sv;
    
    nhapSinhVien(&sv);
    sv.diemTB = tinhDiemTB(sv);
    xepLoaiHocLuc(&sv);
    inSinhVien(sv);
    
    return 0;
}
```

### Bài tập 8: Máy tính đơn giản (Simple Calculator)
**Keywords**: Menu-driven Program, User Interface, Switch Statement, Error Handling
Viết chương trình máy tính với các hàm:
1. Cộng, trừ, nhân, chia
2. Tính lũy thừa
3. Tính căn bậc hai
4. Menu lựa chọn

**Gợi ý:**
```c
#include <stdio.h>
#include <math.h>

float cong(float a, float b) {
    return a + b;
}

float tru(float a, float b) {
    return a - b;
}

float nhan(float a, float b) {
    return a * b;
}

float chia(float a, float b) {
    if (b == 0) {
        printf("Khong the chia cho 0!\n");
        return 0;
    }
    return a / b;
}

float luyThua(float a, float b) {
    return pow(a, b);
}

float canBacHai(float a) {
    if (a < 0) {
        printf("Khong the tinh can bac hai cua so am!\n");
        return 0;
    }
    return sqrt(a);
}

void menu() {
    printf("\n=== MAY TINH DON GIAN ===\n");
    printf("1. Cong\n");
    printf("2. Tru\n");
    printf("3. Nhan\n");
    printf("4. Chia\n");
    printf("5. Luy thua\n");
    printf("6. Can bac hai\n");
    printf("0. Thoat\n");
    printf("Chon: ");
}

int main() {
    int chon;
    float a, b, ketQua;
    
    do {
        menu();
        scanf("%d", &chon);
        
        switch (chon) {
            case 1:
                printf("Nhap hai so: ");
                scanf("%f %f", &a, &b);
                ketQua = cong(a, b);
                printf("%.2f + %.2f = %.2f\n", a, b, ketQua);
                break;
            case 2:
                printf("Nhap hai so: ");
                scanf("%f %f", &a, &b);
                ketQua = tru(a, b);
                printf("%.2f - %.2f = %.2f\n", a, b, ketQua);
                break;
            case 3:
                printf("Nhap hai so: ");
                scanf("%f %f", &a, &b);
                ketQua = nhan(a, b);
                printf("%.2f * %.2f = %.2f\n", a, b, ketQua);
                break;
            case 4:
                printf("Nhap hai so: ");
                scanf("%f %f", &a, &b);
                ketQua = chia(a, b);
                if (b != 0) {
                    printf("%.2f / %.2f = %.2f\n", a, b, ketQua);
                }
                break;
            case 5:
                printf("Nhap co so va so mu: ");
                scanf("%f %f", &a, &b);
                ketQua = luyThua(a, b);
                printf("%.2f ^ %.2f = %.2f\n", a, b, ketQua);
                break;
            case 6:
                printf("Nhap so: ");
                scanf("%f", &a);
                ketQua = canBacHai(a);
                if (a >= 0) {
                    printf("Can bac hai cua %.2f = %.2f\n", a, ketQua);
                }
                break;
            case 0:
                printf("Cam on ban da su dung!\n");
                break;
            default:
                printf("Lua chon khong hop le!\n");
        }
    } while (chon != 0);
    
    return 0;
}
```

## 11. Lưu ý quan trọng (Important Notes)
**Keywords**: Best Practices, Common Mistakes, Debugging Techniques

### 11.1 Lỗi thường gặp (Common Errors)
**Keywords**: Compilation Error, Runtime Error, Logic Error, Syntax Error
1. **Quên khai báo prototype**: Phải khai báo hàm trước khi sử dụng
2. **Không khớp kiểu dữ liệu**: Tham số và giá trị trả về phải đúng kiểu
3. **Quên return**: Hàm có kiểu trả về phải có return
4. **Truyền sai tham số**: Số lượng và kiểu tham số phải khớp
5. **Biến cục bộ không được khởi tạo**: Luôn khởi tạo giá trị cho biến

### 11.2 Best Practices (Thực hành tốt)
**Keywords**: Code Quality, Naming Convention, Single Responsibility Principle, Documentation
1. **Đặt tên hàm có ý nghĩa**: `tinhTong`, `kiemTraSoNguyenTo`
2. **Hàm nên làm một việc**: Mỗi hàm chỉ nên có một nhiệm vụ
3. **Kiểm tra điều kiện**: Luôn kiểm tra điều kiện hợp lệ
4. **Sử dụng const**: Với tham số không thay đổi
5. **Comment code**: Giải thích logic phức tạp

### 11.3 Debugging (Gỡ lỗi)
**Keywords**: Debugging Tools, Print Statements, Breakpoints, Error Tracing
1. **Sử dụng printf**: In giá trị để kiểm tra
2. **Kiểm tra điều kiện dừng**: Với hàm đệ quy
3. **Kiểm tra biến toàn cục**: Tránh xung đột
4. **Test với nhiều trường hợp**: Edge cases

## 12. Kết luận (Conclusion)
**Keywords**: Summary, Key Concepts, Learning Outcomes, Next Steps

Hàm là một khái niệm cơ bản và quan trọng trong lập trình C. Việc sử dụng hàm hiệu quả sẽ giúp:
- Code dễ đọc và bảo trì
- Tái sử dụng mã
- Chia nhỏ bài toán phức tạp
- Debug dễ dàng hơ n


