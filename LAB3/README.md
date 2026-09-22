# BÁO CÁO THỰC HÀNH LAB 3

- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 3 NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
Thiết lập môi trường: Cài đặt Windows 11 (Host-only), chuẩn hóa cây thư mục C:\LAB3, cấu hình Sysmon, Autoruns, Process Explorer, Wireshark và thu thập baseline sạch.
TH1: Xây dựng Risk Register và phân loại 5 nhóm nguồn đe dọa thực tế.
TH2: Kiểm chứng chu trình phát hiện và cách ly mã độc mẫu (EICAR) bằng Microsoft Defender.
TH3: Bật Audit Logon (Event 4624, 4625, 4648) và kiểm chứng bảo mật tài khoản lab3user.
TH4: Tạo persistence lành tính (LAB3_Run_Demo, Scheduled Task) và HTTP listener cục bộ (127.0.0.1:8080); phát hiện qua Sysmon, Autoruns và Process Explorer.
TH5: Bắt gói tin Wireshark trên cổng loopback, so sánh lưu lượng HTTP (plaintext) với HTTPS/TLS.
TH6: Thực thi test tải cục bộ (DoS) và phân tích dataset offline về DDoS, Mail bombing.
TH7: Phân tích mẫu phishing offline và phân loại các tình huống Social Engineering.
Quy trình phục hồi: Dọn dẹp sạch sẽ artefact, xác thực hệ thống và băm SHA-256 toàn bộ file bằng chứng.

## 2. Kết quả thực hiện
- Với Telnet: Giao thức truyền dữ liệu dạng văn bản rõ (plaintext), Wireshark có thể khôi phục đầy đủ username, password và các lệnh thực thi thông qua chức năng Follow TCP Stream. Mật khẩu dài/phức tạp không làm tăng tính bảo mật của Telnet.
- Với SSH: Toàn bộ dữ liệu payload đều được mã hóa, bảo vệ an toàn kênh truyền thông tin xác thực.

## 3. Các lưu ý
- Toàn bộ chi tiết báo cáo và hình ảnh minh chứng nằm trong file báo cáo Word đính kèm trong thư mục này.
