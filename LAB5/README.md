# Thực hành cấu hình Firewall pfSense

## Thông tin

- Họ tên: Lê Công Đạt
- Môn học: An toàn bảo mật hệ thống thông tin
- Mô hình: pfSense, Windows Server 2022 và Kali Linux
- Công cụ ảo hóa: VMware Workstation

## Link youtube : https://youtu.be/opwY-AqjXcg

## Mô hình mạng

| Thiết bị / mạng | Địa chỉ IP | Vai trò |
|---|---|---|
| pfSense LAN | `10.0.0.1/8` | Gateway mạng LAN |
| Windows Server 2022 | `10.0.0.2/8` | Máy chủ trong LAN |
| Kali Linux – LAN | `10.0.0.3/8` | Máy kiểm tra rule LAN |
| pfSense DMZ | `172.16.0.1/16` | Gateway mạng DMZ |
| Kali Linux – DMZ | `172.16.0.2/16` | Máy kiểm tra rule DMZ |

pfSense có các giao diện WAN, LAN và DMZ. Outbound NAT được để ở chế độ tự động.

## Nội dung thực hành

### Tình huống 1: Chặn ICMP, cho phép DNS và Web

Cấu hình các rule trên LAN:

- Chặn ICMP từ LAN đến mọi nơi.
- Cho phép TCP/UDP cổng 53 để truy vấn DNS.
- Cho phép TCP cổng 80 và 443 bằng alias `WEB_PORTS`.

**Kết quả kiểm tra:**

- Ping `8.8.8.8`: bị chặn.
- Phân giải tên miền bằng `Resolve-DnsName`: thành công.
- Truy cập HTTPS bằng `curl.exe`: thành công.

### Tình huống 2: Chỉ cho phép máy chủ được truy cập Internet

Cấu hình rule cho phép địa chỉ `10.0.0.2` và rule chặn các máy còn lại trong LAN. Rule cho phép máy chủ được đặt phía trên rule chặn.

**Kết quả kiểm tra:**

- Windows Server `10.0.0.2` truy cập Internet được.
- Kali `10.0.0.3` ping `8.8.8.8` thất bại.

### Tình huống 3: Cô lập DMZ khỏi LAN

Cấu hình rule trên DMZ:

1. Chặn lưu lượng từ DMZ subnets đến LAN subnets.
2. Cho phép lưu lượng từ DMZ subnets đến mọi nơi để truy cập Internet.

**Kết quả kiểm tra:**

- Kali trong DMZ `172.16.0.2` ping gateway `172.16.0.1`: thành công.
- Kali trong DMZ ping `8.8.8.8`: thành công.
- Kali trong DMZ ping Windows Server `10.0.0.2`: thất bại.

## Kết luận

Các tình huống đã thực hành cách tạo và sắp xếp firewall rule trên pfSense, kiểm tra lưu lượng bằng ping, truy vấn DNS và truy cập Web. Kết quả cho thấy rule có thể giới hạn quyền truy cập giữa các máy và các vùng mạng LAN/DMZ.

## Bằng chứng

Ảnh chụp cấu hình rule và kết quả kiểm tra được ghi trong word
