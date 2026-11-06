# BÁO CÁO THỰC HÀNH LAB 9
- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 9 REMOTE DNS CACHE POISONING TRONG MÔI TRƯỜNG pfSense CÔ LẬP
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
Thiết lập phân vùng mạng và Tường lửa pfSense:
Kế thừa hạ tầng mạng từ Lab trước, thêm card mạng cho pfSense để tạo phân vùng cô lập ATTACKNET (10.10.0.1/24).
Chuyển máy tấn công Kali Linux sang subnet mới (10.10.0.200/24), đồng thời thiết lập chế độ Promiscuous Mode = Deny trên vSwitch để triệt tiêu hoàn toàn khả năng nghe lén gói tin cục bộ.
Cấu hình ma trận luật tường lửa (Firewall Ruleset) chặt chẽ trên pfSense: chỉ mở các luồng dịch vụ tối thiểu cần thiết cho bài lab (DNS query, HTTP, race relay) và chặn toàn bộ lưu lượng không liên quan hay ra Internet.
Khảo sát và nghiệm thu Baseline:
Thiết lập dịch vụ phân giải tên miền BIND9 trên DNS-SERVER (10.9.0.10) với forward zone example.lab10.test trỏ sang máy chủ ủy quyền AUTH-DNS (172.16.6.20).
Khởi chạy script dịch vụ auth_dns_relay_lab10.py trên AUTH-DNS phục vụ phân giải chính thống và mở cổng race harness UDP 5300.
Kiểm chứng máy trạm VICTIM (10.9.0.100) phân giải chính xác tên miền www.example.lab10.test trả về địa chỉ IP trang web hợp lệ 172.16.6.10.
  
## 2. Kết quả thực hiện
Nắm vững bản chất tấn công Remote DNS Cache Poisoning: Hiểu rõ sự khác biệt giữa tấn công Local DNS Spoofing (nghe lén trực tiếp TXID) và tấn công Remote (phải đoán "mù" TXID và cổng nguồn UDP từ xa qua mạng định tuyến).
Thấu hiểu cơ chế tấn công Kaminsky: Nắm rõ kỹ thuật sử dụng chuỗi tên miền con ngẫu nhiên (random non-existent subdomains) để buộc Resolver luôn phải truy vấn upstream, vượt qua rào cản TTL của cache; hiểu rõ vai trò của bản ghi ủy quyền NS kết hợp bản ghi Glue A trong Authority/Additional Section để chuyển hướng toàn bộ phân vùng (zone delegation).   
## 3. Các lưu ý
Toàn bộ chi tiết phân tích 6 câu hỏi lý thuyết của Mục D và đầy đủ các hình ảnh minh chứng bắt buộc được trình bày chi tiết trong file báo cáo Word đính kèm trong thư mục này.
