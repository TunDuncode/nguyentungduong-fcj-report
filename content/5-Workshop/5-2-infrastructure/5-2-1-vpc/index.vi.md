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

1. Vào **VPC → Your VPCs → Create VPC**. Chọn kiểu VPC phù hợp. Dải CIDR của `netmon-vpc` trong ảnh thực tế là `10.0.0.0/16`.

{{< netmonimg src="images/netmon-workshop/06-netmon-vpc-resource-map.png" alt="Bản đồ tài nguyên VPC netmon-vpc" caption="Ảnh 06 – Bản đồ tài nguyên VPC netmon-vpc" >}}

2. Tạo **Public subnet** `10.0.0.0/20` và **Private subnet** `10.0.128.0/20` trong Availability Zone phù hợp.

{{< netmonimg src="images/netmon-workshop/07-subnet-list.png" alt="Danh sách hai subnet" caption="Ảnh 07 – Danh sách hai subnet" >}}


{{< netmonimg src="images/netmon-workshop/08-public-subnet-details.png" alt="Thông tin Public subnet" caption="Ảnh 08 – Thông tin Public subnet" >}}


{{< netmonimg src="images/netmon-workshop/09-private-subnet-details.png" alt="Thông tin Private subnet" caption="Ảnh 09 – Thông tin Private subnet" >}}

3. Tạo **Internet Gateway**, sau đó attach vào VPC.

{{< netmonimg src="images/netmon-workshop/14-netmon-igw-details.png" alt="Internet Gateway netmon-igw" caption="Ảnh 14 – Internet Gateway netmon-igw" >}}


4. Tạo **Public Route Table**; đặt route `0.0.0.0/0` trỏ tới Internet Gateway và liên kết với Public subnet.

{{< netmonimg src="images/netmon-workshop/10-route-tables-list.png" alt="Danh sách route table" caption="Ảnh 10 – Danh sách route table" >}}


{{< netmonimg src="images/netmon-workshop/11-netmon-rtb-public-routes.png" alt="Các route của netmon-rtb-public" caption="Ảnh 11 – Các route của netmon-rtb-public" >}}


{{< netmonimg src="images/netmon-workshop/12-netmon-main-route-table-no-name.png" alt="Main route table của VPC" caption="Ảnh 12 – Main route table của VPC" >}}


{{< netmonimg src="images/netmon-workshop/13-netmon-rtb-private1-us-east-1a-routes.png" alt="Route table của Private subnet" caption="Ảnh 13 – Route table của Private subnet" >}}

5. Private subnet không tự có đường ra Internet. Nếu cần truy cập Internet từ Private subnet, phải thiết kế giải pháp NAT phù hợp và đánh giá chi phí trước khi triển khai.
6. Kiểm tra **Network ACL** và **Security Group** theo luồng traffic dự kiến; mặc định chặn những kết nối không cần thiết.

## Kết quả cần chụp

- VPC và dải CIDR, danh sách subnet.
- Route table và liên kết đến Internet Gateway.
- Security Group gắn cho máy chủ EC2.

> Không tạo NAT Gateway chỉ để hoàn thiện hình minh họa nếu dự án không thật sự cần, vì dịch vụ này có thể phát sinh phí theo giờ và lưu lượng.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
