---
title: "4. EC2 Ubuntu, EBS và giám sát cơ bản"
date: 2026-09-12T09:00:00+07:00
weight: 4
draft: false
description: "EC2 Ubuntu, EBS và giám sát cơ bản"
---

# 4. EC2 Ubuntu, EBS và giám sát cơ bản

### Mục tiêu tuần 4:

- Hiểu các bước khởi tạo EC2 phục vụ hệ thống NetMon.
- Biết vai trò của AMI, instance type, EBS và IAM Role.
- Phân biệt CPU mặc định của EC2 với RAM/disk cần CloudWatch Agent.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Theo dõi Tùng Dương cấu hình netmon-ec2-server bằng Ubuntu 24.04 LTS. | 12/09/2026 | 12/09/2026 | [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| Chủ nhật (tự học) | Tìm hiểu EBS root volume, Security Group, trạng thái instance và 2/2 hay 3/3 health checks tùy giao diện. | 13/09/2026 | 13/09/2026 | [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html) |
| Thứ Hai (tự học) | Kiểm tra cách gán IAM Role sau khi tạo EC2 và xem Metrics trên CloudWatch. | 14/09/2026 | 14/09/2026 | [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| Thứ Ba (tự học) | Thảo luận các trường liên hệ EC2 với bản ghi thiết bị như instanceId, region và monitoringSource. | 15/09/2026 | 15/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Kết quả đạt được tuần 4:

- Hiểu quá trình khởi tạo máy chủ netmon-ec2-server và những yếu tố ảnh hưởng đến chi phí.
- Biết CPUUtilization là chỉ số có sẵn, còn RAM/disk cần thu thập bổ sung tùy cấu hình.
- Thống nhất không gộp số liệu giả lập và số liệu EC2 thành một chỉ số thiếu nguồn gốc.

