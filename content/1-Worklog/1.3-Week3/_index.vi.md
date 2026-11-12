---
title: "Worklog Tuần 3"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Nắm vững các khái niệm về lưu trữ đối tượng với Amazon S3.
* Triển khai lưu trữ web tĩnh sử dụng CDN (CloudFront).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Tìm hiểu kiến thức cơ bản về Amazon S3 <br>&emsp; + Buckets & Objects <br>&emsp; + Storage Classes (Standard, IA, Glacier) <br>&emsp; + S3 Versioning <br> | 22/08/2026   | 22/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Tìm hiểu về Mạng phân phối nội dung (CDN) <br>&emsp; + Amazon CloudFront <br>&emsp; + Edge Locations <br>&emsp; + Origin Access Control (OAC) | 23/08/2026   | 23/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Hiểu về S3 Bucket Policies & IAM Policies <br> - Chuẩn bị mã nguồn website tĩnh (HTML/CSS) <br> | 24/08/2026   | 24/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành:** <br>&emsp; + Tạo S3 Bucket <br>&emsp; + Cấu hình Static Website Hosting <br>&emsp; + Tải lên các tệp HTML/CSS | 25/08/2026   | 25/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Cấu hình CloudFront để phân phối nội dung từ S3 <br>&emsp; + Chặn truy cập công khai trực tiếp vào S3 <br>&emsp; + Kiểm tra URL của CloudFront | 26/08/2026   | 26/08/2026     | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

* Phân biệt được sự khác nhau giữa lưu trữ Object (S3) và Block (EBS).
* Hiểu rõ cách tối ưu chi phí lưu trữ thông qua các S3 Storage Classes:
  * S3 Standard
  * S3 Infrequent Access (IA)
  * S3 Glacier
  

* Quản lý dữ liệu an toàn trên đám mây bằng các tính năng nâng cao:
  * S3 Versioning
  * Lifecycle Rules
  * S3 Bucket Policies

* Triển khai thành công Website tĩnh tốc độ cao trên quy mô toàn cầu, bao gồm:
  * Khởi tạo và upload tài nguyên lên S3
  * Cấu hình CDN thông qua CloudFront
  * Áp dụng OAC để bảo mật nguồn S3 gốc
  

* Hiểu cách truy xuất nội dung web an toàn thông qua domain của CloudFront.