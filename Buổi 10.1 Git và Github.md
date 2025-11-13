# Hướng dẫn Git từ A-Z cho người mới bắt đầu

## Mục lục

1. [Git là gì?](#git-là-gì)
2. [Tại sao cần học Git?](#tại-sao-cần-học-git)
3. [Cài đặt Git](#cài-đặt-git)
4. [Cấu hình Git lần đầu](#cấu-hình-git-lần-đầu)
5. [Khái niệm cơ bản](#khái-niệm-cơ-bản)
6. [Các lệnh Git cơ bản](#các-lệnh-git-cơ-bản)
7. [Làm việc với GitHub](#làm-việc-với-github)
8. [Git Branching](#git-branching)
9. [Xử lý xung đột](#xử-lý-xung-đột)
10. [Các lệnh nâng cao](#các-lệnh-nâng-cao)
11. [Best Practices](#best-practices)
12. [Troubleshooting](#troubleshooting)

---

## Git là gì?

**Git** là một hệ thống quản lý phiên bản phân tán (Distributed Version Control System - DVCS) được tạo ra bởi Linus Torvalds năm 2005.

### Giải thích đơn giản

Hãy tưởng tượng bạn đang viết một bài luận văn:

- **Không có Git**: Bạn tạo nhiều file: `luan_van_v1.docx`, `luan_van_v2.docx`, `luan_van_final.docx`, `luan_van_final_final.docx`... rối rắm và khó quản lý.
- **Có Git**: Bạn chỉ có 1 file `luan_van.docx`, nhưng Git ghi nhớ MỌI thay đổi bạn đã làm, bạn có thể xem lại, so sánh, hoặc quay về bất kỳ phiên bản nào.

### Git giúp bạn

- 📝 Lưu lại lịch sử thay đổi của dự án
- 👥 Làm việc nhóm mà không ghi đè code của nhau
- 🔄 Quay về phiên bản cũ khi cần
- 🌿 Thử nghiệm tính năng mới mà không ảnh hưởng code chính
- 🔍 Tìm ra ai đã thay đổi đoạn code nào, khi nào

---

## Tại sao cần học Git?

### 1. Công việc lập trình chuyên nghiệp

- 99% công ty công nghệ sử dụng Git
- Là yêu cầu bắt buộc trong mọi vị trí lập trình viên

### 2. Làm việc nhóm hiệu quả

- Nhiều người cùng code một dự án mà không xung đột
- Review code của nhau dễ dàng
- Theo dõi ai làm gì, khi nào

### 3. Backup an toàn

- Code được lưu trữ ở nhiều nơi (local + remote)
- Không lo mất code khi máy hỏng

### 4. Thử nghiệm tự do

- Tạo branch riêng để thử tính năng mới
- Nếu hỏng, chỉ cần xóa branch, code chính vẫn nguyên

---

## Cài đặt Git

### Windows

1. Tải Git từ: <https://git-scm.com/download/win>
2. Chạy file cài đặt (`.exe`)
3. Nhấn "Next" cho đến khi xong (dùng cấu hình mặc định)
4. Kiểm tra: Mở **Git Bash** hoặc **CMD** và gõ:

```bash
git --version
```

### macOS

```bash
# Cách 1: Cài qua Homebrew (nên dùng)
brew install git

# Cách 2: Cài qua Xcode Command Line Tools
xcode-select --install
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git
```

### Linux (Fedora)

```bash
sudo dnf install git
```

---

## Cấu hình Git lần đầu

Sau khi cài đặt, bạn cần "giới thiệu bản thân" với Git:

```bash
# Đặt tên của bạn
git config --global user.name "Nguyen Van A"

# Đặt email của bạn
git config --global user.email "nguyenvana@email.com"

# Kiểm tra cấu hình
git config --list
```

**Lưu ý**: Email này nên trùng với email bạn dùng trên GitHub/GitLab.

### Cấu hình thêm (tùy chọn)

```bash
# Đặt editor mặc định (ví dụ: Visual Studio Code)
git config --global core.editor "code --wait"

# Hiển thị màu sắc trong terminal
git config --global color.ui auto

# Đặt branch mặc định là 'main' thay vì 'master'
git config --global init.defaultBranch main
```

---

## Khái niệm cơ bản

### 1. Repository (Repo)

- **Định nghĩa**: Kho lưu trữ dự án, chứa toàn bộ code và lịch sử thay đổi
- **Ví dụ**: Thư mục dự án của bạn sau khi chạy `git init`

### 2. Working Directory

- **Định nghĩa**: Thư mục hiện tại bạn đang làm việc
- **Ví dụ**: Nơi bạn tạo, sửa, xóa file

### 3. Staging Area (Index)

- **Định nghĩa**: Khu vực trung gian trước khi commit
- **Ví dụ**: Giỏ hàng trước khi thanh toán - bạn chọn những thay đổi nào sẽ được commit

### 4. Commit

- **Định nghĩa**: Một "ảnh chụp" (snapshot) trạng thái dự án tại một thời điểm
- **Ví dụ**: Như điểm save game - bạn có thể quay lại bất cứ lúc nào

### 5. Branch

- **Định nghĩa**: Nhánh phát triển độc lập
- **Ví dụ**: Như vũ trụ song song - bạn thử nghiệm ở branch khác mà không ảnh hưởng branch chính

### 6. Remote

- **Định nghĩa**: Phiên bản repository được lưu trữ trên server (GitHub, GitLab...)
- **Ví dụ**: Bản backup online của dự án

### Sơ đồ luồng làm việc

```text
Working Directory → Staging Area → Local Repository → Remote Repository
    (git add)         (git commit)      (git push)
```

---

## Các lệnh Git cơ bản

### 1. Khởi tạo Repository

#### Tạo repo mới từ thư mục hiện tại

```bash
# Di chuyển vào thư mục dự án
cd /duong-dan/den/du-an

# Khởi tạo Git
git init
```

**Giải thích**: Tạo thư mục ẩn `.git` để Git theo dõi thay đổi.

#### Clone repo có sẵn

```bash
git clone https://github.com/username/repository.git
```

**Giải thích**: Tải về toàn bộ dự án từ GitHub về máy.

---

### 2. Kiểm tra trạng thái

```bash
git status
```

**Kết quả có thể thấy**:

- File nào đã thay đổi
- File nào đã được add vào staging
- File nào chưa được theo dõi

**Ví dụ output**:

```text
On branch main
Changes not staged for commit:
  modified:   index.html

Untracked files:
  style.css
```

---

### 3. Thêm file vào Staging Area

```bash
# Thêm một file cụ thể
git add index.html

# Thêm tất cả file đã thay đổi
git add .

# Thêm tất cả file có đuôi .js
git add *.js

# Thêm toàn bộ thư mục
git add src/
```

---

### 4. Commit thay đổi

```bash
# Commit với message
git commit -m "Thêm tính năng đăng nhập"

# Commit và add cùng lúc (chỉ cho file đã tracked)
git commit -am "Sửa lỗi hiển thị"
```

**Lưu ý về commit message**:

- ✅ Tốt: "Thêm validation cho form đăng ký"
- ✅ Tốt: "Sửa lỗi crash khi click button Submit"
- ❌ Tránh: "update", "fix bug", "abc"

---

### 5. Xem lịch sử commit

```bash
# Xem lịch sử đầy đủ
git log

# Xem lịch sử gọn gàng (1 dòng/commit)
git log --oneline

# Xem lịch sử với đồ thị branch
git log --oneline --graph --all

# Xem 5 commit gần nhất
git log -5

# Xem commit của một người cụ thể
git log --author="Nguyen Van A"

# Xem thay đổi trong mỗi commit
git log -p
```

---

### 6. Xem thay đổi

```bash
# Xem thay đổi chưa add
git diff

# Xem thay đổi đã add nhưng chưa commit
git diff --staged

# Xem thay đổi của một file cụ thể
git diff index.html

# So sánh giữa 2 commit
git diff commit1 commit2
```

---

### 7. Loại bỏ thay đổi

```bash
# Loại bỏ thay đổi chưa add (nguy hiểm - mất vĩnh viễn!)
git checkout -- index.html

# Bỏ file ra khỏi staging area (giữ nguyên thay đổi)
git reset index.html

# Quay về commit trước, giữ thay đổi
git reset --soft HEAD~1

# Quay về commit trước, xóa thay đổi (nguy hiểm!)
git reset --hard HEAD~1
```

**Chú ý**: `--hard` sẽ XÓA thay đổi vĩnh viễn!

---

### 8. Bỏ qua file với .gitignore

Tạo file `.gitignore` trong thư mục gốc:

```text
# Bỏ qua file môi trường
.env
.env.local

# Bỏ qua thư mục node_modules
node_modules/

# Bỏ qua tất cả file .log
*.log

# Bỏ qua thư mục build
build/
dist/

# Bỏ qua file cấu hình IDE
.vscode/
.idea/

# Bỏ qua file hệ thống
.DS_Store
Thumbs.db
```

---

## Làm việc với GitHub

### 1. Tạo repository trên GitHub

1. Vào <https://github.com> và đăng nhập
2. Click nút **"New repository"**
3. Đặt tên, chọn Public/Private
4. Click **"Create repository"**

### 2. Kết nối Local với Remote

```bash
# Thêm remote (thường đặt tên là 'origin')
git remote add origin https://github.com/username/repository.git

# Xem danh sách remote
git remote -v

# Đổi tên remote
git remote rename origin upstream

# Xóa remote
git remote remove origin
```

### 3. Push code lên GitHub

```bash
# Push lần đầu
git push -u origin main

# Push lần sau (đã có upstream)
git push

# Push một branch cụ thể
git push origin feature-login

# Push tất cả branch
git push --all

# Push kèm tags
git push --tags
```

**Giải thích `-u`**: Thiết lập tracking, lần sau chỉ cần `git push`

### 4. Pull code từ GitHub

```bash
# Pull từ remote (fetch + merge)
git pull

# Pull từ branch cụ thể
git pull origin main

# Pull với rebase (giữ lịch sử gọn gàng)
git pull --rebase
```

### 5. Fetch vs Pull

```bash
# Fetch: Tải về thông tin mới nhất nhưng KHÔNG merge
git fetch

# Xem thay đổi trước khi merge
git log origin/main

# Merge thủ công sau khi fetch
git merge origin/main
```

**Khác biệt**:

- `fetch`: Tải về + xem trước
- `pull`: Tải về + merge luôn

---

## Git Branching

### 1. Tại sao cần Branch?

- Phát triển tính năng mới mà không ảnh hưởng code chính
- Sửa bug khẩn cấp trong khi vẫn đang làm tính năng dang dở
- Mỗi người một branch, không xung đột

### 2. Các lệnh Branch cơ bản

```bash
# Xem danh sách branch
git branch

# Xem tất cả branch (kể cả remote)
git branch -a

# Tạo branch mới
git branch feature-login

# Chuyển sang branch khác
git checkout feature-login

# Tạo và chuyển sang branch mới (gộp 2 lệnh trên)
git checkout -b feature-register

# Tạo branch từ một commit cụ thể
git checkout -b bugfix abc1234

# Đổi tên branch hiện tại
git branch -m new-name

# Xóa branch (đã merge)
git branch -d feature-login

# Xóa branch (chưa merge - ép buộc)
git branch -D feature-login

# Xóa branch remote
git push origin --delete feature-login
```

### 3. Merge Branch

```bash
# Chuyển về branch đích (thường là main)
git checkout main

# Merge branch khác vào
git merge feature-login
```

**Các kiểu merge**:

#### Fast-forward merge (không có xung đột)

```text
main:     A - B - C
                   \
feature:            D - E

Sau merge:
main:     A - B - C - D - E
```

#### 3-way merge (có diverge)

```text
main:     A - B - C - F
               \
feature:        D - E

Sau merge:
main:     A - B - C - F - G (merge commit)
                   \     /
                    D - E
```

### 4. Rebase (Nâng cao)

```bash
# Rebase branch hiện tại lên main
git checkout feature-login
git rebase main
```

---

## So sánh chi tiết: Merge vs Rebase

### Merge là gì?

**Merge** kết hợp hai branch bằng cách tạo một **merge commit** mới, giữ nguyên lịch sử của cả hai branch.

#### Ví dụ trực quan

**Trước khi merge:**

```text
main:     A --- B --- C --- F
               \
feature:        D --- E
```

**Sau khi merge:**

```text
main:     A --- B --- C --- F --- G (merge commit)
               \             /
feature:        D --------- E
```

#### Lệnh Merge

```bash
git checkout main
git merge feature-branch
```

#### Ưu điểm của Merge

✅ **Giữ nguyên lịch sử**: Biết chính xác khi nào branch được tạo, khi nào merge
✅ **An toàn**: Không thay đổi commit đã có
✅ **Dễ hiểu**: Thấy rõ luồng phát triển song song
✅ **Không lo conflict**: Chỉ giải quyết conflict một lần khi merge
✅ **Phù hợp cho team**: Không ảnh hưởng đến người khác

#### Nhược điểm của Merge

❌ **Lịch sử phức tạp**: Nhiều merge commit làm log khó đọc
❌ **Nhiễu**: Với nhiều branch, git log sẽ rối rắm
❌ **Merge commit "vô nghĩa"**: Commit không chứa code thực sự

---

### Rebase là gì?

**Rebase** di chuyển hoặc "gắn lại" (replay) các commit của branch lên đỉnh của branch khác, tạo lịch sử tuyến tính.

#### Ví dụ

**Trước khi rebase:**

```text
main:     A --- B --- C --- F
               \
feature:        D --- E
```

**Sau khi rebase:**

```text
main:     A --- B --- C --- F
                            \
feature:                     D' --- E'
```

Chú ý: D và E được "viết lại" thành D' và E' (commit mới, hash khác)

#### Lệnh Rebase

```bash
git checkout feature-branch
git rebase main
```

#### Ưu điểm của Rebase

✅ **Lịch sử gọn gàng**: Git log tuyến tính, dễ đọc
✅ **Không có merge commit**: Không tạo commit "vô nghĩa"
✅ **Dễ debug**: Lịch sử đơn giản, dễ tìm bug bằng `git bisect`
✅ **Review dễ hơn**: PR/MR gọn gàng, dễ review

#### Nhược điểm của Rebase

❌ **Nguy hiểm**: Có thể mất commit nếu dùng sai
❌ **Viết lại lịch sử**: Thay đổi commit hash, gây vấn đề nếu đã push
❌ **Conflict nhiều lần**: Phải giải quyết conflict cho từng commit
❌ **Khó hiểu**: Người mới dễ bối rối
❌ **Không phù hợp làm chung**: Nếu nhiều người dùng cùng branch

---

### Bảng so sánh trực quan

| Tiêu chí                  | Merge                      | Rebase                           |
| ------------------------- | -------------------------- | -------------------------------- |
| **Lịch sử**               | Giữ nguyên, phi tuyến tính | Viết lại, tuyến tính             |
| **Commit mới**            | Tạo merge commit           | Không tạo commit mới             |
| **An toàn**               | ✅ Rất an toàn             | ⚠️ Có thể nguy hiểm              |
| **Conflict**              | Giải quyết 1 lần           | Có thể giải quyết nhiều lần      |
| **Git log**               | Phức tạp, nhiều nhánh      | Gọn gàng, thẳng hàng             |
| **Dùng cho code đã push** | ✅ An toàn                 | ❌ Không nên (gây vấn đề)        |
| **Team work**             | ✅ Phù hợp                 | ⚠️ Cần thống nhất                |
| **Trace history**         | ✅ Rõ ràng khi nào merge   | ❌ Mất thông tin thời gian merge |

---

### Khi nào dùng Merge?

✅ **Dùng Merge khi:**

- Làm việc nhóm với nhiều người
- Branch đã được push lên remote
- Muốn giữ lại lịch sử đầy đủ
- Merge branch feature lớn vào main
- Không cần lịch sử tuyến tính
- Team chưa quen với rebase

**Ví dụ:**

```bash
# Merge feature branch vào main
git checkout main
git pull origin main
git merge feature-login
git push origin main
```

---

### Khi nào dùng Rebase?

✅ **Dùng Rebase khi:**

- Làm việc một mình trên branch
- Branch chưa push hoặc chỉ mình bạn dùng
- Muốn lịch sử gọn gàng trước khi tạo PR
- Cập nhật branch feature với thay đổi mới từ main
- Team đã thống nhất dùng rebase workflow

**Ví dụ:**

```bash
# Cập nhật feature branch với main
git checkout feature-login
git rebase main

# Nếu có conflict, giải quyết rồi:
git add .
git rebase --continue

# Nếu muốn hủy rebase:
git rebase --abort
```

---

### Golden Rule of Rebase

> **🚨 KHÔNG BAO GIỜ REBASE COMMIT ĐÃ PUSH LÊN PUBLIC BRANCH**

**Tại sao?**

- Rebase thay đổi commit hash
- Người khác đã pull commit cũ về
- Khi bạn force push, tạo xung đột lớn cho cả team

**Ngoại lệ**: Có thể rebase branch feature của riêng bạn (chưa ai dùng)

```bash
# ❌ ĐỪNG LÀM: Rebase main đã push
git checkout main
git rebase feature  # SAI!

# ✅ NÊN LÀM: Rebase branch riêng của bạn
git checkout my-feature
git rebase main     # OK!
```

---

### Workflow kết hợp Merge và Rebase

**Workflow phổ biến:**

```bash
# 1. Tạo feature branch
git checkout -b feature-login

# 2. Code và commit nhiều lần
git add .
git commit -m "Thêm form login"
git commit -m "Thêm validation"
git commit -m "Fix lỗi typo"

# 3. Trước khi tạo PR: Rebase để cập nhật và gọn lịch sử
git fetch origin
git rebase origin/main

# 4. (Tùy chọn) Squash các commit nhỏ
git rebase -i HEAD~3

# 5. Force push branch của bạn (vì đã rebase)
git push -f origin feature-login

# 6. Tạo Pull Request trên GitHub

# 7. Sau khi approve: MERGE vào main (không rebase)
# Làm trên GitHub UI hoặc:
git checkout main
git pull origin main
git merge feature-login
git push origin main
```

---

### Interactive Rebase (Rebase nâng cao)

Interactive rebase cho phép bạn **chỉnh sửa lịch sử commit**:

```bash
# Rebase 5 commit gần nhất
git rebase -i HEAD~5
```

**Một editor sẽ mở ra:**

```text
pick abc1234 Thêm form login
pick def5678 Thêm validation
pick ghi9012 Fix typo
pick jkl3456 Fix lỗi validation
pick mno7890 Update style

# Commands:
# p, pick = dùng commit
# r, reword = dùng commit nhưng sửa message
# e, edit = dùng commit nhưng dừng để sửa
# s, squash = gộp commit này vào commit trước
# f, fixup = giống squash nhưng bỏ commit message
# d, drop = xóa commit
```

**Ví dụ chỉnh sửa:**

```text
pick abc1234 Thêm form login
squash def5678 Thêm validation
squash ghi9012 Fix typo
pick jkl3456 Fix lỗi validation
fixup mno7890 Update style
```

**Kết quả:** 5 commit → 2 commit gọn gàng

#### Các use case của Interactive Rebase

**1. Gộp nhiều commit nhỏ:**

```bash
git rebase -i HEAD~3
# Đổi 'pick' thành 'squash' cho commit muốn gộp
```

**2. Sửa commit message:**

```bash
git rebase -i HEAD~3
# Đổi 'pick' thành 'reword'
```

**3. Xóa commit không cần:**

```bash
git rebase -i HEAD~3
# Đổi 'pick' thành 'drop' hoặc xóa dòng đó
```

**4. Sắp xếp lại thứ tự commit:**

```bash
git rebase -i HEAD~3
# Đổi thứ tự các dòng
```

**5. Sửa nội dung commit cũ:**

```bash
git rebase -i HEAD~3
# Đổi 'pick' thành 'edit'
# Khi dừng lại: sửa file, git add, git commit --amend
# Sau đó: git rebase --continue
```

---

### Ví dụ thực tế

#### Tình huống 1: Cập nhật feature branch

**Dùng Merge:**

```bash
git checkout feature-login
git merge main
# Tạo merge commit, lịch sử phức tạp
```

**Dùng Rebase:**

```bash
git checkout feature-login
git rebase main
# Lịch sử tuyến tính, gọn gàng
```

#### Tình huống 2: Gộp feature vào main

**Dùng Merge (khuyên dùng):**

```bash
git checkout main
git merge feature-login
# Giữ lịch sử, thấy rõ khi nào merge
```

**Dùng Rebase (có thể):**

```bash
git checkout feature-login
git rebase main
git checkout main
git merge feature-login  # Fast-forward merge
# Lịch sử tuyến tính nhưng mất thông tin branch
```

---

### Tips sử dụng Merge và Rebase

#### Tips cho Merge

```bash
# Merge với --no-ff để luôn tạo merge commit
git merge --no-ff feature-branch

# Xem trước merge mà không thực hiện
git merge --no-commit --no-ff feature-branch
git diff --cached
git merge --abort
```

#### Tips cho Rebase

```bash
# Rebase với autosquash (tự động gộp fixup commits)
git commit --fixup abc1234
git rebase -i --autosquash main

# Bảo toàn merge commits khi rebase
git rebase -r main

# Rebase nhưng dùng strategy của mình khi conflict
git rebase -X ours main    # Ưu tiên code của mình
git rebase -X theirs main  # Ưu tiên code của main
```

---

### Tóm tắt: Nên dùng gì?

**Quy tắc đơn giản:**

1. **Merge** cho:

   - Hợp nhất branch feature → main/develop
   - Làm việc nhóm
   - Code đã public

2. **Rebase** cho:

   - Cập nhật branch cá nhân với main
   - Dọn dẹp lịch sử trước khi tạo PR
   - Làm việc local, chưa push

3. **Cả hai**:
   - Rebase trước để cập nhật
   - Merge cuối cùng vào main

**Workflow đề xuất cho team:**

```text
feature branch: rebase thường xuyên
        ↓
   Pull Request
        ↓
main branch: merge feature (với --no-ff)
```

**Lưu ý**: KHÔNG rebase những commit đã push lên remote (ảnh hưởng đến người khác)

---

## Xử lý xung đột

### Xung đột xảy ra khi nào?

- 2 người sửa cùng dòng code
- Một người xóa file, người kia sửa file đó
- Merge hoặc rebase branch có thay đổi trùng lặp

### Cách xử lý xung đột

#### Bước 1: Git báo có conflict

```bash
git merge feature-branch
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
```

#### Bước 2: Mở file có conflict

```html
<<<<<<< HEAD
<h1>Tiêu đề cũ</h1>
=======
<h1>Tiêu đề mới</h1>
>>>>>>> feature-branch
```

**Giải thích**:

- `<<<<<<< HEAD`: Code ở branch hiện tại
- `=======`: Dấu phân cách
- `>>>>>>> feature-branch`: Code từ branch đang merge

#### Bước 3: Sửa conflict thủ công

```html
<!-- Xóa các dấu <<<, ===, >>> và giữ lại code đúng -->
<h1>Tiêu đề mới đã sửa</h1>
```

#### Bước 4: Add và commit

```bash
git add index.html
git commit -m "Giải quyết xung đột trong index.html"
```

#### Bước 5: Tiếp tục merge/rebase

```bash
# Nếu đang rebase
git rebase --continue

# Nếu muốn hủy merge/rebase
git merge --abort
git rebase --abort
```

### Tips xử lý conflict

- Dùng tool hỗ trợ: VS Code, GitKraken, SourceTree
- Giao tiếp với người gây conflict để hiểu ý đồ
- Test kỹ sau khi giải quyết conflict

---

## Các lệnh nâng cao

### 1. Stash (Cất giữ thay đổi tạm thời)

```bash
# Cất giữ thay đổi hiện tại
git stash

# Cất giữ kèm message
git stash save "Đang làm dở tính năng X"

# Xem danh sách stash
git stash list

# Lấy lại stash gần nhất
git stash pop

# Lấy lại stash cụ thể
git stash apply stash@{0}

# Xóa stash
git stash drop stash@{0}

# Xóa tất cả stash
git stash clear
```

**Khi nào dùng stash?**

- Đang code dở, cần chuyển branch khẩn cấp
- Cần pull code mới nhưng chưa muốn commit code dở

### 2. Cherry-pick (Lấy một commit cụ thể)

```bash
# Lấy commit abc1234 vào branch hiện tại
git cherry-pick abc1234

# Lấy nhiều commit
git cherry-pick abc1234 def5678

# Cherry-pick nhưng không commit luôn
git cherry-pick -n abc1234
```

**Khi nào dùng?**

- Cần hotfix từ branch khác nhưng không muốn merge toàn bộ
- Lấy commit nhầm branch

### 3. Tag (Đánh dấu phiên bản)

```bash
# Tạo tag
git tag v1.0.0

# Tạo tag với message
git tag -a v1.0.0 -m "Phiên bản 1.0.0"

# Tạo tag cho commit cũ
git tag v0.9.0 abc1234

# Xem danh sách tag
git tag

# Xem thông tin tag
git show v1.0.0

# Push tag lên remote
git push origin v1.0.0

# Push tất cả tag
git push --tags

# Xóa tag local
git tag -d v1.0.0

# Xóa tag remote
git push origin --delete v1.0.0
```

### 4. Reflog (Lịch sử mọi thay đổi)

```bash
# Xem reflog
git reflog

# Khôi phục commit đã xóa
git reset --hard HEAD@{2}
```

**Cứu cánh**: Khi bạn nhầm `git reset --hard`, dùng reflog để tìm lại!

### 5. Blame (Tìm người sửa code)

```bash
# Xem ai sửa từng dòng trong file
git blame index.html

# Xem từ dòng 10 đến 20
git blame -L 10,20 index.html
```

### 6. Bisect (Tìm commit gây bug)

```bash
# Bắt đầu bisect
git bisect start

# Đánh dấu commit hiện tại là bad
git bisect bad

# Đánh dấu commit cũ là good
git bisect good abc1234

# Git sẽ checkout commit giữa, bạn test và đánh dấu
git bisect good  # hoặc git bisect bad

# Kết thúc bisect
git bisect reset
```

---

## Best Practices

### 1. Commit thường xuyên

- Commit sau mỗi tính năng nhỏ hoàn thành
- Đừng để commit quá lớn, khó review

### 2. Viết commit message rõ ràng

```bash
# ❌ Tránh
git commit -m "fix"
git commit -m "update code"

# ✅ Nên
git commit -m "Sửa lỗi validation email trong form đăng ký"
git commit -m "Thêm API endpoint để lấy danh sách sản phẩm"
```

**Format commit message phổ biến**:

```text
<type>: <subject>

<body>

<footer>
```

**Types**:

- `feat`: Tính năng mới
- `fix`: Sửa bug
- `docs`: Thay đổi documentation
- `style`: Format code (không ảnh hưởng logic)
- `refactor`: Refactor code
- `test`: Thêm test
- `chore`: Công việc lặt vặt (update dependencies...)

**Ví dụ**:

```text
feat: Thêm chức năng reset mật khẩu

- Thêm API endpoint /api/reset-password
- Thêm giao diện nhập email
- Gửi email chứa link reset

Closes #123
```

### 3. Pull trước khi Push

```bash
# Trước khi push
git pull origin main
git push origin main
```

### 4. Sử dụng Branch cho mọi tính năng

- `main` hoặc `master`: Code production
- `develop`: Code đang phát triển
- `feature/ten-tinh-nang`: Tính năng mới
- `bugfix/ten-bug`: Sửa bug
- `hotfix/ten-hotfix`: Sửa bug khẩn cấp trên production

### 5. Review code trước khi merge

- Sử dụng Pull Request (PR) trên GitHub
- Ít nhất 1 người review trước khi merge
- Run test trước khi merge

### 6. Không commit file nhạy cảm

- Không commit file `.env`, API keys, passwords
- Dùng `.gitignore` để bỏ qua

### 7. Rebase thường xuyên (nếu team dùng)

```bash
git checkout feature-branch
git rebase main
```

### 8. Backup code

- Push code lên remote thường xuyên
- Đừng chỉ giữ code ở local

---

## Troubleshooting

### 1. Quên tạo Branch, đã code trên main

```bash
# Tạo branch mới từ main
git checkout -b feature-branch

# Chuyển main về commit trước
git checkout main
git reset --hard origin/main
```

### 2. Commit nhầm file

```bash
# Xóa file khỏi commit cuối (giữ thay đổi)
git reset --soft HEAD~1
git reset HEAD unwanted-file.txt
git commit -m "Message mới"

# Hoặc sửa commit cuối
git rm --cached unwanted-file.txt
git commit --amend
```

### 3. Push nhầm branch

```bash
# Xóa commit trên remote
git push origin +HEAD~1:branch-name

# Hoặc reset và force push (nguy hiểm!)
git reset --hard HEAD~1
git push -f origin branch-name
```

**Cảnh báo**: `git push -f` nguy hiểm, chỉ dùng khi chắc chắn!

### 4. Xóa nhầm branch

```bash
# Tìm commit cuối của branch bị xóa
git reflog

# Tạo lại branch
git checkout -b branch-name commit-hash
```

### 5. Merge conflict quá nhiều

```bash
# Hủy merge
git merge --abort

# Hoặc dùng theirs/ours
git checkout --theirs file.txt  # Lấy version của branch đang merge
git checkout --ours file.txt    # Lấy version của branch hiện tại
```

### 6. Quên push, đồng nghiệp đã push trước

```bash
# Pull với rebase
git pull --rebase origin main
```

### 7. Sửa commit message cuối cùng

```bash
git commit --amend -m "Message mới"
```

### 8. Gộp nhiều commit thành một

```bash
# Gộp 3 commit cuối
git rebase -i HEAD~3

# Trong editor, đổi 'pick' thành 'squash' (hoặc 's') cho các commit muốn gộp
```

### 9. Lỡ commit code debug

```bash
# Revert commit cụ thể (tạo commit mới đảo ngược)
git revert abc1234

# Hoặc reset (xóa commit)
git reset --hard HEAD~1
```

### 10. Clone quá chậm

```bash
# Clone shallow (không lấy toàn bộ lịch sử)
git clone --depth 1 https://github.com/username/repo.git
```

---

## Tài nguyên học thêm

### Trang web

- [Git Documentation chính thức](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)

### Interactive Learning

- [Learn Git Branching](https://learngitbranching.js.org/) - Game học Git
- [Git Immersion](http://gitimmersion.com/)

### Cheatsheet

- [GitHub Git Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)

### Tools hỗ trợ

- **GUI Clients**: GitKraken, SourceTree, GitHub Desktop
- **VS Code Extensions**: GitLens, Git Graph
- **Command Line Tools**: Oh My Zsh (git plugin)

---

## Kết luận

Git ban đầu có thể khó, nhưng với thực hành đều đặn:

- ✅ Tuần 1: Hiểu `add`, `commit`, `push`, `pull`
- ✅ Tuần 2: Tự tin tạo và merge branch
- ✅ Tuần 3: Xử lý conflict
- ✅ Tuần 4: Sử dụng Git trong team

**Bí quyết học Git**:

1. Thực hành mỗi ngày
2. Đừng sợ làm hỏng (có thể sửa được hầu hết)
3. Đọc error message kỹ càng
4. Hỏi khi không hiểu

**Nhớ rằng**: Mọi lập trình viên giỏi đều từng bối rối với Git. Cứ thực hành, bạn sẽ thành thạo!

---

## Workflow ví dụ (Dự án thực tế)

```bash
# 1. Clone dự án về
git clone https://github.com/company/project.git
cd project

# 2. Tạo branch cho tính năng mới
git checkout -b feature/add-login

# 3. Code code code...
# (Sửa file, tạo file mới...)

# 4. Xem thay đổi
git status
git diff

# 5. Add và commit
git add .
git commit -m "feat: Thêm tính năng đăng nhập"

# 6. Lấy code mới nhất từ main
git checkout main
git pull origin main

# 7. Merge main vào branch của mình (tránh conflict sau)
git checkout feature/add-login
git merge main
# (Giải quyết conflict nếu có)

# 8. Push branch lên remote
git push origin feature/add-login

# 9. Tạo Pull Request trên GitHub

# 10. Sau khi PR được approve và merge
git checkout main
git pull origin main
git branch -d feature/add-login  # Xóa branch local
```
