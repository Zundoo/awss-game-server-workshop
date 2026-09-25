---
title: "4.3.2. Redis"
weight: 432
---

# 4.3.2. Cấu hình Cụm bộ nhớ đệm ElastiCache Redis

*   **Mục tiêu**: Triển khai cụm **Amazon ElastiCache Redis** (chạy cổng `6379`) để gánh vác toàn bộ dữ liệu Session và đồng bộ hóa logic phòng game real-time đa máy chủ.

### 🛠️ Nhật ký Sửa lỗi Thực tế: Khắc phục sự cố treo mạng (Timeout) do mã hóa đường truyền TLS
*   **Hiện tượng lỗi**: Khi đứng trên máy chủ EC2 thực hiện kiểm tra đường truyền nội bộ bằng câu lệnh tiêu chuẩn: `redis6-cli -h ://amazonaws.com -p 6379`, terminal rơi vào trạng thái **treo vô hạn (Hanging)** rồi tự động ngắt kết nối mà không xuất hiện mã lỗi.
*   **Phân tích nguyên nhân**: Cụm ElastiCache khi khởi tạo đã kích hoạt chế độ **Encryption in-transit (TLS)** theo tiêu chuẩn an toàn bảo mật dữ liệu. Cơ chế này ép buộc toàn bộ gói tin đi vào phải thực hiện bắt tay mã hóa an toàn. Các kết nối dạng văn bản thuần (Plaintext) phát đi từ lệnh CLI thông thường sẽ bị hệ thống âm thầm chặn đứng và loại bỏ để bảo vệ an toàn.
*   **Giải pháp xử lý triệt để**:
    1. Bổ sung cờ bảo mật mã hóa đường truyền **`--tls`** vào cuối lệnh chạy trên Terminal của EC2:
       ```bash
       redis6-cli -h ://amazonaws.com -p 6379 --tls
       ```
       *Kết quả*: Hệ thống kết nối thông suốt ngay lập tức dưới 1ms, lệnh gõ `ping` phản hồi `PONG` hoàn hảo.
    2. Đồng bộ hóa mã nguồn kết nối của Game Server (`server.js`) bằng cách kích hoạt thuộc tính chứng chỉ bảo mật client sang trạng thái `ssl: true` hoặc sử dụng giao thức chuỗi kết nối an toàn `rediss://`.
