---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---



### Mục tiêu tuần 11:

* Triển khai thực tế kiến trúc hạ tầng chịu lỗi cao, tự co giãn tài nguyên và tự động điều phối tải.
* Thiết lập hoàn chỉnh bộ đôi giải pháp Application Load Balancer và Auto Scaling Groups chạy đa phân vùng (Lab 6).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - **Thực hành (Phần 1):** <br>&emsp; + Tạo một bản thiết kế EC2 Launch Template <br>&emsp; + Nhập shell script vào User Data để cài đặt sẵn máy chủ Apache | 17/10/2026 | 17/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - **Thực hành (Phần 2):** <br>&emsp; + Xây dựng một Target Group ánh xạ lưu lượng HTTP trên Cổng 80 <br>&emsp; + Khởi tạo một Application Load Balancer (ALB) hướng ra công cộng | 18/10/2026 | 18/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Thực hành (Phần 3):** <br>&emsp; + Khởi tạo một Auto Scaling Group (ASG) được liên kết với Launch Template <br>&emsp; + Phân bổ phạm vi hoạt động của ASG trên 2 Availability Zones (Vùng sẵn sàng) khác biệt | 19/10/2026 | 19/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành (Phần 4):** <br>&emsp; + Xác định các giới hạn dung lượng: Desired (Mong muốn) = 2, Min (Tối thiểu) = 2, Max (Tối đa) = 4 instances <br>&emsp; + Đăng ký cụm ASG với các trình theo dõi Health Check (Kiểm tra sức khỏe) đang hoạt động của ALB | 20/10/2026 | 20/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành (Phần 5):** <br>&emsp; + Mô phỏng một kịch bản thảm họa bằng cách chấm dứt thủ công một instance đang chạy <br>&emsp; + Giám sát hệ thống phát hiện lỗi và cấp phát một instance thay thế <br>&emsp; + Dọn dẹp hệ thống | 21/10/2026 | 21/10/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 11:

* Xây dựng và kiểm chứng thành công mô hình cơ sở hạ tầng tự sửa chữa (Self-healing infrastructure) trên môi trường Cloud:
  * Tự động hóa hoàn toàn quy trình khởi chạy máy chủ có cài đặt sẵn dịch vụ thông qua User Data kịch bản shell script
  * Phân phối lưu lượng đồng đều đến các máy ảo backend thông qua DNS duy nhất của ALB
  * ...

* Triển khai hoàn chỉnh khả năng chống chịu thảm họa vật lý ở quy mô Data Center:
  * Hệ thống hoạt động an toàn tuyệt đối nhờ cơ chế phân bổ máy ảo vắt chéo qua nhiều Availability Zones độc lập
  * Khi một vùng bị cô lập hoặc mất điện kết nối, vùng còn lại tự động gánh vác toàn bộ lưu lượng người dùng
  * ...

* Thực chứng năng lực vận hành co giãn đàn hồi tự động của Auto Scaling Groups:
  * Hệ thống phát hiện chính xác sự thiếu hụt máy chủ so với chỉ số mong muốn (Desired Capacity) khi có máy ảo bị phá hủy
  * Kích hoạt quy trình tạo mới, kiểm tra sức khỏe đạt chuẩn và tự động cấu hình đưa vào phân bổ tải của ALB mà không cần con người can thiệp
  * ...

* Nắm rõ quy trình thu hồi hệ thống co giãn phức tạp để tối ưu hạn mức sử dụng.
* ...