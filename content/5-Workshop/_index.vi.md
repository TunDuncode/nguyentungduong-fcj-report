---
title: "5. Workshop"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5. WORKSHOP — HƯỚNG DẪN THỰC HÀNH NETMON TRÊN AWS

## Tổng quan

NetMon là hệ thống quản lý và giám sát hạ tầng mạng doanh nghiệp vừa và nhỏ trên AWS, kết hợp hạ tầng EC2 với các dịch vụ Serverless. Workshop trình bày quy trình nhóm triển khai tại Region `us-east-1`, từ chuẩn bị tài khoản, xây dựng mạng, thu thập chỉ số, thiết kế API, xác thực người dùng đến vận hành giao diện và kiểm thử.

## Kiến trúc và cách hệ thống hoạt động

| Thành phần | Vai trò |
|---|---|
| VPC, Subnet, Security Group, EC2 | Hạ tầng mạng và máy chủ Ubuntu được giám sát thực tế |
| CloudWatch và CloudWatch Agent | Thu thập CPU, RAM, Disk và các chỉ số lưu lượng EC2 |
| SNS | Gửi thông báo cảnh báo qua email |
| EventBridge và Lambda | Chuyển sự kiện thay đổi trạng thái alarm và lưu lịch sử |
| DynamoDB | Lưu danh sách thiết bị và các sự kiện cảnh báo |
| API Gateway và Lambda | Cung cấp API quản lý, truy xuất chỉ số và xử lý cảnh báo |
| Cognito | Xác thực người dùng và cấp Access Token |
| HTML, CSS, JavaScript | Giao diện NetMon, thao tác thiết bị và hiển thị dữ liệu |

**Luồng quản lý:** Trình duyệt xác thực với Cognito; sau đó gửi JWT đến API Gateway → Lambda → DynamoDB. Lambda cũng đọc CloudWatch khi truy vấn chỉ số EC2.

**Luồng giám sát EC2:** EC2/CloudWatch Agent → CloudWatch → Alarm. Alarm gửi thông báo tới SNS; sự kiện đổi trạng thái được EventBridge chuyển tới Lambda để ghi lịch sử trong DynamoDB. Hai nhánh này hoạt động độc lập.

**Luồng mô phỏng:** Router, Switch và các thiết bị không có collector thực được quản lý dưới dạng dữ liệu mô phỏng. CPU/RAM và trạng thái thay đổi theo cơ chế mô phỏng; việc tạo cảnh báo tự động và gửi SNS phụ thuộc vào hàm giám sát và lịch kích hoạt đã triển khai. Không coi dữ liệu mô phỏng là số liệu đo từ thiết bị vật lý.

## Mục tiêu sau workshop

- Quản lý thiết bị bằng CRUD, tìm kiếm và xem chi tiết.
- Theo dõi CPU/RAM, lưu lượng EC2 và phân biệt nguồn dữ liệu thực với mô phỏng.
- Xem, xử lý cảnh báo và tra cứu nhật ký; kiểm tra kết nối với AWS.
- Bảo vệ API bằng JWT, giới hạn quyền và kiểm soát chi phí.

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
   - [5.4.5. Mô phỏng thiết bị và giám sát tự động](5-4-serverless/5-4-5-simulation/)

5. [5.5. Cognito, JWT và giao diện NetMon](5-5-auth-frontend/)
   - [5.5.1. Tạo Cognito User Pool và Web Client](5-5-auth-frontend/5-5-1-cognito/)
   - [5.5.2. Tạo JWT Authorizer và OAuth Scopes](5-5-auth-frontend/5-5-2-jwt/)
   - [5.5.3. Xây dựng trang kiểm thử trên VS Code](5-5-auth-frontend/5-5-3-test-ui/)
   - [5.5.4. Đăng nhập bằng PKCE và gọi API bảo vệ](5-5-auth-frontend/5-5-4-frontend-login/)
   - [5.5.5. Vận hành giao diện quản lý NetMon](5-5-auth-frontend/5-5-5-netmon-interface/)

6. [5.6. Kiểm thử tổng thể và dọn dẹp tài nguyên](5-6-testing-cleanup/)
   - [5.6.1. Kiểm thử từ giao diện đến CloudWatch/DynamoDB](5-6-testing-cleanup/5-6-1-e2e/)
   - [5.6.2. Kiểm tra chi phí và sao lưu minh chứng](5-6-testing-cleanup/5-6-2-cleanup/)
   - [5.6.3. Dọn dẹp CloudWatch, SNS và EventBridge](5-6-testing-cleanup/5-6-3-monitoring-cleanup/)
   - [5.6.4. Dọn dẹp Lambda, DynamoDB và API Gateway](5-6-testing-cleanup/5-6-4-serverless-cleanup/)
   - [5.6.5. Dọn dẹp Cognito và tài nguyên mạng](5-6-testing-cleanup/5-6-5-auth-cleanup/)

## Kết quả và phạm vi kiểm chứng

Các lần thực hành đã ghi nhận cấu hình VPC/EC2, ba alarm, email SNS thử nghiệm, EventBridge, dữ liệu DynamoDB, HTTP API và JWT Authorizer. Lambda đã trả HTTP 200 khi kiểm thử danh sách thiết bị và đã truy xuất được CPU, RAM, NetworkIn/NetworkOut của EC2. Giao diện chế độ demo đã kiểm thử các thao tác CRUD, dữ liệu mô phỏng và xử lý cảnh báo.

Khi trình diễn với AWS thật, cần xác minh lại đăng nhập, CRUD qua trình duyệt, đồng bộ trạng thái xử lý và gửi email tự động; không suy ra các bước này thành công chỉ từ ảnh cấu hình hoặc demo cục bộ. Sơ đồ mạng mang tính minh họa; hệ thống chưa chứng minh khả năng tự phát hiện router/switch vật lý bằng SNMP.

Ảnh minh chứng phản ánh từng thời điểm triển khai. Giữ tài nguyên phục vụ bảo vệ đồ án, không xóa trước khi demo hoàn tất. Không công khai thông tin đăng nhập hoặc token.
