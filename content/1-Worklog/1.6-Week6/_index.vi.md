---
title: "6. Tìm hiểu giám sát hạ tầng bằng CloudWatch và SNS"
date: 2026-09-26T09:00:00+07:00
weight: 6
draft: false
description: "Tìm hiểu giám sát hạ tầng bằng CloudWatch và SNS"
---

# 6. Tìm hiểu giám sát hạ tầng bằng CloudWatch và SNS

### Mục tiêu tuần 6:

- Hiểu vai trò của hệ thống giám sát tài nguyên AWS.
- Phân biệt chỉ số có sẵn của EC2 và chỉ số thu thập bổ sung.
- Tìm hiểu cách gửi thông báo khi tài nguyên vượt ngưỡng.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Tìm hiểu Amazon CloudWatch và cách xem các chỉ số CPU, lưu lượng mạng của EC2. | 26/09/2026 | 26/09/2026 | [EC2 CloudWatch metrics](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html) |
| Chủ nhật (tự học) | Đọc tài liệu về CloudWatch Agent để hiểu cách thu thập thêm chỉ số RAM và ổ đĩa. | 27/09/2026 | 27/09/2026 | [CloudWatch agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html) |
| Thứ Hai (tự học) | Tự học cách đặt ngưỡng CloudWatch Alarm và phân biệt trạng thái OK, ALARM, INSUFFICIENT_DATA. | 28/09/2026 | 28/09/2026 | [CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Alarms.html) |
| Thứ Ba (tự học) | Tìm hiểu SNS Topic, Subscription và quy trình xác nhận nhận thông báo qua email. | 29/09/2026 | 29/09/2026 | [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) |

### Kết quả đạt được tuần 6:

- Hiểu mục đích của CloudWatch trong theo dõi hoạt động máy chủ EC2.
- Biết vì sao chỉ số RAM và ổ đĩa cần cấu hình thu thập bổ sung.
- Nắm cơ chế kết hợp CloudWatch Alarm và SNS để gửi thông báo.

