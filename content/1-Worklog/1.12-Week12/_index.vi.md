---
title: "Worklog Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---



### Mục tiêu tuần 12:

* Tiếp cận mô hình kiến trúc hiện đại Điện toán không máy chủ Serverless (AWS Lambda).
* Tổng kết toàn bộ lộ trình kiến thức thực tập và đóng gói hoàn thiện sản phẩm trang web báo cáo kết quả trực tuyến (Lab 7 & Wrap-up).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7   | - Tìm hiểu cơ chế điện toán serverless (không máy chủ) <br>&emsp; + Các tính năng cơ bản của AWS Lambda <br>&emsp; + Khái niệm Kiến trúc hướng sự kiện (Event-driven) <br>&emsp; + Amazon API Gateway | 24/10/2026 | 24/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật   | - **Thực hành (Phần 1):** <br>&emsp; + Lập trình một hàm AWS Lambda cơ bản sử dụng môi trường Python gốc <br>&emsp; + Thiết lập một Event Trigger (Trình kích hoạt sự kiện) tự động được ánh xạ tới các tệp tải lên Amazon S3 | 25/10/2026 | 25/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Thực hành (Phần 2):** <br>&emsp; + Tải các tệp lên S3 để kích hoạt quá trình thực thi <br>&emsp; + Truy cập nhật ký Amazon CloudWatch để xem chi tiết quá trình thực thi <br>&emsp; + Hoàn tất các thủ tục dọn dẹp tài nguyên cloud cuối cùng | 26/10/2026 | 26/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Xem xét và kiểm tra tất cả các tệp văn bản markdown (`.md`) đã biên soạn từ Tuần 1 đến Tuần 12 được lưu trữ bên trong các thư mục nội dung | 27/10/2026 | 27/10/2026      | |
| 4   | - Chạy các lệnh biên dịch tĩnh `hugo` gốc <br> - Đóng gói thư mục đầu ra `public` và thực thi thành công các quy trình triển khai lên cloud | 28/10/2026 | 28/10/2026      | |

### Kết quả đạt được tuần 12:

* Làm chủ tư duy xây dựng giải pháp công nghệ không máy chủ (Serverless Paradigm):
  * Hiểu cơ chế vận hành tối ưu chi phí tuyệt đối khi code chỉ chạy và tính tiền theo từng mili-giây khi có sự kiện kích hoạt kích duyệt
  * Loại bỏ hoàn toàn gánh nặng kỹ thuật về việc quản lý và cập nhật bản vá hệ điều hành cho máy chủ máy ảo nền
  * ...

* Triển khai xây dựng thành công ứng dụng tự động hóa hướng sự kiện:
  * Tạo lập hoàn chỉnh hàm xử lý tự động AWS Lambda bằng mã lệnh Python kết nối trực tiếp với cổng tài nguyên lưu trữ Amazon S3
  * Thành thục kỹ năng phân tích và giám sát gỡ lỗi hệ thống thông qua công cụ thu thập log tập trung Amazon CloudWatch
  * ...

* Hoàn thành trọn vẹn tiến trình xây dựng báo cáo chuyên nghiệp:
  * Hệ thống hóa toàn bộ chuỗi số liệu hoạt động, kiến thức kỹ thuật tích lũy xuyên suốt 12 tuần đồng hành cùng chương trình Cloud Journey
  * Biên dịch thành công mã nguồn thô sang trang web tài liệu tĩnh hoàn chỉnh bằng Hugo framework
  * Triển khai phân phối sản phẩm báo cáo lên môi trường mạng trực tuyến, tạo lập thành công đường link xem báo cáo trực quan gửi đến người hướng dẫn đánh giá nghiệm thu đợt thực tập
* ...