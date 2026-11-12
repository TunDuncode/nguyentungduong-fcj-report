---
title: "5. Thiết kế DynamoDB cho thiết bị và lịch sử cảnh báo"
date: 2026-09-19T09:00:00+07:00
weight: 5
draft: false
description: "Thiết kế DynamoDB cho thiết bị và lịch sử cảnh báo"
---

# 5. Thiết kế DynamoDB cho thiết bị và lịch sử cảnh báo

### Mục tiêu tuần 5:

- Thiết kế khóa chính và thuộc tính cho dữ liệu thiết bị.
- Chuẩn bị cấu trúc nhật ký cảnh báo phục vụ Dashboard.
- Tìm hiểu đọc/ghi item qua AWS Console và boto3.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Thiết kế bảng NetworkDevices với deviceId (String) là Partition Key. | 19/09/2026 | 19/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Chủ nhật (tự học) | Thống nhất trường deviceName, deviceType, ipAddress, location, status, cpuUsage, memoryUsage và lastUpdated. | 20/09/2026 | 20/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Thứ Hai (tự học) | Phác thảo NetworkAlerts với eventId, alarmName, alarmState, eventTime và handlingStatus. | 21/09/2026 | 21/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Thứ Ba (tự học) | Thực hành kiểm tra item trên Explore table items, phân biệt kiểu String, Number và giá trị Decimal trong Python. | 22/09/2026 | 22/09/2026 | [Boto3 DynamoDB Table](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb/table/index.html) |

### Kết quả đạt được tuần 5:

- Có cấu trúc thống nhất cho bảng **NetworkDevices**; xác định khóa chính theo mã thiết bị.
- Chuẩn bị mô hình **NetworkAlerts** để lưu thời gian và trạng thái xử lý cảnh báo.
- Biết sử dụng **Explore table items** để xác nhận yêu cầu thêm/sửa có ghi thật vào DynamoDB hay không.

