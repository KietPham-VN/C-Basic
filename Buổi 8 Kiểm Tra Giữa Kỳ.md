# Bài Tập Lập Trình C

---

## bài 1

- viết chương trình cho phép người dùng nhập vào 1 mảng
- và in ra mảng vừa nhập
ví dụ:

```console
Nhập vào kích thước của mảng: 5
Array[0] = 4
Array[1] = 5
Array[2] = 6
Array[3] = 2
Array[4] = 4
Mảng bạn vừa nhập là 4, 5, 6, 2, 4
```

---

## bài 2

- Nhập mảng từ người dùng.
- In ra số lượng phần tử chẵn và số lượng phần tử lẻ.

```console
Nhập vào kích thước của mảng: 6
Array[0] = 1
Array[1] = 4
Array[2] = 6
Array[3] = 3
Array[4] = 7
Array[5] = 2
Mảng bạn vừa nhập là 1, 4, 6, 3, 7, 2
Số phần tử chẵn: 3  
Số phần tử lẻ: 3
```

## bài 3

- Nhập mảng từ người dùng.
- In ra mảng đảo ngược của mảng vừa nhập.

Nhập vào kích thước của mảng: 5
Array[0] = 10
Array[1] = 20
Array[2] = 30
Array[3] = 40
Array[4] = 50
Mảng vừa nhập là : 10, 20, 30, 40, 50
Mảng đảo ngược là: 50, 40, 30, 20, 10

## Bài 4

- Nhập mảng từ người dùng.
- Nhập k và giá trị `x`, chèn `x` vào vị trí `k`.

```console
Nhập vào kích thước của mảng: 4
Array[0] = 1
Array[1] = 2
Array[2] = 3
Array[3] = 4
Mảng vừa nhập là : 1, 2, 3, 4
Nhập vị trí cần chèn: 2
Nhập giá trị cần chèn: 99
Mảng sau khi chèn: 1, 2, 99, 3, 4
```

## Bài 5

Cho phép người dùng nhập hai mảng, rồi gộp lại thành một mảng duy nhất.

```console
Nhập kích thước mảng A: 3
A[0] = 1
A[1] = 3
A[2] = 5
Nhập kích thước mảng B: 3
B[0] = 2
B[1] = 4
B[2] = 6
Mảng sau khi gộp là: 1, 3, 5, 2, 4, 6
```

## Bài 6

- Viết chương trình cho phép người dùng nhập vào hai mảng số nguyên:
  - Mảng A (mảng cha)
  - Mảng B (mảng con)
- Kiểm tra xem mảng B có xuất hiện trong mảng A hay không (theo thứ tự liên tiếp).

Nếu có, in ra vị trí đầu tiên mảng B xuất hiện trong A.
Nếu không, in ra thông báo “Không tìm thấy”

```console
Nhập kích thước mảng A: 8
A[0] = 1
A[1] = 2
A[2] = 3
A[3] = 4
A[4] = 5
A[5] = 6
A[6] = 7
A[7] = 8

Nhập kích thước mảng B: 3
B[0] = 4
B[1] = 5
B[2] = 6

Mảng B xuất hiện trong mảng A tại vị trí bắt đầu: 3
```

## 7. Tìm phần tử lớn thứ hai  

**Cho:** Mảng số nguyên `arr` có `n` phần tử.  
**Yêu cầu:** Viết hàm tìm phần tử lớn thứ hai trong mảng (n >= 2). Không dùng hàm thư viện.  
**Đầu vào:** `int arr[]`, `int n`  
**Đầu ra:** Phần tử lớn thứ hai.

**Ví dụ:**  

```console
Input: arr = [3, 7, 1, 9], n = 4
Output: 7
```
