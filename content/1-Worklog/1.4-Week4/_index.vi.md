---
title: "Worklog Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---




### Mục tiêu tuần 4:

* Khám phá các dịch vụ Cơ sở dữ liệu trên AWS.
* Tìm hiểu sự khác biệt giữa cơ sở dữ liệu quan hệ (RDS) và phi quan hệ (NoSQL).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Tìm hiểu Amazon RDS (Cơ sở dữ liệu quan hệ) <br>&emsp; + MySQL, PostgreSQL <br>&emsp; + Triển khai Multi-AZ <br>&emsp; + Read Replicas (Bản sao đọc) <br> | 29/08/2026   | 29/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Tìm hiểu Amazon DynamoDB (CSDL NoSQL) <br>&emsp; + Partition Keys (Khóa phân vùng) <br>&emsp; + Sort Keys (Khóa sắp xếp) <br>&emsp; + Provisioned vs On-demand (Cấp phát trước vs Theo nhu cầu) <br> | 30/08/2026   | 30/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Phân tích các trường hợp sử dụng RDS và DynamoDB <br> - Học cách thiết kế DB Subnet Groups (Nhóm Subnet cho DB) <br> | 31/08/2026   | 31/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành:** <br>&emsp; + Cấu hình Private Subnet cho DB <br>&emsp; + Tạo DB Security Group (chỉ cho phép lưu lượng từ EC2) <br> | 01/09/2026   | 01/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Khởi tạo RDS MySQL (Gói Free Tier) <br>&emsp; + SSH vào EC2 và kiểm tra kết nối Cơ sở dữ liệu <br>&emsp; + Dọn dẹp tài nguyên | 02/09/2026   | 02/09/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 4:

* Hiểu rõ ưu và nhược điểm của các loại cơ sở dữ liệu trên AWS:
  * Amazon RDS (Cơ sở dữ liệu quan hệ)
  * Amazon DynamoDB (Cơ sở dữ liệu phi quan hệ)
  * ...

* Nắm bắt cơ chế đảm bảo tính sẵn sàng cao (HA) cho Database:
  * Multi-AZ Failover
  * Read Replicas (Mở rộng năng lực đọc)

* Đã thiết lập thành công các nhóm mạng bảo mật dành riêng cho cơ sở dữ liệu:
  * DB Subnet Groups
  * Security Groups chặn truy cập Internet
  * ...

* Triển khai hoàn chỉnh môi trường cơ sở dữ liệu đám mây, bao gồm:
  * Khởi tạo máy chủ RDS MySQL
  * Kết nối an toàn từ tầng Application (EC2) sang tầng Database (RDS) thông qua MySQL CLI
  * ...

* Tự tay thực thi các truy vấn SQL cơ bản trên hệ thống DB đám mây được quản lý.
* ...