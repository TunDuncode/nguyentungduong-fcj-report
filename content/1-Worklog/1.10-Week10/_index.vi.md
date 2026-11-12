---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---



### Mục tiêu tuần 10:

* Tiếp thu sâu sắc các lý thuyết và giải pháp hạ tầng có khả năng tự phục hồi, chống chịu lỗi và tự động co giãn tài nguyên đám mây.
* Hiểu rõ cơ chế phối hợp hoạt động của hệ thống Cân bằng tải và Nhóm co giãn tự động.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Nghiên cứu các mô hình Elastic Load Balancing (ELB) <br>&emsp; + Application Load Balancer (ALB) xử lý lưu lượng Lớp 7 <br>&emsp; + Network Load Balancer (NLB) xử lý lưu lượng Lớp 4 | 10/10/2026 | 10/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Tìm hiểu sâu về các đơn vị cấu hình định tuyến <br>&emsp; + Thiết lập Target Groups (Nhóm mục tiêu) <br>&emsp; + Triển khai các hành vi quy tắc Health Check (Kiểm tra sức khỏe) liên tục | 11/10/2026 | 11/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Khám phá các khuôn khổ cấp phát năng lực tính toán tự động <br>&emsp; + Vai trò của Amazon EC2 Auto Scaling Groups (ASG) trong các kiến trúc | 12/10/2026 | 12/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Nghiên cứu các bản thiết kế tiêu chuẩn hóa cơ sở hạ tầng <br>&emsp; + Tạo Launch Templates (Mẫu khởi chạy) bất biến <br> - Phân tích các yếu tố kích hoạt chỉ số (metric triggers) thúc đẩy Scaling Policies (Chính sách mở rộng) động | 13/10/2026 | 13/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Xem xét các sách trắng doanh nghiệp (whitepapers) trình bày chi tiết cách các ứng dụng production vượt qua các nút thắt lưu lượng truy cập đột ngột bằng cách sử dụng các công cụ mở rộng tự động | 14/10/2026 | 14/10/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 10:

* Nắm vững các thuật ngữ cốt lõi và tiêu chuẩn thiết kế kiến trúc đám mây nâng cao:
  * Scalability (Tính mở rộng linh hoạt theo chiều ngang và chiều dọc)
  * High Availability (Tính sẵn sàng cao giúp ứng dụng hoạt động không ngừng nghỉ)
  * Elasticity (Tính đàn hồi tự động thu gom hoặc nhả tài nguyên theo tải thực tế)
  * ...

* Hiểu sâu sắc kỹ thuật phân phối luồng dữ liệu thông minh trên Internet:
  * Phân biệt rõ ALB xử lý định tuyến thông minh dựa trên URL/Path ở tầng ứng dụng và NLB tối ưu hiệu năng tốc độ siêu cao ở tầng mạng giao thức TCP
  * Cơ chế giám sát liên tục để cô lập các máy chủ lỗi thông qua định kỳ Health Checks
  * ...

* Thấu hiểu giải pháp nhân bản và quản lý cấu hình hệ thống đồng loạt tự động:
  * Sử dụng Launch Templates làm nền móng chuẩn hóa môi trường cho mọi máy ảo phát sinh mới
  * Nắm rõ cách thiết lập ngưỡng cảnh báo CPU/RAM để kích hoạt co giãn tự động hợp lý
* ...