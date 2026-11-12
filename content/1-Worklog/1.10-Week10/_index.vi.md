---
title: "10. Phối hợp CloudWatch, SNS, EventBridge và lưu lịch sử cảnh báo"
date: 2026-10-31T09:00:00+07:00
weight: 10
draft: false
description: "Phối hợp CloudWatch, SNS, EventBridge và lưu lịch sử cảnh báo"
---

# 10. Phối hợp CloudWatch, SNS, EventBridge và lưu lịch sử cảnh báo

### Mục tiêu tuần 10:

- Hiểu luồng CloudWatch Alarm → SNS email và EventBridge → Lambda → DynamoDB.
- Phối hợp với phần giám sát do Mạnh Quân phụ trách.
- Kiểm tra lưu bản ghi cảnh báo và phân biệt trạng thái thử nghiệm.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Rà soát ba alarm CPU, RAM và disk: ngưỡng 80%, 80% và 85% theo cấu hình thử nghiệm. | 31/10/2026 | 31/10/2026 | [CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Alarms.html) |
| Chủ nhật (tự học) | Xem SNS topic netmon-alerts và email subscription đã xác nhận; thử cảnh báo có kiểm soát. | 01/11/2026 | 01/11/2026 | [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) |
| Thứ Hai (tự học) | Theo dõi rule netmon-alarm-state-rule nhận Alarm State Change từ CloudWatch. | 02/11/2026 | 02/11/2026 | [CloudWatch events and EventBridge](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-and-eventbridge.html) |
| Thứ Ba (tự học) | Kiểm tra Lambda netmon-save-alert và quyền PutItem tới NetworkAlerts để lưu thời điểm, tên alarm, trạng thái. | 03/11/2026 | 03/11/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Kết quả đạt được tuần 10:

- Có luồng cảnh báo kết hợp **CloudWatch, SNS, EventBridge và DynamoDB** trong thiết kế/triển khai nhóm.
- Xác nhận nhóm từng nhận email SNS và đã xử lý lỗi quyền `dynamodb:PutItem` khi ghi cảnh báo.
- Biết rằng việc đặt ngưỡng trên CloudWatch chưa chứng minh được cảnh báo cho dữ liệu thiết bị mô phỏng hoạt động hoàn toàn.

