# LAB 6 — pfSense, Active Directory và chính sách truy cập

Bài thực hành môn **An toàn hệ thống thông tin**: xây dựng môi trường mạng riêng, tích hợp Active Directory với pfSense và kiểm thử chính sách truy cập theo máy trạm, dịch vụ và thời gian.

## Thông tin sinh viên

| Thông tin | Nội dung |
|---|---|
| Họ và tên | Lê Công Đạt |
| MSSV | 1150080130 |
| Lớp | CNPM2 |

## Báo cáo thực hành
## Link youtube : https://youtu.be/Ey4BnsueIJ8


Báo cáo bao gồm cấu hình môi trường, hình ảnh minh chứng, kiểm thử chính sách và trả lời câu hỏi.

## Môi trường triển khai

- VMware Workstation.
- pfSense.
- Windows Server 2022: Active Directory và DNS.
- Hai máy Windows 10: Client-A và Client-B.
- Ubuntu Server: Nginx và các website mô phỏng.

### Phân chia vùng mạng

| Vùng mạng | Mạng ảo | Địa chỉ mạng | Vai trò |
|---|---|---|---|
| WAN | VMnet8 | 192.168.250.0/24 | Kết nối ra ngoài qua NAT |
| MGMT | VMnet3 | 192.168.56.0/24 | Quản trị hệ thống |
| LAN | VMnet4 | 10.6.0.0/24 | Domain Controller và máy trạm |
| DMZ | VMnet5 | 172.16.6.0/24 | Website mô phỏng |

### Địa chỉ thiết bị

| Thiết bị / Interface | Địa chỉ IP | Chức năng |
|---|---|---|
| pfSense — LAN | 10.6.0.1 | Gateway LAN, Captive Portal |
| pfSense — MGMT | 192.168.56.254 | Interface quản trị |
| pfSense — DMZ | 172.16.6.1 | Gateway DMZ |
| DC01 | 10.6.0.10 | AD DS và DNS cho domain `lab6.test` |
| Client-A | 10.6.0.21 | Kiểm thử bằng tài khoản `sv_a` |
| Client-B | 10.6.0.22 | Kiểm thử bằng tài khoản `sv_b` |
| DMZ-WEB | 172.16.6.10, 172.16.6.20, 172.16.6.30, 172.16.6.40 | Nginx phục vụ website mô phỏng |

Client-A và Client-B sử dụng DNS `10.6.0.10`, gateway `10.6.0.1`.

## Nội dung thực hành

| Phần | Nội dung |
|---|---|
| B | Dựng mạng ảo, cấu hình pfSense, Domain Controller, máy trạm và DMZ-WEB |
| C | Tích hợp Active Directory qua LDAP với backend `LAB6-AD` |
| D | Tạo Captive Portal zone `LAB6_USERS` trên LAN và xác thực người dùng domain |
| E | Tạo alias cho máy trạm, website và cổng dịch vụ |
| F | Tạo schedule cho giờ nghỉ, giờ hành chính và kiểm thử |
| G | Triển khai năm kịch bản chính sách và kiểm tra Firewall Log |

Báo cáo có phần trả lời 12 câu hỏi về topology, LDAP, Captive Portal, firewall rule, schedule và state.

## Alias

| Alias | Giá trị |
|---|---|
| `CLIENT_A` | 10.6.0.21 |
| `CLIENT_B` | 10.6.0.22 |
| `POLICY_CLIENTS` | 10.6.0.21, 10.6.0.22 |
| `GENERAL_SITE` | 172.16.6.10 |
| `JOB_SITE` | 172.16.6.20 |
| `SOCIAL_SITE` | 172.16.6.30 |
| `RESTRICTED_SITE` | 172.16.6.40 |
| `WEB_PORTS` | 80, 443 |

## Schedule

Thời gian áp dụng theo múi giờ Việt Nam (UTC+7).

| Schedule | Thời gian | Mục đích |
|---|---|---|
| `LUNCH_WINDOW` | 11:30–13:00, thứ Hai–thứ Sáu | Cho Client-B truy cập SOCIAL_SITE trong giờ nghỉ |
| `WORK_HOURS` | 08:00–17:00, thứ Hai–thứ Sáu | Cho phép HTTP/HTTPS trong giờ hành chính |
| `TEST_NOW` | Khoảng 10–15 phút chứa thời điểm kiểm thử | Kiểm chứng nhanh chính sách theo lịch |

## Các kịch bản kiểm thử

| Kịch bản | Chính sách | Kết quả mong đợi |
|---|---|---|
| 1 | Chặn Client-A truy cập JOB_SITE | Client-A không truy cập được `172.16.6.20`, vẫn truy cập GENERAL_SITE |
| 2 | Chặn RESTRICTED_SITE cho cả hai client | A và B không truy cập được `172.16.6.40`, vẫn truy cập GENERAL_SITE |
| 3 | Client-B chỉ truy cập SOCIAL_SITE trong giờ nghỉ | Được phép trong lịch; bị chặn ngoài lịch |
| 4 | Chỉ cho HTTP/HTTPS trong giờ hành chính | Cho TCP/80 và TCP/443 trong lịch; chặn dịch vụ khác và truy cập ngoài lịch qua pfSense |
| 5 | Cô lập DMZ khỏi LAN | DMZ không khởi tạo được kết nối tới LAN; LAN vẫn truy cập web theo chính sách |

Hình ảnh cấu hình và kết quả kiểm thử được trình bày trong [báo cáo Word](./lab6.docx).

## Ghi chú kỹ thuật

- LDAP và Captive Portal xác thực tài khoản Active Directory. Firewall rule chuẩn áp dụng theo IP, port, interface và schedule.
- Các website trong DMZ mô phỏng nhóm nội dung bằng IP cố định.
- Rule được xét từ trên xuống theo nguyên tắc **first-match**. Rule chặn cụ thể cần nằm trên rule cho phép rộng.
- Khi schedule không active, rule gắn schedule không áp dụng. Cần rule Block bên dưới để chặn ngoài giờ.
- Khi kiểm thử từng kịch bản, cần kiểm tra các rule Pass cũ để tránh bỏ qua chính sách mới.
- Sau khi thay đổi rule, sử dụng kết nối mới hoặc xóa state liên quan để kiểm thử.
- Client và DC01 cùng subnet nên truy vấn DNS giữa hai bên không đi qua pfSense. DC01 cần được phép truy vấn DNS upstream.
- Website mô phỏng chạy HTTP trên cổng 80; cổng 443 được khai báo trong alias chính sách.

## Cấu trúc thư mục

```text
LAB6/
├── README.md
└── lab6.docx
```
