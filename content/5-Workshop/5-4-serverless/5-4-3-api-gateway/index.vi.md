---
title: "5.4.3. Xây dựng HTTP API Gateway với 8 Routes"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.4.3. Xây dựng HTTP API Gateway với 8 Routes

## Mục tiêu

Tạo HTTP API phục vụ thao tác quản lý NetMon và tích hợp vào Lambda `netmon-api`.

## Các bước trên Console

1. Vào **API Gateway → APIs → Create API → HTTP API**. Tên dùng trong nhóm: `netmon-management-api`.
2. Tạo hoặc kiểm tra các routes sau:

{{< netmonimg src="images/netmon-workshop/38-api-gateway-netmon-management-api-routes.png" alt="Tám route trên API Gateway" caption="Ảnh 38 – Tám route trên API Gateway" >}}

| Route | Công dụng |
|---|---|
| `GET /devices` | Liệt kê thiết bị |
| `POST /devices` | Thêm thiết bị |
| `GET /devices/{id}` | Xem chi tiết |
| `PUT /devices/{id}` | Sửa thiết bị |
| `DELETE /devices/{id}` | Xóa thiết bị |
| `GET /alerts` | Xem cảnh báo |
| `PUT /alerts/{id}` | Cập nhật xử lý cảnh báo |
| `GET /metrics` | Xem CPU/RAM và lưu lượng EC2 khi có dữ liệu |

3. Ở **Develop → Integrations**, chọn **Lambda function** `netmon-api` tại `us-east-1`, payload format **2.0**, và gắn integration vào cả 8 routes.

{{< netmonimg src="images/netmon-workshop/40-api-gateway-integrations-netmon-api.png" alt="API Gateway gắn với Lambda netmon-api" caption="Ảnh 40 – API Gateway gắn với Lambda netmon-api" >}}

4. Ở **Develop → CORS**, cấu hình origin `http://localhost:5500`, methods GET/POST/PUT/DELETE/OPTIONS, headers `authorization`, `content-type`; không bật credentials nếu chỉ gửi JWT trong header.

{{< netmonimg src="images/netmon-workshop/41-api-gateway-cors-localhost-5500.png" alt="Cấu hình CORS localhost:5500" caption="Ảnh 41 – Cấu hình CORS localhost:5500" >}}

5. Mở **Deploy → Stages → `$default`**, kiểm tra **Automatic deployment = Enabled**. Nếu tắt, cần deploy thủ công.

{{< netmonimg src="images/netmon-workshop/42-api-gateway-default-stage-auto-deploy.png" alt="Stage $default tự động triển khai" caption="Ảnh 42 – Stage $default tự động triển khai" >}}

## Kiểm thử ban đầu

Khi routes đã gắn JWT Authorizer, gọi `GET /devices` mà **không** gửi Authorization header phải nhận `401 Unauthorized`. Điều này cho thấy lớp bảo vệ đang hoạt động; để xác nhận Lambda thật, cần thử với Access Token hợp lệ.

> Trong trang workshop công khai, không đặt Access Token thực, secret hay ảnh chụp dữ liệu cá nhân.

## Kết nối với phiên bản giao diện mới

Tám route trên là cấu hình API nền tảng trong ảnh. Giao diện giám sát có thể dùng `GET /metrics` để lấy CPU/RAM/lưu lượng. Nếu sử dụng thêm `GET /observability` hoặc `GET /sns/status` trong một phiên bản giao diện, phải kiểm tra route đã tồn tại, integration đúng Lambda và JWT scope đọc trước khi bật tính năng. Đây là các phần mở rộng, không được tính là đã triển khai chỉ dựa vào cấu hình tám route.

Trong DevTools → Network, kiểm tra URL đầy đủ, method, status code và response JSON. Lỗi 404 có thể do route hoặc stage sai; lỗi 401/403 liên quan xác thực hoặc scope, còn lỗi 500 cần xem CloudWatch Logs.


[← Về chương](../)
