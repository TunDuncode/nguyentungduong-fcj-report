---
title: "5.2.3. Security Group, IAM Role và truy cập an toàn"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.2.3. Security Group, IAM Role và truy cập an toàn

## Mục tiêu

Bảo vệ máy chủ `netmon-ec2-server` và cấp quyền giám sát mà không mở toàn bộ cổng quản trị ra Internet.

## Các bước thao tác

1. Vào **EC2 → Instances**, chọn `netmon-ec2-server` và mở tab **Security**.
2. Nhấn vào **Security Group** gắn với máy; kiểm tra các **Inbound rules**. Không để SSH TCP/22 có Source `0.0.0.0/0` nếu không có lý do bảo mật cụ thể.

![Lựa chọn phương thức kết nối an toàn với EC2]({{< relURL "images/netmon-workshop/ec2-ssm.webp" >}})

*Hình minh chứng: Lựa chọn phương thức kết nối an toàn với EC2. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. Nếu truy cập bằng **AWS Systems Manager Session Manager**, kiểm tra SSM Agent, IAM instance profile và kết nối mạng cần thiết; nếu điều kiện chưa đủ, dùng phương án kết nối khác được kiểm soát.
4. Tại **EC2 → Actions → Security → Modify IAM role**, gắn instance profile có quyền xuất metrics cho CloudWatch Agent (ví dụ policy quản lý phù hợp).

![Các tùy chọn khi cấu hình máy chủ EC2]({{< relURL "images/netmon-workshop/ec2-security.webp" >}})

*Hình minh chứng: Các tùy chọn khi cấu hình máy chủ EC2. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. Mở tab **Status checks** xác nhận máy đã khởi tạo thành công, rồi đối chiếu log và metrics trên CloudWatch.

## Kiểm tra

- Cấu hình inbound phù hợp với demo, không mở SSH công khai.
- Instance có role phù hợp, không lưu AWS Access Key trực tiếp trên máy.
- Truy cập quản trị được thử nghiệm bằng cách an toàn và có thể thu hồi.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
