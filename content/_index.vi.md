---
title : "Thiết lập tài khoản AWS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
---

# Tạo tài khoản AWS đầu tiên của bạn

#### Tổng quan
Trong bài thực hành đầu tiên này, bạn sẽ tiến hành tạo một tài khoản **AWS** hoàn toàn mới và thiết lập Xác thực đa yếu tố (**MFA**) nhằm tăng cường tính bảo mật cho tài khoản. Tiếp theo, bạn sẽ tạo một **Nhóm Quản trị viên (Administrator Group)** và **Người dùng Admin (Admin User)** để quản lý quyền truy cập vào các tài nguyên trong hệ thống thay vì sử dụng tài khoản root. 
Cuối cùng, chúng ta sẽ đi qua các bước xác thực tài khoản với bộ phận **AWS Support** để xử lý trong trường hợp bạn gặp phải sự cố về lỗi xác thực.

#### Tài khoản AWS (AWS Account)
**Tài khoản AWS** là một vùng chứa cơ bản (basic container) cho tất cả các tài nguyên AWS mà bạn có thể khởi tạo với tư cách là khách hàng của AWS. Theo mặc định, mỗi tài khoản AWS sẽ sở hữu một *tài khoản root (root user)*. *Tài khoản root* này có toàn quyền truy cập cao nhất trong hệ thống AWS của bạn và các đặc quyền của nó không thể bị giới hạn. Khi mới tạo tài khoản lần đầu tiên, bạn sẽ truy cập vào hệ thống dưới danh nghĩa là *tài khoản root*.

![Create Account](/images/1/0001.png?featherlight=false&width=90pc)

{{% notice note %}}
Theo các thực hành tốt nhất về bảo mật (best practices), tuyệt đối không sử dụng *tài khoản root* của AWS cho bất kỳ tác vụ nào nếu không thực sự bắt buộc. Thay vào đó, hãy tạo một người dùng IAM mới cho mỗi cá nhân cần quyền quản trị. Sau đó, những người dùng thuộc nhóm quản trị viên này sẽ chịu trách nhiệm thiết lập các nhóm người dùng, người dùng thành viên khác, v.v., cho tài khoản AWS. Mọi tương tác trong tương lai nên được thực hiện qua tài khoản định danh IAM và các cặp khóa (keys) riêng thay vì dùng tài khoản root. Tuy nhiên, đối với một số tác vụ quản lý tài khoản và dịch vụ đặc biệt, bạn vẫn bắt buộc phải đăng nhập bằng thông tin xác thực root.
{{% /notice %}}

#### Xác thực đa yếu tố (MFA)
**MFA** bổ sung thêm một lớp bảo mật nghiêm ngặt vì nó yêu cầu người dùng phải cung cấp một mã xác thực duy nhất từ thiết bị hoặc cơ chế MFA được AWS hỗ trợ, bên cạnh thông tin đăng nhập mật khẩu thông thường mỗi khi truy cập vào các trang web hoặc dịch vụ của AWS.

#### Nhóm người dùng IAM (IAM User Group)
Một **nhóm người dùng IAM** là một tập hợp gồm nhiều người dùng IAM thành viên. Nhóm người dùng cho phép bạn chỉ định và phân quyền đồng thời cho nhiều người cùng lúc, giúp việc quản lý các quyền truy cập trở nên dễ dàng và tập trung hơn. Bất kỳ người dùng nào được thêm vào nhóm đó sẽ tự động kế thừa các quyền đã được gán cho nhóm.

#### Người dùng IAM (IAM User)
Một **người dùng IAM** là một thực thể mà bạn tạo ra trên AWS để đại diện cho một cá nhân hoặc một ứng dụng cụ thể sử dụng nó nhằm tương tác với các dịch vụ AWS. Một người dùng trên AWS bao gồm một tên định danh và thông tin xác thực đi kèm. 
Vui lòng lưu ý rằng một người dùng IAM có quyền quản trị viên (administrator) không có nghĩa là tài khoản root của hệ thống AWS.

#### Bộ phận hỗ trợ AWS (AWS Support)
Gói hỗ trợ cơ bản AWS Basic Support cung cấp cho tất cả khách hàng quyền truy cập miễn phí vào Trung tâm tài nguyên, Bảng điều khiển trạng thái dịch vụ (Service Health Dashboard), Câu hỏi thường gặp về sản phẩm, Diễn đàn thảo luận và Hỗ trợ kiểm tra sức khỏe hệ thống (Health Checks). Khách hàng có nhu cầu hỗ trợ chuyên sâu hơn có thể đăng ký các gói AWS Support trả phí ở các cấp độ Developer, Business, hoặc Enterprise.

Khi sử dụng các gói AWS Support, khách hàng sẽ nhận được sự hỗ trợ trực tiếp một đối một và phản hồi nhanh chóng từ các kỹ sư AWS. Dịch vụ này giúp khách hàng vận hành hiệu quả các tính năng và sản phẩm của AWS. Với chính sách thanh toán theo từng tháng và không giới hạn số lượng yêu cầu hỗ trợ (cases), khách hàng hoàn toàn được giải phóng khỏi các cam kết dài hạn. Bất kỳ khi nào gặp sự cố vận hành hoặc có câu hỏi kỹ thuật, khách hàng đều có thể kết nối với đội ngũ kỹ sư hỗ trợ để nhận được phản hồi trong thời gian cam kết cùng sự trợ giúp cá nhân hóa.

#### Nội dung chính

1. [Worklog](1-Worklog/)
2. [Proposal](2-Proposal/)
3. [Event](3-Event/)
4. [Blogs Posted](4-BlogsPosted/)
5. [Workshop](5-Workshop/)
6. [Self-Assessment](6-Self-Assessment/)
7. [Sharing and Feedback](7-Sharing-and-Feedback/)

