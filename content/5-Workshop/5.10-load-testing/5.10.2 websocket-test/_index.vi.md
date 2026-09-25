---
title: "4.9.2. WebSocket Test"
weight: 492
---

# 4.9.2. Stress Test Luồng WebSocket Real-time

Sinh viên sử dụng công cụ **Artillery** gõ từ máy tính cá nhân bắn gói tin trực tiếp vào địa chỉ **DNS của ALB** để giả lập cuộc tấn công tải đỉnh: **1.000 người chơi ảo** kết nối cùng 1 giây và gửi liên tiếp **46.500 tin nhắn** WebSocket real-time.

```text
Summary report
errors.Unexpected server response: 504: ....... 140
vusers.created: ............................... 1000
vusers.failed: ................................ 70
websocket.messages_sent: ...................... 46500
websocket.send_rate: .......................... 1629/sec
Total time: 35 seconds
```

### 🔬 Phân tích bản chất Kỹ thuật chuyên sâu (Điểm nhấn Báo cáo)
1.  **Hiệu năng xử lý**: Hệ thống duy trì băng thông truyền tải cực lớn, đạt mốc xử lý trung bình vọt đỉnh lên đến **1.629 tin nhắn/giây** (`websocket.send_rate`).
2.  **Bản chất xuất hiện lỗi 504**: Do kịch bản dồn 1.000 user ập vào cùng một thời điểm cực ngắn (Spike Traffic), container đơn lẻ ban đầu bị quá tải cục bộ, dẫn đến nghẽn hàng đợi kết nối (Socket backlog pool). ALB gửi yêu cầu bắt tay nâng cấp giao thức nhưng container phản hồi chậm quá thời gian quy định, sinh ra **140 lỗi mạng hệ thống `504 Gateway Timeout`** và làm rớt `70` kết nối người chơi ban đầu.
3.  **Hành động giải cứu của Auto Scaling**: Ngay khi lỗi 504 xuất hiện làm CPU Utilization chạm ngưỡng báo động đỏ (>70%), hệ thống tự động sinh thêm Task mới. Ở các chu kỳ giây cuối, khi Task mới chạy ổn định, số lượng `vusers.failed` **lập tức quay về bằng 0**, bảo vệ an toàn cho 930 người chơi còn lại hoàn thành phiên tương tác game mượt mà.

![Đồ thị Active Connections của ALB bắn vọt lên cột mốc cao khi stress test](/images/4.9.2-websocket-test.png)
