---
title: "5.2.1. Tạo VPC, Subnet, Route Table và IGW"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.2.1. Tạo VPC, Subnet, Route Table và IGW

## Mục tiêu

Thiết lập mạng ảo để triển khai máy chủ giám sát EC2, tách biệt các thành phần kết nối Internet và các thành phần nội bộ.

## Thực hiện trên AWS Console

1. Vào **VPC → Your VPCs → Create VPC**. Chọn kiểu VPC phù hợp. Ví dụ khi thực hành: CIDR `10.0.0.0/16` (không khẳng định đây là CIDR thực tế của nhóm).
2. Tạo **Public subnet** (ví dụ `10.0.1.0/24`) và **Private subnet** (ví dụ `10.0.2.0/24`) trong Availability Zone phù hợp.
3. Tạo **Internet Gateway**, sau đó attach vào VPC.

![Trang tạo máy chủ EC2 và lựa chọn cấu hình]({{< relURL "images/netmon-workshop/ec2-creation.webp" >}})

*Hình minh chứng: Trang tạo máy chủ EC2 và lựa chọn cấu hình. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Tạo **Public Route Table**; đặt route `0.0.0.0/0` trỏ tới Internet Gateway và liên kết với Public subnet.
5. Private subnet không tự có đường ra Internet. Nếu cần truy cập Internet từ Private subnet, phải thiết kế giải pháp NAT phù hợp và đánh giá chi phí trước khi triển khai.
6. Kiểm tra **Network ACL** và **Security Group** theo luồng traffic dự kiến; mặc định chặn những kết nối không cần thiết.

## Kết quả cần chụp

- VPC và dải CIDR, danh sách subnet.
- Route table và liên kết đến Internet Gateway.
- Security Group gắn cho máy chủ EC2.

> Không tạo NAT Gateway chỉ để hoàn thiện hình minh họa nếu dự án không thật sự cần, vì dịch vụ này có thể phát sinh phí theo giờ và lưu lượng.

![Sơ đồ minh họa quy trình]({{< relURL "images/netmon-workshop/netmon-vpc-flow.png" >}})

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
