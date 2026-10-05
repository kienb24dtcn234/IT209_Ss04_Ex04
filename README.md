# Báo cáo Session 04 - Bài 4: Quản lý .gitignore và Sửa lịch sử (Amend)

- **Đường dẫn nộp:** `homework/session_04/ex4/`

---

## 1. Mục tiêu
- Gỡ file nhạy cảm `credentials.txt` khỏi theo dõi của Git **mà vẫn giữ file trên đĩa**.
- Cấu hình `.gitignore` để Git bỏ qua file này về sau.
- Sửa thông điệp commit gần nhất bằng `--amend`.

---

## 2. Bối cảnh
Trước đó đã lỡ `git add` + `git commit` nhầm file `credentials.txt` (chứa mật khẩu, API key) lên repo. Cần dọn sạch một cách an toàn, không xóa file vật lý.

---

## 3. Các bước thực hiện (chạy trong repo trên máy cá nhân)

### 3.1. Gỡ file khỏi cache theo dõi của Git (giữ file trên đĩa)
```bash
git rm --cached credentials.txt
```
> 🔑 `git rm --cached` chỉ xóa file khỏi **chỉ mục (staging/index)** của Git — tức Git ngừng theo dõi — nhưng **file vật lý vẫn còn** trong thư mục làm việc. Khác với `git rm` (xóa cả file trên đĩa) và khác với `rm` của hệ điều hành.

### 3.2. Tạo file .gitignore để bỏ qua file này về sau
Tạo file `.gitignore` (nội dung xem file kèm theo) với dòng quan trọng:
```
credentials.txt
```

### 3.3. Đưa thay đổi vào staging rồi sửa commit gần nhất bằng --amend
```bash
git add .gitignore
git commit --amend -m "feat: initial project setup (remove credentials, add .gitignore)"
```
> 🔑 `--amend` gộp thay đổi đang staged vào **commit gần nhất** và cho phép viết lại thông điệp, thay vì tạo thêm commit mới → lịch sử sạch.

---

## 4. Kiểm tra (Verification)

### 4.1. Trạng thái file — `credentials.txt` không còn được theo dõi
```bash
git status
```
Kết quả mong đợi:
```
On branch main
nothing to commit, working tree clean
```
→ `credentials.txt` KHÔNG xuất hiện ở Staged hay Modified (đã bị `.gitignore` bỏ qua), nhưng vẫn còn trên đĩa (kiểm tra bằng `ls` thấy file).

### 4.2. Lịch sử commit gần nhất — thông điệp đã được sửa
```bash
git log -n 1
```
Kết quả mong đợi (dán output thật vào đây khi nộp):
```
commit <hash> (HEAD -> main)
Author: Nguyen The Kien <email>
Date:   Mon Oct 5 ...

    feat: initial project setup (remove credentials, add .gitignore)
```

---

## 5. Kết quả
- `credentials.txt` đã được gỡ khỏi theo dõi của Git nhưng vẫn còn trên đĩa.
- `.gitignore` đảm bảo Git bỏ qua file này trong tương lai.
- Thông điệp commit gần nhất được sửa thành công bằng `--amend`.

---