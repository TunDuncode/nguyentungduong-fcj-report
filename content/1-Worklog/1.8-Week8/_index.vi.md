---
title: "8. Xử lý CRUD và chuẩn hóa API quản lý thiết bị"
date: 2026-10-10T09:00:00+07:00
weight: 8
draft: false
description: "Xử lý CRUD và chuẩn hóa API quản lý thiết bị"
---

# 8. Xử lý CRUD và chuẩn hóa API quản lý thiết bị

### Mục tiêu tuần 8:

- Hoàn thiện thiết kế thêm, sửa, xóa, xem danh sách và xem chi tiết thiết bị.
- Thống nhất phương thức HTTP và đường dẫn với giao diện.
- Biết phân biệt route đã cấu hình và route đã kiểm thử đầy đủ.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Cấu hình GET /devices, POST /devices và GET /devices/{id}. | 10/10/2026 | 10/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Chủ nhật (tự học) | Bổ sung PUT /devices/{id} và DELETE /devices/{id} trong Lambda và API Gateway. | 11/10/2026 | 11/10/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Thứ Hai (tự học) | Đọc httpMethod hoặc requestContext.http.method, pathParameters, JSON body để chia nhánh xử lý. | 12/10/2026 | 12/10/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Thứ Ba (tự học) | Kiểm tra bản ghi mẫu trong DynamoDB sau thao tác; bổ sung CORS và mã lỗi cho trường hợp không hợp lệ. | 13/10/2026 | 13/10/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Kết quả đạt được tuần 8:

- Có cấu hình nhóm route quản lý thiết bị và định dạng JSON dùng chung với giao diện.
- Biết xác minh bản ghi qua **DynamoDB Explore table items**, không chỉ nhìn thông báo trên trình duyệt.
- Các route còn phải kiểm thử với access token thật trước khi khẳng định toàn bộ CRUD đã chạy end-to-end.

