---
title: "5. Workshop"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5. WORKSHOP — HƯỚNG DẪN THỰC HÀNH NETMON TRÊN AWS

## Tổng quan

Workshop này hướng dẫn tái hiện đề tài **Xây dựng hệ thống quản lý và giám sát hạ tầng mạng doanh nghiệp vừa và nhỏ trên AWS tích hợp dịch vụ Serverless**. Dựa trên quy trình mà nhóm đã thử nghiệm tại **us-east-1**, tài liệu được tổ chức theo từng màn hình AWS, từng bước bấm và ảnh minh chứng — giống cấu trúc của trang mẫu mà bạn đưa ra.

**Luồng dữ liệu:** Giao diện → Cognito → API Gateway → Lambda → DynamoDB; giám sát EC2 → CloudWatch → SNS / EventBridge → Lambda → DynamoDB.



## Danh sách chương thực hành

1. [5.1. Chuẩn bị môi trường & chọn Region](5-1-preparation/)
   - [5.1.1. Đăng nhập AWS và chọn Region](5-1-preparation/5-1-1-region-budget/)
   - [5.1.2. Cấu hình IAM và phân công nhóm](5-1-preparation/5-1-2-iam/)
   - [5.1.3. Thiết lập AWS Budgets và kiểm soát chi phí](5-1-preparation/5-1-3-budget/)

2. [5.2. Thiết kế hạ tầng VPC và EC2](5-2-infrastructure/)
   - [5.2.1. Tạo VPC, Subnet, Route Table và IGW](5-2-infrastructure/5-2-1-vpc/)
   - [5.2.2. Tạo máy chủ Ubuntu EC2](5-2-infrastructure/5-2-2-ec2/)
   - [5.2.3. Security Group, IAM Role và truy cập an toàn](5-2-infrastructure/5-2-3-security/)

3. [5.3. CloudWatch, SNS và EventBridge](5-3-monitoring/)
   - [5.3.1. Thu thập các chỉ số CPU, RAM và Disk](5-3-monitoring/5-3-1-metrics/)
   - [5.3.2. Tạo CloudWatch Alarm và gửi SNS Email](5-3-monitoring/5-3-2-alarms-sns/)
   - [5.3.3. Tạo quy tắc EventBridge chuyển trạng thái Alarm](5-3-monitoring/5-3-3-eventbridge/)
   - [5.3.4. Lambda lưu lịch sử cảnh báo vào DynamoDB](5-3-monitoring/5-3-4-alert-history/)

4. [5.4. Lambda, DynamoDB và API Gateway](5-4-serverless/)
   - [5.4.1. Khởi tạo bảng NetworkDevices và NetworkAlerts](5-4-serverless/5-4-1-dynamodb/)
   - [5.4.2. Viết Lambda netmon-api bằng Python](5-4-serverless/5-4-2-lambda-api/)
   - [5.4.3. Xây dựng HTTP API Gateway với 8 Routes](5-4-serverless/5-4-3-api-gateway/)
   - [5.4.4. Kiểm thử CRUD và truy vấn dữ liệu](5-4-serverless/5-4-4-crud-test/)

5. [5.5. Cognito, JWT và giao diện kiểm thử](5-5-auth-frontend/)
   - [5.5.1. Tạo Cognito User Pool và Web Client](5-5-auth-frontend/5-5-1-cognito/)
   - [5.5.2. Tạo JWT Authorizer và OAuth Scopes](5-5-auth-frontend/5-5-2-jwt/)
   - [5.5.3. Xây dựng trang kiểm thử trên VS Code](5-5-auth-frontend/5-5-3-test-ui/)
   - [5.5.4. Đăng nhập bằng PKCE và gọi API bảo vệ](5-5-auth-frontend/5-5-4-frontend-login/)

6. [5.6. Kiểm thử tổng thể và dọn dẹp tài nguyên](5-6-testing-cleanup/)
   - [5.6.1. Kiểm thử từ giao diện đến CloudWatch/DynamoDB](5-6-testing-cleanup/5-6-1-e2e/)
   - [5.6.2. Kiểm tra chi phí và sao lưu minh chứng](5-6-testing-cleanup/5-6-2-cleanup/)
   - [5.6.3. Dọn dẹp CloudWatch, SNS và EventBridge](5-6-testing-cleanup/5-6-3-monitoring-cleanup/)
   - [5.6.4. Dọn dẹp Lambda, DynamoDB và API Gateway](5-6-testing-cleanup/5-6-4-serverless-cleanup/)
   - [5.6.5. Dọn dẹp Cognito và tài nguyên mạng](5-6-testing-cleanup/5-6-5-auth-cleanup/)


## Tiến độ thực tế và phạm vi

- **Đã có minh chứng:** EC2, ba CloudWatch Alarms, SNS gửi mail, DynamoDB có dữ liệu, Lambda ghi lịch sử, EventBridge rule, tám HTTP API Routes, JWT Authorizer, CORS và Lambda Integration.
- **Còn kiểm thử:** giao diện chính, PKCE đổi code lấy token và toàn bộ CRUD từ trình duyệt đến DynamoDB.
- **An toàn:** tránh công khai email, mật khẩu, AWS keys hoặc token. Budget cảnh báo không tự chặn chi phí.

> Bộ hình được lấy từ các ảnh AWS người thực hiện đã chia sẻ; không sử dụng ảnh của GameHub để minh họa như thể đó là dữ liệu NetMon.
