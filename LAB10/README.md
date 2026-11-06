
# LAB 10 – Remote DNS Cache Poisoning

Bài thực hành môn **An toàn và Bảo mật Hệ thống Thông tin**, mô phỏng tấn công Remote DNS Cache Poisoning (Kaminsky Attack) trong môi trường VMware Workstation.

## Thông tin sinh viên

| Thông tin | Nội dung |
|---|---|
| Họ và tên | Lê Công Đạt |
| MSSV | 1150080130 |
| Lớp | CNPM2 |

## Mục tiêu

- Tìm hiểu cơ chế tấn công Remote DNS Cache Poisoning.
- Mô phỏng tấn công từ mạng ATTACKNET, không nghe lén DNSLAB.
- Kiểm tra sự thay đổi DNS Cache và kết quả phân giải tên miền.
- Khôi phục BIND9 và tìm hiểu các biện pháp bảo vệ DNS.

## Môi trường thực hành

| Máy ảo | Vai trò | Địa chỉ IP |
|---|---|---|
| pfSense | Firewall, phân chia mạng | 10.9.0.1 / 10.10.0.1 |
| Ubuntu WEB-PROXY | DNS Resolver | 10.9.0.10 |
| Ubuntu DMZ-WEB | AUTH-DNS / Web Server | 172.16.6.10 / 172.16.6.20 |
| Kali Linux | Attacker | 10.10.0.200 |
| Windows 10 | Victim | 10.9.0.20 |

## LINK YOUTUBE : https://youtu.be/VXDz1ReQ2Us




