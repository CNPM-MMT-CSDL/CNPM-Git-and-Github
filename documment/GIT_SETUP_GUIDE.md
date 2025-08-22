# 🚀 Git, GitHub và SSH Key

## 1. Git là gì?
- **Git**: hệ thống quản lý phiên bản (Version Control System).
- Giúp theo dõi lịch sử code, làm việc nhóm, quay lại phiên bản cũ.

## 2. GitHub là gì?
- **GitHub**: dịch vụ lưu trữ code online dùng Git.
- Hỗ trợ chia sẻ, làm việc nhóm, deploy project.

## 3. SSH Key là gì?
- **SSH key** gồm 2 phần:  
  - Private key (lưu trong máy, giữ bí mật).  
  - Public key (thêm lên GitHub).  
- Dùng để kết nối bảo mật với GitHub mà không cần nhập mật khẩu.

## 4. Cách tạo SSH Key và kết nối GitHub

- Tạo SSH key:  
  `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

- Thêm key vào SSH agent:  
  `eval "$(ssh-agent -s)"`  
  `ssh-add ~/.ssh/id_rsa`

- Copy public key:  
  `cat ~/.ssh/id_rsa.pub`

- Thêm vào GitHub:  
  Vào **Settings → SSH and GPG keys → New SSH key**, dán key, Save.

- Kiểm tra kết nối:  
  `ssh -T git@github.com`  
  → Nếu thành công sẽ hiện: *Hi <username>! You've successfully authenticated...*

✅ Từ giờ có thể dùng `git clone`, `git push`, `git pull` qua SSH mà không cần nhập mật khẩu.

---

# 🛠️ Extension Git hữu ích trong VS Code

## 1. Git Graph
![Git Graph](https://ardalis.com/img/image-git-graph.png)

- Hiển thị lịch sử commit dưới dạng **đồ thị trực quan**.  
- Cho phép xem nhanh branch, merge, tag.  
- Hỗ trợ checkout branch, tạo branch, revert commit... ngay trên giao diện.  

👉 Rất hữu ích để **nhìn tổng thể dòng lịch sử code** thay vì chỉ đọc `git log`.  

---

## 2. GitLens
![Git Graph](https://raw.githubusercontent.com/gitkraken/vscode-gitlens/main/images/docs/commit-graph.png)

- Cung cấp thông tin commit ngay trong file code: ai viết, khi nào, commit nào.  
- Cho phép xem chi tiết lịch sử thay đổi của từng dòng (blame).  
- Tích hợp mạnh với VS Code: hover, sidebar, history explorer.  

👉 Rất hữu ích để **theo dõi ai sửa code gì** và **hiểu bối cảnh commit**.  


✅ Kết hợp **Git Graph** + **GitLens** = vừa thấy **tổng quan (branch, merge)** vừa biết **chi tiết (commit, blame)** → cực kỳ mạnh cho teamwork.