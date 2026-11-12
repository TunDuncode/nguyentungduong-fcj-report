---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---



### Mục tiêu tuần 8:

* Nghiên cứu sâu toàn diện các dịch vụ giải pháp Cơ sở dữ liệu của hạ tầng AWS.
* Phân tích thiết kế cấu trúc dữ liệu và chuẩn bị kiến trúc phân vùng lưu trữ cho hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Nghiên cứu kiến trúc Amazon RDS (Cơ sở dữ liệu quan hệ) <br>&emsp; + Các Engine Cơ sở dữ liệu hỗ trợ (MySQL, PostgreSQL) <br>&emsp; + Các tính năng quản lý nền tảng tự động | 26/09/2026 | 26/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Nghiên cứu các mô hình Tính sẵn sàng cao (HA) cho lưu trữ dữ liệu <br>&emsp; + Triển khai Multi-AZ (Sao chép dữ liệu đồng bộ) <br>&emsp; + Read Replicas (Mở rộng theo chiều ngang cho các khối lượng công việc đọc) | 27/09/2026 | 27/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Tìm hiểu các tùy chọn cơ sở dữ liệu NoSQL phi quan hệ <br>&emsp; + Các thành phần cốt lõi của Amazon DynamoDB <br>&emsp; + Các khái niệm chính về Partition Keys (Khóa phân vùng) và Sort Keys (Khóa sắp xếp) <br>&emsp; + Chế độ dung lượng Provisioned (Cấp phát trước) so với On-demand (Theo nhu cầu) | 28/09/2026 | 28/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Phân tích các trường hợp sử dụng thực tế để đánh giá khi nào nên chọn RDS hay DynamoDB <br> - Phác thảo một mẫu lược đồ cơ sở dữ liệu quan hệ logic mẫu | 29/09/2026 | 29/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Nghiên cứu các nguyên tắc cách ly mạng để bảo mật an toàn cho cơ sở dữ liệu trên cloud <br> - Hiểu các chức năng cơ bản của DB Subnet Groups (Nhóm Subnet cho DB) | 30/09/2026 | 30/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
### Kết quả đạt được tuần 8:

* Phân biệt sâu sắc các mô hình kiến trúc lưu trữ dữ liệu có cấu trúc và phi cấu trúc đám mây:
  * Amazon RDS phù hợp cho các truy vấn quan hệ phức tạp cần tính toàn vẹn cao (ACID)
  * Amazon DynamoDB đáp ứng các ứng dụng quy mô lớn cần độ trễ micro-second ổn định
  * ...

* Nắm vững các mô hình thiết kế đảm bảo dữ liệu không bị gián đoạn hoạt động:
  * Mô hình Multi-AZ tự động chuyển đổi dự phòng (Failover) khi có thảm họa phần cứng
  * Mô hình Read Replicas phân tách tải, tăng tốc độ xử lý cho các hệ thống đọc nhiều
  * ...

* Hiểu rõ cơ chế bảo mật và quản lý tệp lưu trữ sao lưu tự động (Automated Snapshots).
* Thiết kế thành công lược đồ dữ liệu logic, xác định rõ ràng luồng liên kết thực thể phù hợp để chuẩn bị triển khai lên cloud thực tế.
* ...