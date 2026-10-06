# BÁO CÁO THỰC HÀNH LAB 5

- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 5 THIẾT LẬP MÔ HÌNH TƯỜNG LỬA pfSense
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
- Thiết lập mô hình phân vùng mạng 3 chân (Three-legged Firewall): Khởi tạo máy ảo tường lửa pfSense (FreeBSD 64-bit) với 3 giao diện mạng riêng biệt gồm WAN (Bridged kết nối Internet), LAN (10.0.0.1/8 qua Host-only/VMnet1) và DMZ (172.16.0.1/16 qua LAN Segment/Internal Network).   
- Cấu hình trạm mạng nội bộ (LAN): Thiết lập máy quản trị trên máy thật (10.0.0.100/8) và máy Domain Controller (10.0.0.2/8, Gateway 10.0.0.1, DNS Forwarder 8.8.8.8); kiểm tra định tuyến và khả năng quản trị pfSense qua WebConfigurator ([https://10.0.0.1](https://10.0.0.1)).   
- Cấu hình phân vùng dịch vụ công cộng (DMZ): Gán card mạng OPT1 thành interface DMZ (172.16.0.1/16), triển khai máy chủ DMZ-Web (172.16.0.2/16, Gateway 172.16.0.1) và kích hoạt dịch vụ IIS Web Server.   
- Kích hoạt cơ chế Outbound NAT: Thiết lập chế độ Hybrid Outbound NAT, xác nhận hệ thống tự sinh các rule NAT tự động cho phép cả hai dải mạng nội bộ LAN (10.0.0.0/8) và DMZ (172.16.0.0/16) chuyển đổi địa chỉ để ra Internet.   
- Chuẩn hóa Ruleset nền tảng và quản lý State Table: Vô hiệu hóa hai rule mặc định (Default allow LAN to any IPv4/IPv6), duy trì Anti-Lockout Rule bảo vệ WebGUI; khởi tạo rule nền tảng do người dùng kiểm soát (LAN net -> Any Pass) và thực thi thao tác Reset States để đo kiểm trạng thái cắt/mở lưu lượng từ Domain Controller.   
- Triển khai Tình huống 1 (Kiểm soát lọc gói tin theo dịch vụ): Thiết lập chính sách kết hợp chặn toàn bộ gói tin ICMP (ping) nhưng mở luồng phân giải tên miền DNS (TCP/UDP 53) và lưu lượng Web HTTP/HTTPS (TCP 80/443); kiểm thử bằng ping, nslookup và curl.   
- Triển khai Tình huống 2 (Kiểm soát truy cập theo định danh IP): Thiết lập luật phân quyền chỉ cho phép duy nhất máy Domain Controller (10.0.0.2) được phép ra Internet và chặn toàn bộ các máy khác trong dải LAN net; kiểm thử đối chứng giữa DC và máy trạm phụ LAN-Test (10.0.0.3).   
- Triển khai Tình huống 3 (Cô lập vùng DMZ khỏi LAN): Xây dựng baseline kiểm thử cho phép DMZ kết nối LAN; sau đó áp dụng rule Block DMZ net -> LAN net đặt phía trên rule Pass DMZ net -> Any để ngăn chặn DMZ xâm nhập LAN nội bộ trong khi máy chủ DMZ vẫn kết nối Internet bình thường.   
- Triển khai Tình huống 4 (Chuyển tiếp cổng Port Forwarding): Tắt chính sách chặn dải mạng riêng trên cổng WAN, cấu hình NAT Port Forwarding ánh xạ cổng công cộng WAN:8080 về máy chủ nội bộ DMZ:80 (IIS); kiểm thử truy cập thành công từ trình duyệt máy thật bên ngoài.   
- Triển khai Tình huống 5 (Giám sát và phân tích Firewall Log): Kích hoạt tính năng Log packets that are handled by this rule trên các rule chặn, tạo lưu lượng vi phạm và trích xuất phân tích bản ghi nhật ký drop gói tin thời gian thực trong Status -> System Logs -> Firewall.
  
## 2. Kết quả thực hiện
- Nguyên lý đánh giá luật "First Match Wins": pfSense xử lý các quy tắc từ trên xuống dưới theo thứ tự xuất hiện. Gói tin sẽ nhận hành động của rule đầu tiên mà nó thỏa mãn; do đó, các luật chặn cụ thể (Block) bắt buộc phải đặt trên các luật cho phép tổng quát (Pass) để tránh bị vô hiệu hóa.   
- Cơ chế tường lửa có trạng thái (Stateful Inspection): pfSense duy trì bảng trạng thái phiên (State Table). Khi một kết nối đã được thiết lập, các gói tin thuộc cùng phiên sẽ tự động được đi qua mà không cần duyệt lại ruleset. Vì vậy, thao tác Reset States sau mỗi lần thay đổi rule là yêu cầu bắt buộc để đảm bảo tính chính xác của các bài đo kiểm an ninh.   
- Phân định ranh giới giữa NAT và Firewall Rule: NAT giải quyết bài toán định tuyến và tái cấu trúc địa chỉ mạng (chuyển đổi IP Private $\leftrightarrow$ Public hoặc Port Redirection) nhưng không mang tính chất kiểm soát an ninh. Firewall Rule đóng vai trò là chính sách an toàn (Access Control List), trực tiếp quyết định quyền cho phép hay bác bỏ dữ liệu.   
- Kiến trúc phòng thủ phân vùng DMZ: Việc đưa máy chủ hướng ngoại (Web/Mail/FTP) vào DMZ và cô lập luồng truy cập từ DMZ sang LAN triệt tiêu hoàn toàn nguy cơ tấn công dịch chuyển ngang (lateral movement). Khi máy chủ DMZ bị xâm nhập, kẻ tấn công vẫn bị chặn đứng trước bức tường lửa và không thể tiếp cận dữ liệu nhạy cảm trong LAN (Domain Controller).   
- Khả năng quan sát qua Firewall Logging: Ghi nhật ký tường lửa cho phép quản trị viên định danh chính xác gói tin bị drop hay pass, cung cấp bằng chứng IP nguồn/đích, port và giao thức theo thời gian thực để nhận diện sớm các hành vi quét cổng dò xét hoặc cấu hình sai chính sách.   

## 3. Các lưu ý
Toàn bộ chi tiết phân tích 6 câu hỏi lý thuyết của Mục D và đầy đủ các hình ảnh minh chứng bắt buộc (Cấu hình card mạng VMware, Console IP, Dashboard pfSense, Outbound NAT, Bảng rule LAN, cùng các ảnh kiểm thử trước/sau của 5 tình huống) được trình bày chi tiết trong file báo cáo Word đính kèm trong thư mục này.
