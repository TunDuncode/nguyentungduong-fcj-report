---
title : "Giới thiệu Workshop"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Mục tiêu Workshop

Trong phần này, bạn sẽ biết cách:
- Khởi tạo pipeline CI/CD cho backend serverless bằng AWS SAM.
- Cấu hình Dev và Prod stage.
- Kết nối GitHub với CodePipeline.
- Triển khai frontend với AWS Amplify.
- Thêm kiểm thử và giám sát trong pipeline.

#### Nội dung chính

1. Khởi tạo pipeline bằng `sam pipeline init --bootstrap`.
2. Cấu hình repository, template path và stage.
3. Thêm stage kiểm thử tự động.
4. Thiết lập giám sát CloudWatch cho Lambda và API Gateway.
5. Triển khai frontend Flutter web với Amplify.

#### Kiến trúc GameHub

GameHub được xây dựng như một ứng dụng serverless:
- Lambda function xử lý logic,
- API Gateway cung cấp endpoint HTTP,
- AWS Cognito hoặc custom auth quản lý đăng nhập,
- AWS Amplify hosting phục vụ frontend tĩnh.

#### Lưu ý

- Tên `GameHub` là ví dụ; hãy thay bằng tên dự án của bạn.
- Nếu backend và frontend cùng trong một repository, xác định rõ thư mục riêng.
- Kiểm tra profile và region AWS trước khi chạy lệnh SAM.

Note (hình ảnh): Chèn ảnh mô hình kiến trúc hệ thống tại vị trí này để trực quan. Thư mục placeholder: `images/5-Workshop/5.1-Workshop-overview/gamehub-architecture.svg`.
