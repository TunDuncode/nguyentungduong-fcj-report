---
title: "5.4.4. Kiểm thử CRUD và truy vấn dữ liệu"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.4.4. Kiểm thử CRUD và truy vấn dữ liệu

## Mục tiêu

Kiểm tra CRUD trên bảng `NetworkDevices` qua Lambda/API bằng **bản ghi thử riêng** để không thay đổi dữ liệu EC2 thật đang phục vụ đồ án.

## Chuẩn bị bản ghi thử

Sử dụng `deviceId` bắt đầu bằng `TEST-` và IP private dành cho ví dụ, chẳng hạn `TEST-SW01`.

```json
{
  "deviceId": "TEST-SW01",
  "deviceName": "Switch test NetMon",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.250",
  "status": "Online"
}
```

## Kịch bản CRUD

1. **POST `/devices`**: tạo thiết bị `TEST-SW01`, kỳ vọng phản hồi thành công và bản ghi xuất hiện trong DynamoDB.
2. **GET `/devices`**: đọc danh sách, kiểm tra có thiết bị thử.

{{< netmonimg src="images/netmon-workshop/33-dynamodb-networkdevices-2-items.png" alt="Hai bản ghi trong NetworkDevices" caption="Ảnh 33 – Hai bản ghi trong NetworkDevices" >}}

3. **GET `/devices/TEST-SW01`**: đọc chi tiết, đối chiếu đủ thuộc tính.

4. **PUT `/devices/TEST-SW01`**: cập nhật trạng thái hoặc tên; đọc lại để kiểm tra.

5. **DELETE `/devices/TEST-SW01`**: chỉ xóa bản ghi thử sau khi đã thu thập minh chứng.
6. **GET `/alerts`** và **PUT `/alerts/{id}`**: xác nhận bảng lịch sử, chỉ thay đổi cảnh báo thử; không tự động đánh dấu cảnh báo thật đã xử lý.

{{< netmonimg src="images/netmon-workshop/37-lambda-netmon-api-get-devices-test-200.png" alt="GET /devices trả về HTTP 200 và dữ liệu thiết bị" caption="Ảnh 37 – GET /devices trả về HTTP 200 và dữ liệu thiết bị" >}}


## Lưu ý bảo mật

Nếu đã gắn JWT Authorizer, hãy gọi API bằng Access Token có scope `netmon-api/read` hoặc `netmon-api/write` thích hợp. Nếu không có token, 401 là kết quả mong đợi.

**Trạng thái:** Đây là kế hoạch kiểm thử đầu-cuối; từ những ảnh đã có, chưa đủ căn cứ khẳng định tất cả thao tác CRUD trên trình duyệt đều thành công.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
