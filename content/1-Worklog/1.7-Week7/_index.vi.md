---
title: "7. API Gateway, HTTP routes và CORS"
date: 2026-10-03T09:00:00+07:00
weight: 7
draft: false
description: "API Gateway, HTTP routes và CORS"
---

# 7. API Gateway, HTTP routes và CORS

### Mục tiêu tuần 7:

- Tạo điểm truy cập HTTP cho Lambda từ frontend.
- Kiểm tra route, integration, stage và Invoke URL.
- Giải thích được lỗi CORS khi gọi API qua localhost.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Cấu hình HTTP API netmon-management-api và kết nối Lambda netmon-api. | 03/10/2026 | 03/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Chủ nhật (tự học) | Tạo route GET /devices và kiểm tra stage, auto deploy/Invoke URL. | 04/10/2026 | 04/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Thứ Hai (tự học) | Cấu hình Access-Control-Allow-Origin, Methods và Headers cho localhost; hiểu preflight OPTIONS. | 05/10/2026 | 05/10/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |
| Thứ Ba (tự học) | Thử gọi API bằng browser, HTML/JavaScript hoặc C# thay vì bắt buộc Postman. | 06/10/2026 | 06/10/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |

### Kết quả đạt được tuần 7:

- Đã nối được **API Gateway → Lambda** và biết cách kiểm tra phản hồi JSON.
- Biết phân biệt lỗi sai **stage/route** với lỗi **CORS** hoặc Lambda.
- Có phương án kiểm tra API trực tiếp từ trang localhost trong VS Code.

