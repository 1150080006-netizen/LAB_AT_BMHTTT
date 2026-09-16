# BÁO CÁO BÀI THỰC HÀNH LAB 1: TELNET & SSH

- **Sinh viên:** Nguyễn Ngọc Mỹ Dung
- **MSSV:** 1150080006
- **Bài Lab:** Lab 1 - Bắt gói tin và phân tích tính an toàn của Telnet & SSH

---

### 1. Môi trường thực hiện
- **Ảo hóa:** VMware Workstation
- **Máy Client (Kali Linux):** `192.168.190.129`
- **Máy Server (Ubuntu):** `192.168.190.133` (User: `uitlab` / Pass: `123456`)
- **Công cụ:** Wireshark, OpenSSH, Telnet

---

### 2. Nội dung đã thực hiện
- Bắt gói tin Telnet (cổng 23) bằng Wireshark và dùng **Follow TCP Stream** trích xuất tài khoản/mật khẩu dạng rõ (cleartext).
- Tạo và cấu hình cặp khóa SSH Key trên Kali, đẩy Public Key sang Ubuntu bằng `ssh-copy-id`.
- Xác thực đăng nhập SSH thành công không cần dùng mật khẩu.
- Bắt gói tin SSHv2 (cổng 22) trên Wireshark, chứng minh dữ liệu phiên làm việc được mã hóa hoàn toàn.

---

### 3. Kết quả đạt được
- **Telnet:** Không an toàn, để lộ thông tin đăng nhập trên đường truyền (vi phạm tính Confidentiality).
- **SSH:** Toàn bộ payload trao đổi đều được mã hóa an toàn (`Encrypted packet payload`).
- **SSH Key:** Đăng nhập an toàn, loại bỏ nguy cơ tấn công dò quét mật khẩu (brute-force).

---

### 4. Hướng dẫn kiểm tra lại
1. Chạy dịch vụ SSH trên Ubuntu: `sudo systemctl start ssh`.
2. Mở Wireshark trên Kali bắt gói tại card `any` với bộ lọc: `tcp.port == 22`.
3. Từ Kali đăng nhập SSH không cần mật khẩu: `ssh uitlab@192.168.190.133`.
4. Trên Wireshark, chọn gói **SSHv2** > **Follow TCP Stream** để kiểm tra mã hóa.
