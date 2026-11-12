---
title: "3. Bài viết kỹ thuật"
weight: 3
chapter: true
draft: false
---

## Các bài viết trong quá trình thực tập AWS NetMon

Trong kỳ thực tập từ **08/08 đến 14/11/2026**, nhóm em thực hiện đề tài **xây dựng hệ thống quản lý và giám sát hạ tầng mạng doanh nghiệp vừa và nhỏ trên AWS tích hợp dịch vụ Serverless**. Bên cạnh nội dung Workshop, em tổng hợp những phần đã học và thực hành thành ba bài viết kỹ thuật dưới đây.

Đây là **bài viết cá nhân đang chuẩn bị đăng**, không phải ba bài đã được đăng trên AWS Study Group. Khi đăng chính thức, em sẽ bổ sung đường dẫn bài viết thật.

| Bài viết | Nội dung | Xem chi tiết |
|---|---|---|
| **3.1** | Quản lý thiết bị mạng bằng Lambda, API Gateway, DynamoDB | [Blog 1](./3.1-blog1/) |
| **3.2** | Giám sát và cảnh báo bằng CloudWatch, SNS, EventBridge | [Blog 2](./3.2-blog2/) |
| **3.3** | Đăng nhập Cognito, xác thực JWT và kết nối giao diện | [Blog 3](./3.3-blog3/) |

### Sơ lược kiến trúc liên quan

`Giao diện → Amazon Cognito → API Gateway → AWS Lambda → DynamoDB`

`EC2 → CloudWatch Alarm → Amazon SNS (email)`

`Sự kiện đổi trạng thái Alarm → EventBridge → Lambda → DynamoDB (lịch sử)`

> **Trạng thái:** Bản thảo trên website báo cáo thực tập. Chưa gắn liên kết bài đăng công khai vì em chưa xuất bản các bài này.
