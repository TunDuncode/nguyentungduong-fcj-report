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
2. Nếu demo đã kết thúc, sao lưu cấu hình cần lưu rồi xóa App Client, Resource Server và User Pool theo đúng thứ tự phù hợp; việc xóa pool sẽ làm người dùng không thể đăng nhập vào NetMon.

![Cognito xác nhận User Pool và App Client được tạo]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Hình minh chứng: Cognito xác nhận User Pool và App Client được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. **EC2:** Nếu chỉ tạm dừng bài thực hành, chọn **Stop instance**. **Stop không tự xóa EBS**, public IPv4 hoặc tài nguyên tính phí khác.
4. Nếu kết thúc hẳn, đối chiếu instance `netmon-ec2-server`, EBS, Elastic IP/Public IPv4, VPC, Internet Gateway, Route Table, NAT Gateway (nếu có), Security Group, IAM instance profile trước khi quyết định xóa.

![Máy chủ EC2 đã xuất hiện trong bảng Instances]({{< relURL "images/netmon-workshop/ec2-list.webp" >}})

*Hình minh chứng: Máy chủ EC2 đã xuất hiện trong bảng Instances. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. **Billing:** Kiểm tra hóa đơn và Cost Explorer những ngày sau khi dọn dẹp, vì số liệu chi phí có thể cập nhật trễ.

## Cảnh báo

Không xóa tài khoản root AWS, không xóa VPC mặc định hoặc tài nguyên dùng chung chỉ để làm sạch danh sách.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
