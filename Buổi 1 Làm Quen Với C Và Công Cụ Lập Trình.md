# Buổi 1: Làm Quen Với C Và Công Cụ Lập Trình

1. Hiểu khái niệm IDE và Text Editor.
2. Cài đặt Dev-C++ và chạy chương trình C đầu tiên.
3. Làm quen với biến, kiểu dữ liệu, printf/scanf.
4. Hiểu quá trình biên dịch code thành chương trình chạy được.

> tải IDE dev c

## 1. IDE và Text Editor

- có 2 khái niệm mà ta thường hay nhầm lẫn đó là IDE và text editor. - text editor đơn giản là 1 công cụ soạn thảo văn bản thường bắt gặp là word, notepad, vscode.
  - IDE(Integrated Development Environment): là text editor nhưng chuyên biệt hơn cho việc viết code có tích hợp các công cụ mà một lập trình viên cần biên dịch code, debugging tool, …
    > Dev-C++ là 1 cái IDE dành riêng cho việt viết code C/C++

## 2. Biến(variable)

- là nơi mà chúng ta lưu trữ dữ liệu.
- syntax: `<datatype> <name> = <initial value>` - **data type** là kiểu dữ liệu là cách mà chúng ta nói cho máy tính biết rằng cái biến này lưu loại dữ liệu gì trong đó. - các kiểu dữ liệu thường gặp là: - int: integer : lưu số nguyên 4 byte - char: character : lưu 1 ký tự 1 byte - float: floating point: lưu số thực 4 byte - ngoài ra có nhiều lắm có thể tham khảo trên mạng thêm hoặc là trong này

| Loại dữ liệu  | Từ khóa | Tên tiếng Anh  | Kích thước | Ví dụ         | Ghi chú                        |
| ------------- | ------- | -------------- | ---------- | ------------- | ------------------------------ |
| Ký tự         | char    | character      | 1 byte     | 'a', '2'      | Lưu 1 ký tự (trong '')         |
| Số nguyên     | int     | integer        | 4 byte     | 9, 1999       | Không lưu phần thập phân       |
| Số nguyên nhỏ | short   | short integer  | 2 byte     | 5, \-200      | Dùng khi cần tiết kiệm bộ nhớ  |
| Số nguyên lớn | long    | long integer   | 8 byte     | 1000000       | Lưu số nguyên lớn hơn          |
| Số thực       | float   | floating-point | 4 byte     | 17.9          | Độ chính xác đơn (\~7 chữ số)  |
| Số thực lớn   | double  | double float   | 8 byte     | 17.9, 1.2e+18 | Độ chính xác gấp đôi (\~15 số) |


  - **tên biến**
    - thì đặt theo cú pháp con lạc đà (camelCase) tức là viết hoa chữ cái đầu tiên của mỗi từ kể từ từ thứ 2 trở đi
    - không được bắt đầu bằng số
    - không được chứa ký tự đặc biệt
    - không được trùng với từ khóa của ngôn ngữ
    - không được trùng với tên hàm
    - không được trùng với tên biến đã có
    - ví dụ: firstName, lastName, fullName, …

- **giá trị khởi tạo** là cái giá trị mặc định lúc mình tạo biến biến tên tiếng anh là variable dịch ra là có thể thay đổi thì giá trị của biến cũng có thể thay đổi.
  - còn nếu mà 1 biến với giá trị không đổi thì gọi là hằng số trong toán học pi, e, ... là các hằng số.
  - nếu ta tạo biến mà không gán giá trị thì sao, trả lời đối với những cái trình biên dịch cũ thì nó có thể chứa rác.
  - nhưng đối với các trình biên dịch hiện đại thì nó sẽ chứa default của kiểu dữ liệu mà nó
  - trình biên dịch là cái dịch code của mình ra thành các số 0 và 1 để máy hiểu và thực thi được khai báo
    - int: 0
    - float: 0.000000
    - char: thì nó sẽ in ra ký tự lạ

> **làm nhẹ bài swap string và number1**

```c
  int sting = 15;
  int number1 = 20;
  int tmp = 0;

  tmp = sting;
  sting = number1;
  number1 = tmp;
  // cách không cần biến phụ

  number1 = number1 + sting; // number1 = 35
  sting = number1 - sting; // 35 - 20 = 15
  number1 = number1 - sting; // 35 - 15 = 20
```

> còn 1 cách nữa là dùng toán tử bitwise các em về nhà tìm hiểu nhá

**_giờ mình có biến rồi thì mình in ra nó như thế nào?_**

mình sẽ dùng câu lệnh `printf`  
tới lúc này các bạn sẽ hỏi của cái %d là gì  
trả lời  
Chúng là các

## 3\. “format specifiers” (chỉ thị định dạng), cụ thể là “conversion specifiers”

`%d` → In số nguyên (int) có dấu  
`%i` → Tương tự %d  
`%u` → In số nguyên không dấu (unsigned int)  
`%ld` → In số nguyên lớn (long int)  
`%lld` → In số nguyên rất lớn (long long int)

`%f` → In số thực float/double (6 số sau dấu . mặc định)  
`%.2f` → In số thực với 2 số thập phân  
`%e` → In số thực dạng khoa học (exponential)  
`%lf` → In double (thực ra %f và %lf đều dùng được với printf)

`%c` → In ký tự (char)  
`%s` → In chuỗi (char array hoặc con trỏ char)

`%p` → In địa chỉ bộ nhớ (pointer), cần ép về (void\*)

`%%` → In dấu %

tới đây a có 1 câu hỏi ví dụ

```c
int main() {
  char a \= 122;
  printf("\nGiá trị của a: %c", a);
  return 0;
}
```

mấy em có thể đoán được là in ra màn hình là gì ko  
rồi tới để giải thích hiện tượng trên  
anh giới thiệu tới mấy em bảng mã ASCII

## 4\. ASCII (American Standard Code for Information Interchange) là bảng mã ký tự chuẩn được dùng để biểu diễn

chữ cái, chữ số, ký hiệu và các ký tự điều khiển trong máy tính.  
A-z: 65-90  
a-z: 97-122  
\n: 10  
space: 32  
chèn thêm bảng mã ascii vô

hiểu được nhiêu đây là mình đã có thể viết chương trình in ra 1 cái biến rối  
nhưng để gán giá trị cho 1 biến thì cần có thể 1 xíu gia vị nữa

khi ta nói về 1 biến thì có 2 cái mà ta cần quan tâm

- giá trị: cái mà biến nó lưu
- địa chỉ: vị trí mà cái biến nó nằm trên thanh ram

```c

int main() {
  SetConsoleOutputCP(65001);
  int yearOfBirth = 2005;
  printf("\nGiá trị của a: %d", yearOfBirth); // giá trị truy cập bằng tên
  printf("\nĐịa chỉ của biến a: %d", &yearOfBirth); // địa chỉ thì thêm dấu &
  return 0;
}
```

- giải thích về hàm main  
  **- viết chương trình đơn giản tính chu vi tam giác**

```c
int main() {
  SetConsoleOutputCP(65001);
  float a, b, c;
  printf("\n Nhập giá trị cho a: ");
  scanf("%f", &a);

  printf("\n Nhập giá trị cho b: ");
  scanf("%f", &b);

  printf("\n Nhập giá trị cho c: ");
  scanf("%f", &c);

  printf("\n Chu vi tam giác trên là: %.2f", a + b + c):
 return 0;
}
```

**_viết chương trình biến chữ thường thành chữ hoa_**

```c
int main() {
    char ch;
    printf("Nhap ky tu: ");
    scanf("%c", &ch);

    printf("Chu hoa: %c\n", ch - 32);

    return 0;
}
```

- giải thích về scanf
- rồi muốn chương trình của mình xịn hơn thì bài sau anh sẽ nói về if-else

## 5\. Toán tử (Operator)

- Số học (Arithmetic): \+ \- \* / %
- Tăng/giảm (Increment/Decrement) \++, \- \-
- So sánh (Relational): \== \!= \< \> \<= \>=
- Logic (Logical) || && \!
- Gán (Assignment) \+= \-= \*= /= %=
- Bitwise & | \>\> \<\< ^ \~

## 6\. bonus

- lưu ý để code không lỗi
  - đường dẫn không tiếng việt
  - không onedrive, gg drive, ...
  - trình biên dịch dịch thành mã nhị phân như thế nào

1. Preprocessing (Tiền xử lý)
   - Nó đọc code C của bạn (main.c), thực hiện:
   - Chèn code từ file header (`#include <stdio.h>` → lấy nội dung từ stdio.h nhét vào)
   - Xóa comment // hoặc /\* \*/
   - Kết quả: tạo file mã nguồn tạm thời (ví dụ main.i) chỉ còn code thuần C, không có chỉ thị `#include`.
2. Compilation (Biên dịch sang Assembly)
   - Đọc file .i và dịch thành mã Assembly cho CPU của bạn.
   - Kết quả: file main.s (mã Assembly).
3. Assembling (Dịch Assembly thành Mã Máy)
   - Dịch file .s thành mã máy nhị phân mà CPU hiểu được.
   - Kết quả: file object file (main.o)
4. Linking (Liên kết thành file .exe)
   - Ghép main.o với các thư viện .lib hoặc .a (ví dụ libc.a chứa printf)
   - Sắp xếp và tạo entry point (điểm bắt đầu chương trình)
   - Thêm header định dạng .exe (Portable Executable) cho Windows.
   - Kết quả: main.exe chạy được trên Windows.  
     => TA CÓ THỂ THẤY ĐƯỢC LÀ IDE XỊN NÓ LÀM TẤT CẢ CÁC BƯỚC TRÊN TRONG 1 NÚT BẤM
