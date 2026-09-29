\# BÁO CÁO BÀI THỰC HÀNH LAB 3: THỰC HÀNH AN TOÀN HỆ THỐNG VÀ ĐIỀU TRA SỰ CỐ



Sinh viên: Nguyễn Ngọc Mỹ Dung

MSSV: 1150080006
# Báo Cáo Thực Hành: Lab 4 - Khảo Sát Và Đánh Giá Bề Mặt Mạng Bằng Nmap

## 1. Giới thiệu tổng quan
Tài liệu này ghi lại toàn bộ quá trình thực hành rà quét, khảo sát bề mặt mạng nội bộ, nhận diện dịch vụ và phân tích rủi ro an toàn hệ thống bằng công cụ **Nmap** trong môi trường mạng ảo hóa cô lập an toàn trên VMware Workstation.

* **Môn học:** An toàn hệ thống thông tin
* **Nền tảng ảo hóa:** VMware Workstation
* **Dải mạng khảo sát:** `192.168.168.0/24`

---

## 2. Mô hình hệ thống (Topology - 2 Máy ảo thực tế)

| Thiết bị / Máy ảo | Hệ điều hành | Vai trò | Địa chỉ IP | Subnet Mask | Địa chỉ MAC |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VM 1: MydunKali** | Kali Linux | Máy quét chính (Auditor / Scanner) | `192.168.168.133` | `255.255.255.0` | `00:0C:29:FF:FE:8B:54:AF` |
| **VM 2: Metasploitable2** | Ubuntu Linux | Máy đích cố ý có lỗ hổng (Target) | `192.168.168.132` | `255.255.255.0` | `00:0C:29:04:71:FC` |
| **VMware Gateway** | Linux Kernel | Cổng cấp mạng/DHCP tự sinh của VMware | `192.168.168.254` | `255.255.255.0` | `00:50:56:F7:73:E8` |

---

## 3. Quy trình thực hiện & Các lệnh Nmap chính

### 3.1. Xác thực IP & Kiểm tra kết nối
* **Kiểm tra IP trên Kali Linux:**
  ```bash
  ip -br addr