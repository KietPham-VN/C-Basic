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

## Bài 8: Đếm số lượng dãy con liên tiếp có tổng lớn hơn hoặc bằng K

**Đề bài:**
Cho mảng số nguyên `A[N]` gồm N phần tử và số nguyên `K`.
Hãy đếm có bao nhiêu đoạn con liên tiếp (subarray) mà tổng các phần tử trong đoạn đó lớn hơn hoặc bằng K.

**Input:**

```console
N = 5, K = 5
A = [1, 2, 3, 4, 5]
```

**Output:**

```console
6
```

**Giải thích:**
Các đoạn con thỏa mãn:

- [1, 2, 3] → tổng = 6
- [2, 3] → tổng = 5
- [2, 3, 4] → tổng = 9
- [2, 3, 4, 5] → tổng = 14
- [3, 4] → tổng = 7
- [3, 4, 5] → tổng = 12
- [4, 5] → tổng = 9
- [5] → tổng = 5
- [1, 2, 3, 4] → tổng = 10
- [1, 2, 3, 4, 5] → tổng = 15

---

## Bài 9: Đảo dấu các phần tử để tạo ra nhiều số dương liên tiếp nhất (K lần đổi)

**Đề bài:**
Cho một mảng gồm các số 0 và 1. Bạn được phép đảo tối đa `K` số 0 thành 1.
Tìm độ dài lớn nhất của một đoạn liên tiếp toàn số 1 sau khi thực hiện tối đa `K` lần đổi.

**Input:**

```console
N = 10, K = 2
A = [1,0,0,1,1,0,1,0,1,1]
```

**Output:**

```console
7
```

**Giải thích:**
Đổi hai số 0 ở vị trí 5 và 7 (tính từ 0) thành 1, ta được một đoạn liên tiếp gồm 6 số 1: `[1,1,1,1,1,1]` từ vị trí 3 đến 8.

---

## Bài 10: Tìm tổng lớn nhất của đoạn con liên tiếp có đúng K phần tử

**Đề bài:**
Cho mảng `A[N]` và số nguyên `K`.
Tìm tổng lớn nhất trong mọi đoạn liên tiếp có đúng K phần tử.

**Input:**

```console
N = 6, K = 3
A = [3, -2, 5, 1, 2, 4]
```

**Output:**

```console
8
```

**Giải thích:**
Các tổng đoạn con dài 3:

- [3, -2, 5] = 6
- [-2, 5, 1] = 4
- [5, 1, 2] = 8
- [1, 2, 4] = 7
Tổng lớn nhất là 8 tại đoạn [5, 1, 2].

---
<!--
## Bài 4: Tìm đoạn con liên tiếp dài nhất sao cho tổng không vượt quá K

**Đề bài:**
Cho mảng `A[N]` và số nguyên `K`.
Tìm độ dài lớn nhất của đoạn liên tiếp có tổng không vượt quá K.

**Input:**

```
N = 7, K = 8
A = [1, 2, 3, 1, 1, 1, 2]
```

**Output:**

```
5
```

**Giải thích:**
Đoạn `[3, 1, 1, 1, 2]` có tổng là 8, dài 5 là lớn nhất thỏa mãn.

---

## Bài 5: Xóa phần tử trùng lặp trong mảng đã sắp xếp

**Đề bài:**
Cho một mảng số nguyên đã được sắp xếp không giảm (có thể có phần tử trùng lặp).
Hãy xóa các phần tử trùng lặp sao cho mỗi phần tử chỉ xuất hiện một lần.
Lưu ý: Thực hiện trực tiếp trên mảng, không dùng mảng phụ.

**Input:**

```
N = 8
A = [1, 1, 2, 2, 2, 3, 4, 4]
```

**Output:**

```
Số lượng phần tử còn lại: 4
Mảng sau khi xóa trùng lặp: 1 2 3 4
```

**Giải thích:**
Chỉ giữ lại mỗi số xuất hiện một lần, và theo thứ tự ban đầu. -->
