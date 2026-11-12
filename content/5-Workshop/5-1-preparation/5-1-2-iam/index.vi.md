---
title: "5.1.2. Cấu hình IAM và phân công nhóm"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.1.2. Cấu hình IAM và phân công nhóm

## Mục tiêu

Phân công trách nhiệm triển khai và cấu hình IAM để từng thành viên có thể thực hiện phần việc của mình mà không dùng chung thông tin đăng nhập.

## Phân công nhóm

| Thành viên | Vai trò |
|---|---|
| Tùng Dương | VPC, Public/Private Subnet, Route Table, Internet Gateway, Security Group, EC2 |
| Xuân Đức | Lambda, DynamoDB, API Gateway, xử lý CRUD và API cảnh báo |
| Mạnh Quân | CloudWatch, SNS, giao diện và kiểm thử |

## Thực hiện

1. Vào **IAM → Users**. Tạo IAM user riêng hoặc sử dụng AWS IAM Identity Center theo khả năng của tài khoản.
2. Chỉ bật **AWS Management Console access** cho tài khoản cần truy cập Console; thiết lập mật khẩu mạnh và MFA.
3. Tạo policy hoặc nhóm quyền theo công việc. Trong thời gian thực hành, có thể dùng policy AWS-managed phù hợp, sau đó thu hẹp quyền khi triển khai ổn định.

4. Khi tạo Lambda, mở **Configuration → Permissions** để xác định execution role. Role `netmon-api` cần được cấp quyền phù hợp để đọc/ghi `NetworkDevices`, `NetworkAlerts` và đọc chỉ số CloudWatch theo nhu cầu thực tế.

{{< netmonimg src="images/netmon-workshop/53-lambda-netmon-api-execution-role-permissions.png" alt="Execution role của Lambda netmon-api" caption="Ảnh 53 – Execution role của Lambda netmon-api" >}}


{{< netmonimg src="images/netmon-workshop/54-iam-netmon-api-role-permission-policies.png" alt="Danh sách IAM policies của role" caption="Ảnh 54 – Danh sách IAM policies của role" >}}


{{< netmonimg src="images/netmon-workshop/55-iam-netmon-api-access-policy-json.png" alt="JSON chính sách quyền DynamoDB và CloudWatch" caption="Ảnh 55 – JSON chính sách quyền DynamoDB và CloudWatch" >}}

5. Execution role của `netmon-save-alert` chỉ nên được cấp quyền cần thiết để ghi bảng `NetworkAlerts` và ghi log CloudWatch.

## Kiểm tra

Đăng nhập bằng user của từng thành viên, kiểm tra các chức năng được cấp. Khi gặp `AccessDeniedException`, xem tên action và tài nguyên trong CloudWatch Logs rồi sửa role chính xác, không cấp quyền `*` bừa bãi.

> **Phân biệt:** IAM user quản trị AWS khác với Cognito user đăng nhập ứng dụng NetMon. Xóa tài khoản Cognito không xóa tài nguyên IAM hoặc EC2.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
