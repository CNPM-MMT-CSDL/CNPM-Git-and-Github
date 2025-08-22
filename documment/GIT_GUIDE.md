# 🐙 Git Cơ Bản – Hướng Dẫn Lệnh Thông Dụng

## 1. Git là gì?
- **Git** là hệ thống quản lý phiên bản (VCS).  
- Giúp theo dõi lịch sử code, làm việc nhóm, khôi phục phiên bản cũ.  

---

## 2. Thiết lập ban đầu
- Cấu hình tên và email:
  - `git config --global user.name "Tên của bạn"`
  - `git config --global user.email "email@example.com"`
- Kiểm tra cấu hình:  
  - `git config --list`

![Git Config](images/config.png)

---

## 3. Làm việc với remote (GitHub/GitLab)
- Tạo repo mới trong thư mục hiện tại:  
  - `git init`
- Clone repo có sẵn:  
  - `git clone <url>`
- Thêm remote:  
  - `git remote add origin <url>`
- Xem remote:  
  - `git remote -v`

![Git Remote](images/remote.png)

---

## 4. Làm việc với file

![Git Status](https://git-scm.com/images/about/index1@2x.png)

- Kiểm tra trạng thái:  
  - `git status`
- Thêm file vào stage:  
  - `git add <tên_file>`
  - `git add .` (thêm tất cả)
- Commit (lưu thay đổi):  
  - `git commit -m "Thông điệp commit"`

![Git Status](images/status.png)

---

## 5. Làm việc với nhánh (Branch)

Nhánh (**branch**) trong Git giống như "bản copy" của code để bạn làm việc riêng mà không ảnh hưởng đến nhánh chính (thường là `main` hoặc `master`).  
Khi xong thì có thể hợp lại (merge/rebase).

---

### 1. Tạo nhánh mới
- `git branch <ten_nhanh>` → tạo nhánh mới.  
- `git checkout -b <ten_nhanh>` hoặc `git switch -c <ten_nhanh>` → tạo + chuyển luôn sang nhánh mới.  

---

### 2. Chuyển nhánh
- `git checkout <ten_nhanh>` → chuyển sang nhánh khác.  
- `git switch <ten_nhanh>` → cách mới hơn, dễ nhớ.  

---

### 3. Cherry-pick
- `git cherry-pick <commit_id>`  
- Lấy **một commit cụ thể từ nhánh khác** và áp dụng vào nhánh hiện tại.  
👉 Dùng khi bạn chỉ cần 1 thay đổi nhỏ, không muốn merge cả nhánh.  

---

### 4. Revert
- `git revert <commit_id>`  
- Tạo một commit mới để **đảo ngược thay đổi** của commit chỉ định, giữ lịch sử commit an toàn.  

---

### 5. Merge
- `git merge <ten_nhanh>`  
- Hợp nhánh khác vào nhánh hiện tại.  
- Có thể tạo commit merge (nếu có thay đổi khác nhau) hoặc fast-forward (nếu nhánh đi thẳng).  

---

### 6. Rebase
- `git rebase <ten_nhanh>`  
- **Chuyển nhánh hiện tại** thành "đứng sau" nhánh khác.  
- Giúp lịch sử commit gọn, thẳng hàng → dễ nhìn hơn.  
⚠️ Cẩn thận khi rebase nhánh đã push chung cho team.  

---

### 7. Reset
- `git reset --soft <commit_id>` → quay về commit, giữ code trong stage.  
- `git reset --mixed <commit_id>` → quay về commit, giữ code trong working directory (mặc định).  
- `git reset --hard <commit_id>` → quay về commit và **xóa luôn thay đổi** (không thể khôi phục).  

![Git Branch](images/branch.png)

---


## 6. Push (đẩy code lên remote)

Push = đưa code từ **local repo → remote repo (GitHub, GitLab, …)**

- Lần đầu push nhánh mới:  
  - `git push -u origin <ten_nhanh>`  
  - (cờ `-u` để gắn nhánh local với remote → lần sau chỉ cần `git push`)  

- Push nhánh hiện tại (sau khi đã liên kết):  
  - `git push`  

- Push ép buộc (⚠ nguy hiểm, dùng khi muốn ghi đè vào):  
  - `git push --force`  

![Git Push](images/push.png)

---

## 7. Pull (lấy code mới về + merge)

Pull = **fetch + merge** (tải code mới về từ remote và trộn vào nhánh hiện tại).

- Lấy code mới từ remote:  
  - `git pull`  

- Chỉ định remote + nhánh:  
  - `git pull origin <ten_nhanh>`  

![Git Pull](images/pull.png)

---

## 8. Fetch (lấy code mới về, không merge)

Fetch = tải code mới từ remote nhưng **không ảnh hưởng tới nhánh hiện tại**.  
Bạn có thể kiểm tra trước khi merge hoặc rebase.  

- Lấy toàn bộ thông tin mới từ remote:  
  - `git fetch`  

- Lấy về nhưng chỉ nhánh cụ thể:  
  - `git fetch origin <ten_nhanh>`  

![Git Fetch](images/fetch.png)

---

## 9. Conflict (Xung đột)

### Conflict là gì?
- Xảy ra khi **cùng một dòng code** bị thay đổi ở **nhiều nhánh hoặc nhiều commit khác nhau**, và Git không biết chọn phiên bản nào.  
- Thường gặp khi **merge, rebase hoặc pull**.  

---

### Ví dụ
- **Nhánh A** sửa dòng 10 thành:  
  `print("Xin chào")`  

- **Nhánh B** sửa dòng 10 thành:  
  `print("Hello World")`  

➡ Khi merge, Git sẽ báo conflict.

---

### Dấu hiệu conflict trong file
Git sẽ chèn các ký hiệu đặc biệt trong file bị xung đột:  

```bash
<<<<<< HEAD
print("Xin chào")
=======
print("Hello World")
>>>>>> branch-b
```
- `<<<<<<< HEAD` → code của nhánh hiện tại  
- `>>>>>>> branch-b` → code của nhánh được merge vào  
- `=======` → ranh giới giữa 2 thay đổi  

---

### Cách xử lý conflict
1. Mở file bị conflict  
2. Chỉnh sửa code cho đúng (chọn 1 trong 2 hoặc kết hợp)  
3. Xóa các dấu `<<<<<<<`, `=======`, `>>>>>>>`  
4. Thêm lại vào stage:  
   `git add <ten_file>`  
5. Commit để hoàn tất merge:  
   `git commit`  

---

### Công cụ hỗ trợ
- **VS Code**: có nút bấm *Accept Current / Accept Incoming / Accept Both*  
- **Git mergetool**: dùng tool ngoài (Meld, KDiff3, …)  

---

![Git Conflict](https://cdn.hashnode.com/res/hashnode/image/upload/v1630758001424/BQIq-8p1L.png)

---

✅ Phần lớn đi làm sẽ sài tool git graph để dùng chính ít khi gõ lệnh, gõ lệnh chỉ khi dùng server thôi
