
# LAB4 – Rà soát an toàn mạng nội bộ bằng Nmap

## 1. Thông tin sinh viên

- Họ và tên: Lê Công Đạt
- MSSV: 1150080130
- Lớp: 11_ĐH_CNPM2
- Công cụ: Kali Linux, Nmap, Metasploitable 2 và Windows 10

## 2. Mô hình thực hành

- Kali Linux: `192.168.37.129`
- Metasploitable 2: `192.168.37.130`
- Windows 10: `192.168.37.128`
- Dải mạng kiểm tra: `192.168.37.0/24`

## 3. Nội dung thực hiện

- Phát hiện các host đang hoạt động.
- Quét cổng bằng TCP Connect, SYN, FIN, Xmas, NULL và ACK.
- Quét các cổng UDP phổ biến.
- Nhận diện phiên bản dịch vụ và hệ điều hành.
- Thu thập thông tin SMB bằng NSE Script.
- Xuất kết quả dạng TXT, XML và HTML.
- So sánh kết quả trước và sau khi áp dụng firewall.

## 4. Kết quả chính

- Phát hiện Metasploitable 2 tại địa chỉ `192.168.37.130`.
- Phát hiện nhiều dịch vụ đang mở như FTP, SSH, Telnet, HTTP, SMB và MySQL.
- Hệ điều hành mục tiêu được nhận diện là Linux 2.6.X.
- Dịch vụ SMB sử dụng Samba 3.0.20-Debian.
- Cổng `445/tcp` của Windows chuyển từ `open` sang `filtered` sau khi áp dụng firewall.
- Script kiểm tra MS17-010 không trả về trạng thái `VULNERABLE`, nên chưa đủ cơ sở kết luận mục tiêu có lỗ hổng.

## 5. Video thực hành

https://youtu.be/D4N3nvvZPkc

## 6. Kết luận

Bài thực hành giúp nhận biết các host, cổng và dịch vụ trong mạng nội bộ. Kết quả trước và sau khi áp dụng firewall cho thấy việc lọc cổng giúp giảm bề mặt tấn công và tăng mức độ an toàn cho hệ thống.
