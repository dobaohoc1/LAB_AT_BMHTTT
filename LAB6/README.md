# BÁO CÁO THỰC HÀNH LAB 6

- **Họ và tên:** Đỗ Bảo Học
- **Mã số sinh viên:** 1150080135
- **Tên bài Lab:** Lab 6 XÁC THỰC ACTIVE DIRECTORY VÀ CHÍNH SÁCH TRUY CẬP TRÊN pfSense
- **Link Video thực hành (YouTube):** [https://www.youtube.com/@baohoc6710]

## 1. Nội dung đã thực hiện
Xây dựng mô hình mạng 4 phân vùng: Thiết lập tường lửa pfSense với đầy đủ 4 interface (WAN, MGMT, LAN, DMZ); cấu hình máy chủ DMZ-WEB mang 4 địa chỉ IP phụ (.10, .20, .30, .40) nhằm mô phỏng các danh mục website.   
Triển khai máy chủ Domain Controller (DC01): Cài đặt dịch vụ AD DS và DNS cho domain lab6.test; tạo OU LAB6-Users chứa 2 tài khoản người dùng sv_a, sv_b cùng tài khoản dịch vụ svc_pfsense_ldap.   
Tích hợp LDAP và Captive Portal: Cấu hình pfSense kết nối tới Active Directory qua LDAP (cổng TCP/389); kích hoạt Captive Portal trên phân vùng LAN sử dụng AD làm nguồn xác thực tập trung.   
Khởi tạo Aliases và Schedules: Định nghĩa các nhóm IP máy trạm (CLIENT_A, CLIENT_B, POLICY_CLIENTS), nhóm website đích (GENERAL_SITE, JOB_SITE, SOCIAL_SITE, RESTRICTED_SITE), danh mục cổng Web (WEB_PORTS) và các khung thời gian hoạt động (WORK_HOURS, LUNCH_WINDOW / TEST_NOW).   
Cấu hình chính sách tường lửa (Ruleset): Thiết lập bộ luật trên LAN theo nguyên tắc First-match (từ trên xuống dưới) kết hợp điều kiện IP, Port, Schedule; cấu hình rule trên DMZ để ngăn chặn lưu lượng khởi tạo từ DMZ sang LAN.   
Thực nghiệm kiểm thử, phân tích và sao lưu: Kiểm tra toàn bộ 7 kịch bản chính sách; so sánh hành vi giữa Block và Reject; đối chiếu bản ghi tại Firewall Log và bảng quản lý phiên State Table; xuất tập tin sao lưu cấu hình config.xml.   
  
## 2. Kết quả thực hiện
Xác thực định danh: pfSense truy vấn và xác thực thành công tài khoản sv_a và sv_b từ AD DS qua công cụ Diagnostics; Client khi mở trình duyệt được chuyển hướng chính xác đến Captive Portal và đăng nhập thành công vào mạng.   
Kịch bản 1 (Chặn Job Site): Client-A bị chặn truy cập 172.16.6.20 (Job Site) nhưng vẫn kết nối thành công đến 172.16.6.10 (General Site).   
Kịch bản 2 (Cấm nhóm Restricted): Cả Client-A và Client-B đều bị chặn hoàn toàn khi truy cập 172.16.6.40 (Restricted Site) theo nhóm đối tượng POLICY_CLIENTS.   
Kịch bản 3 (Kiểm soát theo lịch trình): Client-B truy cập được 172.16.6.30 (Social Site) khi Schedule đang kích hoạt; tự động bị chặn ngay khi ngoài khung giờ.   
Kịch bản 4 (Giới hạn dịch vụ ngoài Web): Trong giờ làm việc, client chỉ được phép duyệt web (HTTP/HTTPS qua cổng 80/443); các giao thức khác như ping (ICMP) bị chặn hoàn toàn.   
Kịch bản 5 (Cô lập DMZ): Chiều từ LAN sang Web DMZ hoạt động bình thường, nhưng chiều ngược lại từ DMZ-WEB khởi tạo kết nối sang DC01 (10.6.0.10) bị tường lửa từ chối hoàn toàn.   
Kịch bản 6 & 7 (Hành vi lọc, Log & State):Đặt Reject: Phía client nhận thông báo từ chối kết nối tức thì (Connection refused).   Đặt Block: Phía client bị treo chờ đến khi hết hạn thời gian (Connection timed out).   
Hệ thống Firewall Log ghi nhận đầy đủ các gói tin vi phạm kèm chi tiết IP nguồn/đích; bảng State Table duy trì và cập nhật chính xác các phiên kết nối.   

## 3. Các lưu ý
Toàn bộ chi tiết phân tích 6 câu hỏi lý thuyết của Mục D và đầy đủ các hình ảnh minh chứng bắt buộc được trình bày chi tiết trong file báo cáo Word đính kèm trong thư mục này.
