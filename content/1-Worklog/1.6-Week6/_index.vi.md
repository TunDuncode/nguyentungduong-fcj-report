---
title: "6. Viết Lambda netmon-api và truy vấn DynamoDB"
date: 2026-09-26T09:00:00+07:00
weight: 6
draft: false
description: "Viết Lambda netmon-api và truy vấn DynamoDB"
---

# 6. Viết Lambda netmon-api và truy vấn DynamoDB

### Mục tiêu tuần 6:

- Tạo Lambda Python làm backend không cần máy chủ riêng.
- Đọc danh sách thiết bị từ NetworkDevices bằng boto3.
- Biết kiểm tra IAM execution role, CloudWatch Logs và statusCode.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Tạo/kiểm tra hàm netmon-api, runtime Python và execution role có quyền DynamoDB cần thiết. | 26/09/2026 | 26/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Chủ nhật (tự học) | Dùng boto3.resource("dynamodb") và table.scan() để đọc dữ liệu; xem LastEvaluatedKey cho phân trang. | 27/09/2026 | 27/09/2026 | [Boto3 DynamoDB Table](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb/table/index.html) |
| Thứ Hai (tự học) | Xử lý Decimal sang số JSON phù hợp và trả statusCode, headers, body. | 28/09/2026 | 28/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Thứ Ba (tự học) | Chạy Test event, xem kết quả và tìm lỗi trong CloudWatch Logs nếu không thấy dữ liệu. | 29/09/2026 | 29/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |

### Kết quả đạt được tuần 6:

- Tạo được luồng đọc thiết bị bằng **Lambda `netmon-api` → DynamoDB `NetworkDevices`**.
- Đã có mã xử lý phân trang `LastEvaluatedKey` và chuyển đổi kiểu số để trả JSON.
- Biết kiểm tra lỗi quyền truy cập bảng khi Lambda trả 500 thay vì suy đoán là lỗi giao diện.

