---
title: "4.9.1. HTTP Test"
weight: 491
---

# 4.9.1. Kiểm tra Tải luồng HTTP Health Check

*   **Mục tiêu**: Đánh giá khả năng chịu tải phản hồi của API tĩnh `/health` khi phải tiếp nhận hàng loạt yêu cầu thăm dò liên tục từ bộ cân bằng tải.
*   **Kết quả thử nghiệm**: Đường truyền HTTP phản hồi ổn định với thời gian phản hồi (Response Time) trung bình cực thấp dưới 5ms, mã trạng thái `200 OK` đạt tỷ lệ tuyệt đối 100%, xác nhận cấu hình API cấu trúc gọn nhẹ, hoạt động hiệu quả.
