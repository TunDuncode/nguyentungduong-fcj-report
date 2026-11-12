---
title: "3. Kiến trúc mạng VPC và phân tách hạ tầng"
date: 2026-09-05T09:00:00+07:00
weight: 3
draft: false
description: "Kiến trúc mạng VPC và phân tách hạ tầng"
---

# 3. Kiến trúc mạng VPC và phân tách hạ tầng

### Mục tiêu tuần 3:

- Đọc được sơ đồ VPC và các thành phần mạng cơ bản.
- Biết nhiệm vụ của public/private subnet, route table và Internet Gateway.
- Hiểu cách backend Serverless kết hợp với tài nguyên EC2 của nhóm.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Cùng Tùng Dương rà soát thiết kế mạng netmon-vpc và dải CIDR thử nghiệm. | 05/09/2026 | 05/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Chủ nhật (tự học) | Phân biệt public subnet, private subnet và đường đi đến Internet Gateway. | 06/09/2026 | 06/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Thứ Hai (tự học) | Tìm hiểu Security Group inbound/outbound, lưu ý không mở SSH 22 cho toàn Internet. | 07/09/2026 | 07/09/2026 | [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html) |
| Thứ Ba (tự học) | Vẽ luồng Dashboard → API Gateway → Lambda → DynamoDB, tách với đường giám sát EC2 → CloudWatch. | 08/09/2026 | 08/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |

### Kết quả đạt được tuần 3:

- Đọc được kiến trúc mạng mô phỏng và luồng kết nối dịch vụ Serverless.
- Hiểu **EC2 metrics** khác với số liệu thiết bị giả lập lưu trong **NetworkDevices**.
- Phân định rõ phần VPC/EC2 do Tùng Dương phụ trách; em theo dõi để chuẩn bị tích hợp API.

