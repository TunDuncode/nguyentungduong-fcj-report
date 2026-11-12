---
title: "5.6.5. Dọn dẹp Cognito và tài nguyên mạng"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.6.5. Dọn dẹp Cognito và tài nguyên mạng

## Mục tiêu

Thu hồi quyền truy cập khi kết thúc đồ án và xử lý các thành phần hạ tầng còn phát sinh phí.

## Các bước dọn dẹp

1. **Amazon Cognito:** Kiểm tra User Pool được dùng bởi `netmon-web-client`. Tài khoản ứng dụng Cognito khác với IAM user đăng nhập AWS Console.

{{< netmonimg src="images/netmon-workshop/43-cognito-user-pool-overview.png" alt="Tổng quan Cognito User Pool" caption="Ảnh 43 – Tổng quan Cognito User Pool" >}}


{{< netmonimg src="images/netmon-workshop/44-cognito-app-client-netmon-web-client.png" alt="Cognito App Client netmon-web-client" caption="Ảnh 44 – Cognito App Client netmon-web-client" >}}


{{< netmonimg src="images/netmon-workshop/49-cognito-users-confirmed-enabled.png" alt="Hai tài khoản được xác minh trong Cognito" caption="Ảnh 49 – Hai tài khoản được xác minh trong Cognito" >}}

2. Nếu demo đã kết thúc, sao lưu cấu hình cần lưu rồi xóa App Client, Resource Server và User Pool theo đúng thứ tự phù hợp; việc xóa pool sẽ làm người dùng không thể đăng nhập vào NetMon.

3. **EC2:** Nếu chỉ tạm dừng bài thực hành, chọn **Stop instance**. **Stop không tự xóa EBS**, public IPv4 hoặc tài nguyên tính phí khác.
4. Nếu kết thúc hẳn, đối chiếu instance `netmon-ec2-server`, EBS, Elastic IP/Public IPv4, VPC, Internet Gateway, Route Table, NAT Gateway (nếu có), Security Group, IAM instance profile trước khi quyết định xóa.

5. **Billing:** Kiểm tra hóa đơn và Cost Explorer những ngày sau khi dọn dẹp, vì số liệu chi phí có thể cập nhật trễ.

## Cảnh báo

Không xóa tài khoản root AWS, không xóa VPC mặc định hoặc tài nguyên dùng chung chỉ để làm sạch danh sách.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
