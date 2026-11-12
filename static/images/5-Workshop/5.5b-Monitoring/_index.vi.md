---
title : "Giám sát & Logging"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.5b. </b> "
---

#### Mục tiêu

Thiết lập giám sát và logging để theo dõi trạng thái ứng dụng GameHub sau khi triển khai.

#### Nội dung chi tiết

- Bật CloudWatch Logs cho Lambda và API Gateway.
- Tạo metric filters cho lỗi và latency.
- Cấu hình alarm khi phát hiện sự cố.
- Gửi cảnh báo bằng SNS hoặc email.

#### Hướng dẫn từng bước

1. Mở CloudWatch Console.
2. Vào Logs > Log groups.
3. Chọn log group của Lambda hoặc API Gateway.
4. Tạo metric filter cho các mẫu lỗi như `ERROR` hoặc HTTP `5xx`.
5. Tạo alarm dựa trên metric filter.

#### Gợi ý cảnh báo

- Lambda error rate vượt 1% trong 5 phút.
- API Gateway `5xx` rate vượt 5% trong 5 phút.
- CodePipeline deployment fail.

#### Kết nối thông báo

- Dùng SNS topic để gửi email hoặc Slack.
- Đặt tên alarm rõ ràng, ví dụ `GameHub-Lambda-Error-Alarm`.
- Kiểm tra dashboard CloudWatch định kỳ.

Note (hình ảnh): Thêm ảnh `cloudwatch-alarms.png` vào `images/5-Workshop/5.5b-Monitoring/`.
