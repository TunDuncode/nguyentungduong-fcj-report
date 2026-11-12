---
title: "Worklog Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---



### Mục tiêu tuần 7:

* Triển khai hệ thống lưu trữ Website tĩnh có tính sẵn sàng cao và bảo mật nghiêm ngặt.
* Tích hợp thành công mạng phân phối nội dung toàn cầu Amazon CloudFront (CDN) kết hợp S3 (Lab 4).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Tìm hiểu về Mạng phân phối nội dung toàn cầu (CDN) <br>&emsp; + Kiến thức cơ bản về Amazon CloudFront <br>&emsp; + Cơ chế bộ nhớ đệm (Caching) và các Edge Locations (Vị trí biên) | 19/09/2026 | 19/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - Nghiên cứu các tính năng bảo mật nâng cao cho nguồn (origin) của CDN <br>&emsp; + Kiểm soát truy cập nguồn (OAC) <br> - Thiết kế luồng lưu lượng để chặn truy cập công khai trực tiếp vào kho lưu trữ đối tượng | 20/09/2026 | 20/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Thực hành (Phần 1):** <br>&emsp; + Tạo Amazon S3 Bucket với cấu hình riêng tư <br>&emsp; + Bật tính năng Lưu trữ trang web tĩnh (Static Website Hosting) <br>&emsp; + Tải lên các tệp nguồn tĩnh (HTML/CSS/JS) | 21/09/2026 | 21/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành (Phần 2):** <br>&emsp; + Tạo Phân phối CloudFront trỏ đến nguồn (origin) S3 <br>&emsp; + Cấu hình các thiết lập Kiểm soát truy cập nguồn (OAC) an toàn | 22/09/2026 | 22/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành (Phần 3):** <br>&emsp; + Cập nhật S3 Bucket Policy để chỉ cấp quyền truy cập rõ ràng cho CloudFront OAC <br>&emsp; + Xác minh việc chặn truy cập trực tiếp <br>&emsp; + Truy cập trang web thông qua tên miền CloudFront bảo mật | 23/09/2026 | 23/09/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 7:

* Làm chủ tư duy và cơ chế vận hành mạng phân phối nội dung CDN:
  * Sử dụng hệ thống Edge Locations giảm thiểu tối đa độ trễ phản hồi cho người dùng toàn cầu
  * Hiểu rõ cơ chế phân phối dữ liệu từ máy chủ gốc (Origin) đến các điểm lưu đệm biên
  * ...

* Đã xây dựng và triển khai thành công mô hình Static Website Hosting trên môi trường production thực tế, bao gồm:
  * Đóng gói mã nguồn web tĩnh và đẩy lên Amazon S3 bảo mật
  * Cấu hình CloudFront Distribution thiết lập định tuyến luồng traffic
  * ...

* Thiết lập tường lửa bảo mật dữ liệu nguồn ở mức độ cao:
  * Cấu hình thành công cơ chế Origin Access Control (OAC) mã hóa định danh
  * Chỉnh sửa S3 Bucket Policy nhằm từ chối mọi yêu cầu truy xuất trực tiếp từ Internet
  * ...

* Đạt khả năng phân tích luồng mạng, đảm bảo tệp tin ứng dụng web được cache tối ưu và vận hành trơn tru qua link domain an toàn.
* ...