# BÁO CÁO THỰC HÀNH LAB 8

- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 8 LOCAL DNS ATTACK DNS SPOOFING VÀ CACHE POISONING TRONG MẠNG ẢO CÔ LẬP
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
Xây dựng và cấu hình mạng cô lập DNS-LAB (10.9.0.0/24) phía sau pfSense, thiết lập máy chủ DNS-SERVER chạy BIND9 làm resolver/cache, đồng thời cấu hình máy nạn nhân (VICTIM) và máy tấn công (ATTACKER-Kali).   Thực hiện 3 nhiệm vụ tấn công cốt lõi gồm: Thay đổi file /etc/hosts cục bộ trên nạn nhân (Task 1), thực hiện tấn công giả mạo phản hồi DNS trực tiếp - Direct DNS Spoofing nhắm vào client (Task 2), và tiến hành đầu độc bộ nhớ đệm máy chủ DNS - DNS Cache Poisoning nhắm vào resolver (Task 3).  
  
## 2. Kết quả thực hiện
Hoàn tất việc thiết lập cơ sở hạ tầng mạng lab, các dịch vụ DNS, trang web giả mạo và web hợp lệ hoạt động ổn định, phục vụ chính xác cho quá trình quan sát luồng gói tin bằng Wireshark.   Ghi nhận thành công các kịch bản chuyển hướng tên miền: file hosts ghi đè thành công trên cục bộ, các gói phản hồi DNS giả mạo đã vượt qua phản hồi hợp lệ trong cuộc đua để chuyển hướng nạn nhân sang trang web của kẻ tấn công, và bộ nhớ đệm của DNS server đã bị đầu độc thành công trong thời gian TTL.   
## 3. Các lưu ý
Toàn bộ chi tiết phân tích 6 câu hỏi lý thuyết của Mục D và đầy đủ các hình ảnh minh chứng bắt buộc được trình bày chi tiết trong file báo cáo Word đính kèm trong thư mục này.
