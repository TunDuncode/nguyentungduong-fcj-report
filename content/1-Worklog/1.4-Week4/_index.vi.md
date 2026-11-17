---
title: "4. Tự học định tuyến và bảo mật mạng trên AWS"
date: 2026-09-12T09:00:00+07:00
weight: 4
draft: false
description: "Tự học định tuyến và bảo mật mạng trên AWS"
---

# 4. Tự học định tuyến và bảo mật mạng trên AWS

### Mục tiêu tuần 4:

- Hiểu cơ chế hoạt động của Route Table và Internet Gateway.
- Phân biệt Security Group và Network ACL.
- Nắm nguyên tắc kiểm soát kết nối đến tài nguyên mạng.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Tìm hiểu Route Table, tuyến nội bộ local và cách kết hợp với subnet trong buổi thực tập. | 12/09/2026 | 12/09/2026 | [Subnet route tables](https://docs.aws.amazon.com/vpc/latest/userguide/subnet-route-tables.html) |
| Chủ nhật (tự học) | Đọc cách gắn Internet Gateway vào VPC và cấu hình tuyến ra Internet cho subnet công khai. | 13/09/2026 | 13/09/2026 | [Internet gateway](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-igw.html) |
| Thứ Hai (tự học) | Tự học các quy tắc inbound, outbound của Security Group và cách hạn chế cổng SSH. | 14/09/2026 | 14/09/2026 | [VPC infrastructure security](https://docs.aws.amazon.com/vpc/latest/userguide/infrastructure-security.html) |
| Thứ Ba (tự học) | So sánh Security Group với Network ACL và ghi chú cách kiểm soát lưu lượng ở từng lớp. | 15/09/2026 | 15/09/2026 | [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) |

### Kết quả đạt được tuần 4:

- Hiểu vai trò của Route Table và Internet Gateway khi thiết lập kết nối Internet.
- Phân biệt được bảo mật cấp tài nguyên và cấp subnet.
- Nắm nguyên tắc chỉ mở các cổng thực sự cần thiết.

