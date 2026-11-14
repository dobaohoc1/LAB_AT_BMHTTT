# BÁO CÁO THỰC HÀNH LAB 10
- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 10 MÃ HÓA ĐỐI XỨNG CỔ ĐIỂN VÀ ỨNG DỤNG
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
Xây dựng tiện ích & giao diện: Phát triển lớp FileTextIO.java hỗ trợ chọn, đọc và ghi tệp văn bản (.txt) tương thích với JTextArea.   Hiện thực 6 thuật toán mật mã cổ điển: Gồm Caesar, Vigenère, Rail Fence, Playfair, Transposition, và Autokey kèm các form giao diện tương ứng.   Tích hợp Cơ sở dữ liệu Microsoft SQL Server: Thiết kế CSDL lưu trữ lịch sử thao tác (dbo.history), cấu hình kết nối an toàn (DbConfig.java), xử lý dữ liệu qua HistoryDao.java và xây dựng giao diện quản lý kết nối, xem lịch sử.   Phát triển ứng dụng tổng hợp: Tích hợp cả 6 thuật toán vào một màn hình duy nhất (CipherTongHop.java) với tính năng tự động lưu vết lịch sử.   Mô phỏng phân tích và thám mã (AttackDemos.java): Triển khai tấn công vét cạn Caesar (Brute-Force), phân tích tần suất chữ cái, và tấn công biết trước bản rõ (Known Plaintext Attack).   Giao diện Menu trung tâm (frm_Menu.java): Thiết kế bảng điều khiển tập trung để mở linh hoạt 9 cửa sổ chức năng khác nhau.   
  
## 2. Kết quả thực hiện
Nắm vững nguyên lý mật mã cổ điển: Hiểu rõ cơ chế và phân biệt được hai nhóm chính: mã hóa thay thế (biến đổi tần suất ký tự như Caesar, Vigenère, Autokey, Playfair) và mã hóa hoán vị (giữ nguyên 100% tần suất ký tự như Rail Fence, Transposition).

Thành thạo lập trình Java Swing & kiến trúc phần mềm: Tổ chức mã nguồn tách biệt 3 lớp (Logic, DAO/Config, GUI), xử lý tốt tệp văn bản UTF-8 và bắt ngoại lệ dữ liệu đầu vào.

Làm chủ kết nối CSDL Java Desktop: Cấu hình và kết nối an toàn với Microsoft SQL Server (Port 14333) qua JDBC (PreparedStatement/ResultSet), đồng thời đảm bảo ứng dụng chạy linh hoạt cả hai chế độ online (tự động lưu lịch sử) và offline.

Hiểu rõ kỹ thuật thám mã: Nhận diện được các điểm yếu bảo mật cốt lõi (không gian khóa nhỏ, lặp khóa chu kỳ, bảo toàn tần suất) để áp dụng các phương pháp phá mã như vét cạn (Brute-Force), phân tích tần suất n-gram và tấn công bản rõ đã biết.
## 3. Các lưu ý
Toàn bộ chi tiết phân tích 6 câu hỏi lý thuyết của Mục D và đầy đủ các hình ảnh minh chứng bắt buộc được trình bày chi tiết trong file báo cáo Word đính kèm trong thư mục này.
