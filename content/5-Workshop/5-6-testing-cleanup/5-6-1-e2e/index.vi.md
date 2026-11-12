---
title: "5.6.1. Kiểm thử từ giao diện đến CloudWatch/DynamoDB"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.6.1. Kiểm thử từ giao diện đến CloudWatch/DynamoDB

## Mục tiêu

Thực hiện kịch bản kiểm thử có thể chứng minh ba phần của nhóm (hạ tầng, backend, giám sát/giao diện) kết nối thành một quy trình thống nhất.


## Kịch bản đề xuất

| Mã | Bước kiểm thử | Kết quả mong đợi |
|---|---|---|
| T01 | Truy cập GET `/devices` không JWT | `401 Unauthorized` |
| T02 | Đăng nhập Cognito bằng PKCE | Nhận Access Token hợp lệ |
| T03 | GET `/devices` có scope `read` | Nhận danh sách thiết bị |
| T04 | POST `/devices` với `TEST-SW01` | Tạo bản ghi trong `NetworkDevices` |
| T05 | GET/PUT `/devices/{id}` | Xem và sửa thiết bị thử |
| T06 | DELETE `/devices/{id}` | Xóa đúng thiết bị thử |
| T07 | GET `/alerts` | Đọc sự kiện trong `NetworkAlerts` |
| T08 | PUT `/alerts/{id}` | Chuyển `handlingStatus` thành `Acknowledged` hoặc `Resolved` |
| T09 | GET `/metrics` | Lấy CPU thực từ CloudWatch nếu metric có dữ liệu |
| T10 | Đổi trạng thái một Alarm trong môi trường demo | SNS và lịch sử sự kiện được kiểm tra |

## Lưu bằng chứng

Chụp trang Cognito Users (che email khi công khai), danh sách JWT routes, Lambda Test, DynamoDB Scan, CloudWatch Alarms, EventBridge rule, email SNS đã che người nhận và kết quả API Test. Gắn chú thích `T01`, `T02`... cho từng ảnh.

## Lưu ý kết luận

Chỉ đánh dấu **Pass** sau khi thực sự chạy được và có minh chứng. Những bài test chưa chạy cần ghi `Pending` chứ không được điền thành công tự động. Tránh xóa bản ghi EC2 thật, chỉ thao tác dữ liệu có ID `TEST-`.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

## Các ảnh minh chứng liên quan

{{< netmonimg src="images/netmon-workshop/32-dynamodb-networkalerts-7-items.png" alt="Các bản ghi trong NetworkAlerts" caption="Ảnh 32 – Các bản ghi trong NetworkAlerts" >}}

{{< netmonimg src="images/netmon-workshop/33-dynamodb-networkdevices-2-items.png" alt="Hai bản ghi trong NetworkDevices" caption="Ảnh 33 – Hai bản ghi trong NetworkDevices" >}}

{{< netmonimg src="images/netmon-workshop/37-lambda-netmon-api-get-devices-test-200.png" alt="GET /devices trả về HTTP 200 và dữ liệu thiết bị" caption="Ảnh 37 – GET /devices trả về HTTP 200 và dữ liệu thiết bị" >}}

{{< netmonimg src="images/netmon-workshop/38-api-gateway-netmon-management-api-routes.png" alt="Tám route trên API Gateway" caption="Ảnh 38 – Tám route trên API Gateway" >}}

[← Về chương](../)
