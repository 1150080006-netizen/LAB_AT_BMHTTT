\# BÁO CÁO BÀI THỰC HÀNH LAB 3: THỰC HÀNH AN TOÀN HỆ THỐNG VÀ ĐIỀU TRA SỰ CỐ



Sinh viên: Nguyễn Ngọc Mỹ Dung

MSSV: 1150080006

Bài Lab: Lab 3 - An toàn hệ điều hành, phân tích tấn công và điều tra sự cố (Endpoint Security \& Incident Response)



\## 1. Môi trường thực hiện



\* Ảo hóa: VMware Workstation\[cite: 3]

\* Hệ điều hành: Windows 10 x64 (Hostname: `DESKTOP-RU23J91`, User: `mydung`)\[cite: 1]

\* Công cụ: Windows PowerShell (Admin), Windows Defender, Event Viewer, Wireshark/TShark, Sysinternals (Autoruns, Process Explorer)\[cite: 1, 3]



\## 2. Nội dung đã thực hiện



\* Kiểm tra cấu hình nền (Baseline) và kiểm chứng cơ chế phát hiện mã độc thời gian thực của Windows Defender qua tệp mẫu EICAR.

\* Tạo tài khoản `lab3user`, mô phỏng tấn công dò sai mật khẩu, phân tích nhật ký xác thực thất bại (Event ID 4625) trong Event Viewer và thực hiện đổi mật khẩu (Credential Rotation).

\* Đánh giá tính toàn vẹn dữ liệu của tệp cấu hình `app\_config.ini` qua mã băm SHA-256 trước và sau khi bị sửa đổi trái phép.

\* Giả lập dịch vụ web (cổng 8080), tạo lưu lượng DoS, bắt và phân tích gói tin TCP/HTTP bằng Wireshark/TShark, giám sát tiến trình qua Process Explorer.

\* Thiết lập cơ chế duy trì ẩn nấp (Persistence) bằng Registry Run Key trỏ tới backdoor giả lập, rà soát phát hiện bằng Autoruns và gỡ bỏ sạch.

\* Tạo và phân tích mẫu email lừa đảo (Phishing), chỉ ra các dấu hiệu giả mạo danh tính, tạo áp lực thời gian và thu thập thông tin xác thực.

\* Thu thập toàn bộ artifact (Event Logs .evtx, pcap), tạo bản kiểm kê mã băm bảo toàn tính toàn vẹn (`evidence\_manifest.txt`) và đóng gói tệp nén `LAB3\_Evidence\_Package.zip`.



\## 3. Kết quả đạt được



\* Windows Defender: Bật bảo vệ thời gian thực, ngăn chặn tức thì tệp thử nghiệm EICAR khi vừa ghi xuống đĩa.

\* Xác thực: Ghi nhận chính xác Event 4625 với mã lỗi bad password cho `lab3user`; xoay vòng mật khẩu thành công để vô hiệu hóa rủi ro brute-force.

\* Toàn vẹn dữ liệu: Mã băm SHA-256 thay đổi hoàn toàn sau can thiệp (`E0245FCC...` chuyển thành `C3286B45...`), chứng minh hiệu ứng tuyết lở và sự mất toàn vẹn.

\* Tấn công DoS: Bắt đầy đủ chuỗi gói tin flood TCP SYN/HTTP GET gửi dồn dập đến cổng 8080 trên Wireshark.

\* Ẩn nấp (Persistence): Nhận diện đúng entry `LAB3\_FakeUpdate` trong thẻ Logon của Autoruns và làm sạch khóa Registry thành công.

\* Chuỗi hành trình chứng cứ (Chain of Custody): Niêm phong toàn bộ bằng chứng với danh sách mã băm SHA-256 đối soát toàn vẹn.



\## 4. Hướng dẫn kiểm tra lại



\* Kiểm tra toàn vẹn gói bằng chứng: 

&#x20; \* Chạy lệnh PowerShell: `Get-FileHash -Algorithm SHA256 C:\\LAB3\\Evidence\\\*`

&#x20; \* So sánh với danh sách băm ghi nhận trong tệp `evidence\_manifest.txt`.

\* Kiểm tra Event Logs: Mở file `Security\_Artifact.evtx` bằng Event Viewer, lọc Event ID `4625` để xem lại vết đăng nhập lỗi của `lab3user`.

\* Kiểm tra lưu lượng mạng: Mở tệp `dos\_traffic.pcap` bằng Wireshark và nhập bộ lọc `tcp.port == 8080`.

