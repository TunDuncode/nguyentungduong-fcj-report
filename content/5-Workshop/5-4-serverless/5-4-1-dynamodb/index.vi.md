---
title: "5.4.1. Khởi tạo bảng NetworkDevices và NetworkAlerts"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.4.1. Khởi tạo bảng NetworkDevices và NetworkAlerts

## Mục tiêu

Thiết kế cơ sở dữ liệu NoSQL cho danh sách thiết bị và lịch sử cảnh báo. Dùng các bảng đã có, không tạo trùng khi không cần thiết.

## Tạo bảng

1. Mở **DynamoDB → Tables**, Region `us-east-1`.
2. Tạo hoặc xác minh bảng **`NetworkDevices`**, Partition Key `deviceId` (String), chế độ dung lượng **On-demand**.

{{< netmonimg src="images/netmon-workshop/33-dynamodb-networkdevices-2-items.png" alt="Hai bản ghi trong NetworkDevices" caption="Ảnh 33 – Hai bản ghi trong NetworkDevices" >}}


3. Tạo hoặc xác minh bảng **`NetworkAlerts`**, Partition Key `eventId` (String), On-demand.

{{< netmonimg src="images/netmon-workshop/32-dynamodb-networkalerts-7-items.png" alt="Các bản ghi trong NetworkAlerts" caption="Ảnh 32 – Các bản ghi trong NetworkAlerts" >}}



4. Không cần Sort Key nếu thiết kế hiện tại dùng khóa đơn; chỉ bổ sung index khi xác định được mẫu truy vấn cụ thể.

### Dữ liệu thiết bị ví dụ

```json
{
  "deviceId": "TEST-SW01",
  "deviceName": "Switch Demo",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.10",
  "status": "Online"
}
```

Đối với EC2, có thể lưu thêm `instanceId`, `region`, `monitoringSource`, `vpcId`. **Không chép nhầm InstanceId vào ô IP**: `instanceId` là định danh của EC2, còn `ipAddress` là địa chỉ mạng.

### Dữ liệu lịch sử cảnh báo

`NetworkAlerts` dùng `eventId` duy nhất, có thể lưu thêm `alarmName`, `alarmType`, `alarmState`, `eventTime`, `deviceId`, `handlingStatus`, `reason`, `isTest`.

## Kiểm tra

Vào **Explore items → chọn bảng → Scan → Run** và xác nhận bản ghi xuất hiện. `Scan` phù hợp dữ liệu demo nhỏ; với dữ liệu lớn nên thiết kế `Query` và index phù hợp.

> Tránh xóa bảng `NetworkDevices` cũ nếu Lambda hoặc giao diện đang tham chiếu tới bảng đó.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
