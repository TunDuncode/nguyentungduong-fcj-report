---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:

* Hiểu sâu về dịch vụ lưu trữ đối tượng toàn diện Amazon S3.
* Nắm vững các quy tắc quản lý vòng đời dữ liệu và chính sách bảo mật lưu trữ đám mây.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Tìm hiểu kiến trúc lưu trữ Amazon S3 <br>&emsp; + Cấu trúc nhận dạng Bucket & Object <br>&emsp; + Nguyên lý Key-Value của Object Storage (Lưu trữ đối tượng) <br> | 12/09/2026   | 12/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Tìm hiểu sâu về các Lớp lưu trữ S3 (Storage Classes) <br>&emsp; + S3 Standard <br>&emsp; + S3 Standard-IA <br>&emsp; + S3 Glacier (Instant/Flexible/Deep Archive) | 13/09/2026   | 13/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Tìm hiểu cơ chế bảo vệ và quản lý dữ liệu lớn <br>&emsp; + S3 Versioning (Tạo phiên bản) <br>&emsp; + Lifecycle Rules (Quy tắc vòng đời) <br> | 14/09/2026   | 14/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Phân biệt các cơ chế kiểm soát truy cập S3 <br>&emsp; + S3 Bucket Policies (Chính sách Bucket) <br>&emsp; + IAM Policies (Chính sách IAM) <br> - Chuẩn bị mã nguồn website tĩnh (HTML/CSS/JS) | 15/09/2026   | 15/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Nghiên cứu lý thuyết tối ưu chi phí lưu trữ tệp lớn <br> - Tóm tắt kiến trúc lưu trữ phi cấu trúc cho các mô hình hệ thống khác nhau | 16/09/2026   | 16/09/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:

* Phân biệt rõ ràng bản chất giữa hai nền tảng lưu trữ cốt lõi:
  * Object Storage (Amazon S3)
  * Block Storage (Amazon EBS)
  * ...

* Làm chủ kỹ thuật tối ưu hóa chi phí hệ thống dựa trên tần suất truy cập tệp tin qua S3 Storage Classes:
  * Lớp Standard dành cho dữ liệu truy cập thường xuyên
  * Lớp Infrequent Access (IA) tiết kiệm chi phí cho dữ liệu ít dùng
  * Lớp Glacier chuyên dụng cho việc lưu trữ lưu kho dài hạn
  * ...

* Hiểu rõ cơ chế quản lý và bảo vệ toàn vẹn tài nguyên trên Cloud:
  * Cơ chế S3 Versioning giúp khôi phục các tệp tin bị ghi đè hoặc xóa nhầm
  * Quy tắc Lifecycle Rules tự động hóa tiến trình chuyển lớp lưu trữ hoặc hủy tệp tin hết hạn
  * ...

* Nắm vững cách phân cấp và thực thi quyền hạn truy cập an toàn bảo mật:
  * Thiết lập S3 Bucket Policies áp dụng trực tiếp cho tài nguyên chứa
  * Kết hợp IAM Policies phân quyền chi tiết cho định danh người dùng