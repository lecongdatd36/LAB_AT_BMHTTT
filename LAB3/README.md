# LAB 3 – AN TOÀN VÀ BẢO MẬT HỆ THỐNG THÔNG TIN

## 1. Thông tin sinh viên

- Họ và tên: Lê Công Đạt
- MSSV: 1150080130
- Lớp: 11_ĐH_CNPM2
- Repository: LAB_AT_BMHTTT
- Thư mục bài thực hành: LAB3

## 2. Môi trường thực hành

- Máy thực hành: Máy ảo VMware
- Hệ điều hành: Windows
- Công cụ sử dụng: Microsoft Defender, Sysinternals, Wireshark và Python
- Phạm vi kiểm thử tải: Chỉ trên địa chỉ cục bộ `127.0.0.1:8080`

Thông tin phiên bản chi tiết của môi trường và các công cụ được trình bày trong báo cáo Word.

## 3. Cách dựng môi trường

1. Khởi động máy ảo Windows.
2. Kiểm tra Microsoft Defender đang hoạt động.
3. Chuẩn bị các công cụ cần thiết cho từng tình huống.
4. Cài đặt Python và Wireshark nếu tình huống yêu cầu.
5. Chỉ thực hiện kiểm thử trong máy ảo và trên địa chỉ cục bộ.
6. Lưu kết quả vào các thư mục `output` và `logs`.
7. Làm sạch thông tin nhạy cảm trước khi đưa tệp lên GitHub.
8. Tạo mã kiểm tra SHA-256 cho các tệp bằng chứng.

## 4. Các tình huống đã thực hiện

### TH1 – Nhận diện Asset, Vulnerability, Threat, Risk và Attack

- Xác định tài sản cần bảo vệ trong máy thực hành.
- Phân biệt lỗ hổng, mối đe dọa, rủi ro và hành vi tấn công.
- Phân loại các tình huống theo nguyên nhân.
- Kết quả: **PASS**

### TH2 – Kiểm tra Microsoft Defender bằng tệp EICAR

- Sử dụng tệp kiểm thử EICAR an toàn.
- Ghi nhận khả năng phát hiện và xử lý của Microsoft Defender.
- Không sử dụng mã độc thật và không tắt Defender để chạy mẫu.
- Kết quả: **PASS**

### TH3 – Quan sát tiến trình và kết nối hệ thống

- Sử dụng công cụ Sysinternals để quan sát tiến trình.
- Theo dõi hoạt động và kết nối liên quan trong máy thực hành.
- Thu thập output phục vụ phân tích.
- Kết quả: **PASS**

### TH4 – Quan sát lưu lượng mạng bằng Wireshark

- Thu thập lưu lượng mạng trong phạm vi máy thực hành.
- Áp dụng bộ lọc để tìm các gói tin cần quan sát.
- Lưu kết quả và ảnh bằng chứng.
- Kết quả: **PASS**

### TH5 – Kiểm thử tải cục bộ

- Chạy máy chủ thử nghiệm trên `127.0.0.1:8080`.
- Chỉ gửi yêu cầu đến máy cục bộ.
- Không chỉnh sửa chương trình để hướng đến hệ thống bên ngoài.
- Không thực hiện DDoS, mail bomb, spoofing hoặc MITM.
- Kết quả: **PASS**

## 5. Kết quả tổng hợp

| Tình huống | Nội dung | Kết quả |
|---|---|---|
| TH1 | Nhận diện các khái niệm an toàn thông tin | PASS |
| TH2 | Kiểm tra Defender bằng EICAR | PASS |
| TH3 | Quan sát tiến trình và kết nối | PASS |
| TH4 | Phân tích lưu lượng bằng Wireshark | PASS |
| TH5 | Kiểm thử tải trên localhost | PASS |

## 6. Lỗi gặp phải và cách khắc phục

- Không tìm thấy output sau khi chạy công cụ: kiểm tra lại thư mục lưu và thực hiện xuất kết quả đúng đường dẫn.
- Wireshark hiển thị nhiều gói tin: sử dụng bộ lọc để thu hẹp dữ liệu cần phân tích.
- Microsoft Defender cách ly tệp EICAR: đây là kết quả mong đợi; không khôi phục hoặc đưa tệp bị cách ly lên GitHub.
- Máy ảo hoạt động chậm: tắt các ứng dụng không cần thiết và điều chỉnh tài nguyên máy ảo.
- Một số log chứa thông tin máy thực hành: làm sạch tên máy, tên tài khoản, địa chỉ IP và dữ liệu nhạy cảm trước khi tải lên.

## 7. Cấu trúc thư mục

```text
LAB3/
├── README.md
├── LAB3_K11_CNPM2_1150080130_LECONGDAT.docx
├── evidence_sha256.csv
├── output/
└── logs/
## Link youtube : https://youtu.be/M1myTt6G09Q

