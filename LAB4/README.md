```bash
# 1. Kiểm tra IP máy quét Kali Linux
ip -br addr

# 2. Kiểm tra kết nối mạng sang máy mục tiêu
ping -c 4 192.168.59.128

# 3. Host Discovery (Phát hiện các host đang sống trong dải mạng)
sudo nmap -sn 192.168.59.0/24

# 4. Khảo sát cổng TCP SYN Scan (nửa mở) & TCP Connect Scan
sudo nmap -sS 192.168.59.128
nmap -sT 192.168.59.128

# 5. Khảo sát chính sách lọc tường lửa (FIN, Xmas, NULL, ACK scan)
sudo nmap -sF 192.168.59.128
sudo nmap -sX 192.168.59.128
sudo nmap -sN 192.168.59.128
sudo nmap -sA 192.168.59.128

# 6. Quét 20 cổng UDP phổ biến
sudo nmap -sU --top-ports 20 192.168.59.128

# 7. Nhận diện phiên bản dịch vụ và Hệ điều hành
sudo nmap -sV 192.168.59.128
sudo nmap -O 192.168.59.128
sudo nmap -A 192.168.59.128

# 8. Chạy NSE script kiểm tra SMB
sudo nmap -p 445 --script smb-os-discovery 192.168.59.128
sudo nmap -p 445 --script smb-vuln-ms17-010 192.168.59.128

# 9. Xuất kết quả ra các định dạng bằng chứng
sudo nmap -sV -O 192.168.59.128 -oN ket_qua.txt -oX ket_qua.xml
xsltproc ket_qua.xml -o bao_cao.html
