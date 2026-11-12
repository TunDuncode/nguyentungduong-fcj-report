---
title: "11. Đăng nhập Cognito, JWT và kết nối giao diện thử nghiệm"
date: 2026-11-07T09:00:00+07:00
weight: 11
draft: false
description: "Đăng nhập Cognito, JWT và kết nối giao diện thử nghiệm"
---

# 11. Đăng nhập Cognito, JWT và kết nối giao diện thử nghiệm

### Mục tiêu tuần 11:

- Hiểu User Pool, App Client, Resource Server và JWT Authorizer.
- Kết nối đăng nhập với các API quản lý thiết bị.
- Thử giao diện HTML/CSS/JavaScript tại localhost bằng VS Code.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Kiểm tra Cognito User Pool, netmon-web-client và miền đăng nhập của ứng dụng. | 07/11/2026 | 07/11/2026 | [Amazon Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html) |
| Chủ nhật (tự học) | Tìm hiểu Authorization Code + PKCE, access token, ID token và sự khác biệt khi gọi API. | 08/11/2026 | 08/11/2026 | [Cognito Authorization Code + PKCE](https://docs.aws.amazon.com/cognito/latest/developerguide/using-pkce-in-authorization-code.html) |
| Thứ Hai (tự học) | Rà soát netmon-jwt-authorizer, OAuth scopes đọc/ghi và các HTTP route cần xác thực. | 09/11/2026 | 09/11/2026 | [HTTP API JWT authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) |
| Thứ Ba (tự học) | Kiểm tra màn hình đăng nhập, danh sách thiết bị, chi tiết và lịch sử cảnh báo trên localhost; đối chiếu dữ liệu demo với dữ liệu AWS. | 10/11/2026 | 10/11/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |

### Kết quả đạt được tuần 11:

- Đã cấu hình luồng đăng nhập bằng Cognito và các thành phần JWT Authorizer trong dự án.
- Có giao diện thử nghiệm localhost; biết lỗi 401 do token khác với lỗi CORS hoặc Lambda.
- **Chưa khẳng định 8 route hoạt động end-to-end** nếu chưa kiểm thử đầy đủ với access token thật và dữ liệu DynamoDB.

