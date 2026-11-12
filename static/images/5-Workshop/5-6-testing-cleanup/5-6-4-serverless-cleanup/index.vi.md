---
title: "5.6.4. Dọn dẹp Lambda, DynamoDB và API Gateway"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.6.4. Dọn dẹp Lambda, DynamoDB và API Gateway

## Điều kiện trước khi xóa

Sau khi hoàn tất đồ án, đã xuất ảnh minh chứng, nội dung log, cấu hình API và dữ liệu thử. **Xóa DynamoDB table có thể làm mất dữ liệu vĩnh viễn**.

## Thực hiện

1. **DynamoDB:** Mở `NetworkDevices` và `NetworkAlerts`, Export/Backup theo nhu cầu rồi chỉ xóa khi không còn dùng; không nên xóa trong giai đoạn thử giao diện.
2. **API Gateway:** Vào APIs → `netmon-management-api`, lưu cấu hình tám Routes, Authorizer, CORS, Stage và Integration. Xóa API nếu chắc chắn không còn frontend sử dụng.

![DynamoDB: danh sách bảng dữ liệu trong dự án]({{< relURL "images/netmon-workshop/dynamodb-tables.webp" >}})

*Hình minh chứng: DynamoDB: danh sách bảng dữ liệu trong dự án. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. **AWS Lambda:** Với `netmon-api` và `netmon-save-alert`, kiểm tra EventBridge target và các trigger trước khi xóa hàm.
4. **IAM Roles:** Kiểm tra role nào chỉ dùng riêng cho Lambda đã xóa; không xóa role dùng chung với EC2 hoặc các dịch vụ khác.

![Tám Route đã được kết nối tới netmon-api]({{< relURL "images/netmon-workshop/api-gateway-integration.webp" >}})

*Hình minh chứng: Tám Route đã được kết nối tới netmon-api. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. **CloudWatch Log groups:** Có thể còn log groups sau khi xóa Lambda, kiểm tra thủ công.

## Kiểm tra

Truy cập AWS Console trong Region `us-east-1`, xác nhận tài nguyên đã xóa thực sự là tài nguyên thuộc NetMon, không phải dự án của thành viên khác.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
