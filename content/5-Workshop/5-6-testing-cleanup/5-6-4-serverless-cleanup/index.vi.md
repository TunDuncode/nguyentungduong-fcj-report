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

{{< netmonimg src="images/netmon-workshop/32-dynamodb-networkalerts-7-items.png" alt="Các bản ghi trong NetworkAlerts" caption="Ảnh 32 – Các bản ghi trong NetworkAlerts" >}}


{{< netmonimg src="images/netmon-workshop/33-dynamodb-networkdevices-2-items.png" alt="Hai bản ghi trong NetworkDevices" caption="Ảnh 33 – Hai bản ghi trong NetworkDevices" >}}

2. **API Gateway:** Vào APIs → `netmon-management-api`, lưu cấu hình tám Routes, Authorizer, CORS, Stage và Integration. Xóa API nếu chắc chắn không còn frontend sử dụng.

{{< netmonimg src="images/netmon-workshop/38-api-gateway-netmon-management-api-routes.png" alt="Tám route trên API Gateway" caption="Ảnh 38 – Tám route trên API Gateway" >}}


3. **AWS Lambda:** Với `netmon-api` và `netmon-save-alert`, kiểm tra EventBridge target và các trigger trước khi xóa hàm.

{{< netmonimg src="images/netmon-workshop/34-lambda-netmon-api-code-and-api-gateway.png" alt="Hàm netmon-api và kết nối API Gateway" caption="Ảnh 34 – Hàm netmon-api và kết nối API Gateway" >}}

4. **IAM Roles:** Kiểm tra role nào chỉ dùng riêng cho Lambda đã xóa; không xóa role dùng chung với EC2 hoặc các dịch vụ khác.

5. **CloudWatch Log groups:** Có thể còn log groups sau khi xóa Lambda, kiểm tra thủ công.

## Kiểm tra

Truy cập AWS Console trong Region `us-east-1`, xác nhận tài nguyên đã xóa thực sự là tài nguyên thuộc NetMon, không phải dự án của thành viên khác.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
