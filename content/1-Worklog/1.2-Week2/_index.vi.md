---
title: "2. IAM, phân quyền nhóm và AWS Budgets"
date: 2026-08-29T09:00:00+07:00
weight: 2
draft: false
description: "IAM, phân quyền nhóm và AWS Budgets"
---

# 2. IAM, phân quyền nhóm và AWS Budgets

### Mục tiêu tuần 2:

- Hiểu IAM User, Role, Policy và nguyên tắc cấp quyền tối thiểu.
- Tách quyền thao tác của các thành viên khỏi quyền thực thi Lambda.
- Biết cách đặt cảnh báo chi phí cho tài khoản AWS học tập.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| Thứ Bảy (tại cơ sở) | Tìm hiểu cách một tài khoản AWS làm việc theo nhóm với từng danh tính IAM riêng. | 29/08/2026 | 29/08/2026 | [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Chủ nhật (tự học) | Xem phạm vi quyền cần thiết cho hạ tầng VPC/EC2, Serverless và CloudWatch. | 30/08/2026 | 30/08/2026 | [IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| Thứ Hai (tự học) | Tìm hiểu ngân sách tháng 20 USD và ngưỡng cảnh báo 25%, 50%, 100%; phân biệt cảnh báo với giới hạn chi tiêu. | 31/08/2026 | 31/08/2026 | [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |
| Thứ Ba (tự học) | Kiểm tra cách theo dõi chi phí EC2/EBS, IPv4 công khai, CloudWatch, Lambda và DynamoDB. | 01/09/2026 | 01/09/2026 | [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |

### Kết quả đạt được tuần 2:

- Có phương án phân chia quyền theo ba mảng công việc; hiểu rằng không nên dùng chung thông tin đăng nhập root.
- Nắm cấu hình AWS Budget 20 USD/tháng và các ngưỡng cảnh báo; đây không phải số tiền đã chi.
- Biết kiểm tra IAM Role của Lambda khi gặp lỗi truy cập DynamoDB.

