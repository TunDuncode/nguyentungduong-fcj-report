---
title: "Worklog Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---


### Mục tiêu tuần 9:

* Khởi tạo máy chủ cơ sở dữ liệu đám mây hoạt động độc lập và bảo mật an toàn sâu trong mạng nội bộ.
* Thực hành thiết lập kết nối an toàn đa tầng kiến trúc từ máy chủ ứng dụng đến cơ sở dữ liệu (Lab 5).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Nghiên cứu cấu hình nhóm mạng an toàn cho lớp DB <br>&emsp; + Thiết lập DB Subnet Groups (Nhóm Subnet cho DB) bị cô lập bên trong các Private Subnet | 03/10/2026 | 03/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Cấu hình các quy tắc tường lửa bảo vệ lớp Cơ sở dữ liệu <br>&emsp; + Tạo DB Security Groups (Nhóm bảo mật DB) <br>&emsp; + Chỉ cho phép lưu lượng đầu vào từ Web/App Security Group | 04/10/2026 | 04/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Thực hành (Phần 1):** <br>&emsp; + Khởi tạo một Instance Amazon RDS MySQL sử dụng hạn mức gói Free Tier <br>&emsp; + Liên kết các DB Subnet Groups và Security Groups đã chuẩn bị vào instance | 05/10/2026 | 05/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành (Phần 2):** <br>&emsp; + Kết nối an toàn qua SSH vào môi trường máy chủ EC2 Bastion Host <br>&emsp; + Cài đặt các công cụ MySQL CLI gốc cục bộ trên máy chủ EC2 | 06/10/2026 | 06/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành (Phần 3):** <br>&emsp; + Thiết lập kết nối nội bộ từ EC2 đến RDS Endpoint <br>&emsp; + Chạy các thao tác SQL cơ bản (CREATE TABLE, INSERT, SELECT) <br>&emsp; + Dọn dẹp tài nguyên để tránh phát sinh thêm chi phí | 07/10/2026 | 07/10/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 9:

* Đã cấu hình và vận hành thành công kiến trúc bảo mật phân tầng (Multi-tier Infrastructure):
  * Tầng Database được giấu hoàn toàn trong phân vùng mạng kín Private Subnet
  * Chặn đứng mọi nỗ lực quét cổng hoặc dò tìm thông tin từ môi trường mạng ngoài Internet
  * ...

* Làm chủ kỹ năng cấu hình tường lửa lớp dữ liệu tinh gọn nâng cao:
  * Tạo lập thành công liên kết an toàn giữa DB Subnet Groups đa vùng
  * Áp dụng thành công luật lọc gói tin chỉ cho phép cổng dịch vụ tiêu chuẩn (Port 3306) kết nối từ tầng máy chủ Web chỉ định
  * ...

* Thành thục kỹ năng quản trị dòng lệnh điều khiển hệ thống từ xa:
  * Sử dụng thành công công cụ terminal máy chủ Linux kết nối xuyên suốt đến dịch vụ quản lý đám mây
  * Khởi tạo bảng dữ liệu và ghi đọc kiểm tra chất lượng kết nối thành công qua MySQL CLI
  * ...

* Hiểu rõ tầm quan trọng của việc thu hồi tài nguyên thực hành (RDS snapshot/termination) để tối ưu hóa hạn mức tài khoản.
* ...