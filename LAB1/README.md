# BÁO CÁO THỰC HÀNH LAB 1

- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 1 - Examining SSH & Telnet in Wireshark
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
- Thiết lập mô hình mạng Client - Server - Attacker trên máy ảo.
- Cấu hình dịch vụ Telnet Server và SSH Server trên máy chủ.
- Tạo tài khoản sinh viên (dobaohoc) trên hệ thống.
- Thực hiện bắt gói tin bằng Wireshark khi kết nối qua Telnet và SSH.
- Đổi mật khẩu phức tạp để kiểm chứng khả năng bảo mật của Telnet.

## 2. Kết quả thực hiện
- Với Telnet: Giao thức truyền dữ liệu dạng văn bản rõ (plaintext), Wireshark có thể khôi phục đầy đủ username, password và các lệnh thực thi thông qua chức năng Follow TCP Stream. Mật khẩu dài/phức tạp không làm tăng tính bảo mật của Telnet.
- Với SSH: Toàn bộ dữ liệu payload đều được mã hóa, bảo vệ an toàn kênh truyền thông tin xác thực.

## 3. Các lưu ý
- Toàn bộ chi tiết báo cáo và hình ảnh minh chứng nằm trong file báo cáo Word đính kèm trong thư mục này.
