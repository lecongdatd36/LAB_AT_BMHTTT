# Lab 1: Bắt gói tin Telnet và SSH bằng Wireshark

## Thông tin sinh viên

Họ và tên: Lê Công Đạt

Mã số sinh viên: 1150080130

Lớp: 11_ĐH_CNPM2

Học phần: Thực hành An toàn Hệ thống thông tin

## Mục tiêu

Thiết lập kết nối Telnet và SSH giữa máy khách và máy chủ; sử dụng Wireshark để phân tích lưu lượng, so sánh khả năng bảo vệ thông tin đăng nhập và nội dung trao đổi; thực hành xác thực SSH bằng khóa công khai.

## Nội dung thực hiện

Kiểm tra địa chỉ IP và kết nối giữa các máy bằng lệnh ping.

Cài đặt, khởi động Telnet Server và tạo tài khoản thử nghiệm lecongdat.

Đăng nhập Telnet bằng PuTTY, thực hiện lệnh và bắt gói bằng Wireshark.

Sử dụng Follow TCP Stream để xem thông tin đăng nhập và nội dung phiên Telnet.

Đổi sang mật khẩu phức tạp và thực hiện lại phép thử Telnet.

Khởi động SSH Server, kiểm tra fingerprint của khóa máy chủ và kết nối SSH.

Phân tích thông tin bắt tay và các gói dữ liệu mã hóa của SSH.

Tạo cặp khóa Ed25519 bằng PuTTYgen, đăng ký khóa công khai trong ~/.ssh/authorized_keys và thử đăng nhập SSH bằng khóa.
Kết quả thực hiện

## Kết quả thực hiện

Kết nối từ xa tới Kali Server và thực hiện các lệnh kiểm tra tài khoản, thư mục và xuất thông báo.

Quan sát được thông tin đăng nhập trong phiên Telnet bằng Follow TCP Stream.

Việc tăng độ phức tạp của mật khẩu không bổ sung mã hóa cho Telnet.

Quan sát được thông tin phiên bản và thuật toán trong giai đoạn bắt tay SSH; các gói sau khi thiết lập mã hóa được Wireshark nhận diện là Encrypted packet.

Đăng nhập SSH bằng khóa thành công, với thông báo Authenticating with public key "lecongdat-lab1" from agent; lệnh whoami trả về lecongdat.

## Video thực hành
https://youtu.be/-jb1mOBQ0VM
