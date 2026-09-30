---
title : "Load Testing"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.2.6 </b> "
---

## Load Testing

Phần này hướng dẫn cách thực hiện kiểm thử tải hệ thống để đánh giá khả năng chịu tải, tính ổn định và hiệu năng của hạ tầng Game Server khi có số lượng người dùng kết nối qua giao thức WebSocket và HTTP thông qua công cụ kiểm thử tải chuyên dụng.

### 1. Test Objective

Mục tiêu kiểm thử nhằm xác định giới hạn và hành vi của hệ thống dưới áp lực lưu lượng, cụ thể bao gồm:
* Xác thực khả năng chịu tải: Kiểm tra hệ thống có đáp ứng tốt và xử lý mượt mà lượng yêu cầu lớn gửi đến đồng thời hay không.
* Đánh giá độ trễ: Đảm bảo thời gian phản hồi (Target Response Time) của các thông điệp WebSocket và API HTTP nằm trong ngưỡng cho phép và ổn định.
* Kiểm tra tính toàn vẹn của dữ liệu: Xác nhận các kết nối từ công cụ kiểm thử tải được ghi nhận đầy đủ tại hệ thống máy chủ và lưu lại nhật ký chính xác.
* Giám sát hệ thống: Sử dụng bộ công cụ giám sát tích hợp sẵn của AWS để theo dõi hành vi của bộ cân bằng tải ALB và Log Streams.

### 2. Test Configuration

Sử dụng công cụ kiểm thử tải mã nguồn mở **Artillery** để tạo kịch bản mô phỏng hành vi người chơi và gửi các thông điệp liên tục tới máy chủ:
* Công cụ sử dụng: **Artillery**.
* Kịch bản hành vi: Khởi tạo luồng kết nối liên tục, gửi thông điệp giả lập dạng chuỗi ký tự (`hello from Artillery!`) qua bộ cân bằng tải Application Load Balancer để kiểm tra hiệu năng xử lý thời gian thực.

### 3. Test Architecture

Hệ thống hạ tầng phục vụ và ghi nhận quá trình kiểm thử tải bao gồm:
* Máy phát tải (Load Generator): Máy ảo thực thi kịch bản Artillery tạo tải và gửi dữ liệu giả lập tới Application Load Balancer (ALB).
* Application Load Balancer (`alb-game-server`): Tiếp nhận lưu lượng, phân phối các request tới Target Group chạy ứng dụng Game Server trong mạng nội bộ.
* Amazon CloudWatch Logs: Thu thập toàn bộ log sự kiện (Log events) từ Game Server thông qua Log stream chuyên dụng (`game-server-stream`) để phục vụ quá trình dò lỗi và kiểm tra kết quả.

### 4. Test Execution

Quy trình thực hiện bài kiểm thử tải được tiến hành theo các bước sau:
1. Thực thi câu lệnh chạy kịch bản Artillery từ máy phát tải hướng thẳng mục tiêu về DNS Name của ALB (`://amazonaws.com`).
2. Trong quá trình chạy test, truy cập vào giao diện quản trị **EC2 > Load Balancers > alb-game-server**, chọn tab **Monitoring** để theo dõi trực tiếp các chỉ số thời gian thực.

![Giám sát các chỉ số thời gian thực của Load Balancer tại tab Monitoring](images/5/5.6/testalb.png?featherlight=false&width=90pc)

3. Song song với đó, truy cập vào **CloudWatch > Log management > /aws/gameserver/logs > game-server-stream** để xác nhận máy chủ nhận được dữ liệu.

### 5. Test Results

Hệ thống ghi nhận kết quả kiểm thử tải thông qua việc tiếp nhận và xử lý thành công toàn bộ dữ liệu, chứng minh qua nhật ký hệ thống:
* Hệ thống nhận đầy đủ gói tin truyền tải từ Artillery mà không gặp hiện tượng mất mát gói tin hoặc ngắt kết nối giữa chừng.
* Nội dung thông điệp kiểm thử hiển thị đồng bộ, rõ ràng theo chuỗi thời gian thực.

### 6. CloudWatch Monitoring & Logging

Trong suốt quá trình kiểm thử tải, các chỉ số và dữ liệu hạ tầng trên Amazon CloudWatch ghi nhận như sau:

* **Log Events:** Tại màn hình Log events của luồng `game-server-stream`, hệ thống liên tục in ra các dòng thông báo chứng minh kết nối thành công:

![Log events của luồng game-server-stream ghi nhận dữ liệu truyền tải từ Artillery](images/5/5.8/cloudlog2.png?featherlight=false&width=90pc)

* **Requests Count:** Biểu đồ lượng Request trên ALB ghi nhận một đợt tăng trưởng đột biến mạnh mẽ, đạt đỉnh với giá trị cao nhất khoảng **813 requests** tại thời điểm phát tải tập trung, sau đó hạ dần khi bài test kết thúc.

![Biểu đồ lượng Request trên bộ cân bằng tải ALB đạt mốc đỉnh điểm 813 kết nối](images/5/5.6/test2.png?featherlight=false&width=90pc)

* **Target Response Time:** Đồ thị thời gian phản hồi đích (Target Response Time) duy trì vô cùng ổn định. Ngoài mốc khởi đầu đạt ngưỡng cao nhất khoảng 16.7 giây do cơ chế khởi động kết nối ban đầu, phần lớn thời gian xử lý các request đều nằm ở mức vô cùng thấp (gần chạm ngưỡng 0 giây), đảm bảo trải nghiệm mượt mà.

![Đồ thị thời gian phản hồi Target Response Time duy trì ổn định ở mức an toàn](images/5/5.6/test3.png?featherlight=false&width=90pc)

### 7. Performance Analysis

Dựa trên dữ liệu trực quan thu được từ hệ thống giám sát CloudWatch và biểu đồ ALB:
* Hiệu năng xử lý: Bộ cân bằng tải `alb-game-server` hoàn thành xuất sắc nhiệm vụ tiếp nhận và điều phối lượng request tăng đột biến (~813 count) mà không gây ra hiện tượng quá tải hay treo dịch vụ.
* Phân tích độ trễ: Đồ thị phản hồi ghi nhận một điểm đột biến lên tới **16.7 giây** ngay khi loạt kết nối đầu tiên được khởi tạo (Cold Start / Handshake latency). Tuy nhiên, hệ thống đã nhanh chóng tự điều chỉnh, đưa độ trễ của toàn bộ các luồng request tiếp theo về mức tiệm cận 0 giây, chứng minh khả năng tối ưu hóa luồng dữ liệu thời gian thực rất tốt.

### 8. Conclusion

Bài kiểm thử tải với **Artillery** đã diễn ra thành công tốt đẹp. Hạ tầng mạng, bộ cân bằng tải ALB và cấu hình ứng dụng Game Server đáp ứng hoàn hảo áp lực tải đột biến, xử lý thông điệp chính xác và duy trì độ trễ tối ưu. Hệ thống đã sẵn sàng cho giai đoạn đưa vào vận hành thực tế.
