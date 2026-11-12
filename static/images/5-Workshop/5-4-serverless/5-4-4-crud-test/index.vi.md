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
3. **GET `/devices/TEST-SW01`**: đọc chi tiết, đối chiếu đủ thuộc tính.

![Các bản ghi thiết bị trong NetworkDevices]({{< relURL "images/netmon-workshop/dynamodb-items.webp" >}})

*Hình minh chứng: Các bản ghi thiết bị trong NetworkDevices. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. **PUT `/devices/TEST-SW01`**: cập nhật trạng thái hoặc tên; đọc lại để kiểm tra.

![Bản ghi cảnh báo trong NetworkAlerts]({{< relURL "images/netmon-workshop/dynamodb-alerts.webp" >}})

*Hình minh chứng: Bản ghi cảnh báo trong NetworkAlerts. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. **DELETE `/devices/TEST-SW01`**: chỉ xóa bản ghi thử sau khi đã thu thập minh chứng.
6. **GET `/alerts`** và **PUT `/alerts/{id}`**: xác nhận bảng lịch sử, chỉ thay đổi cảnh báo thử; không tự động đánh dấu cảnh báo thật đã xử lý.

## Lưu ý bảo mật

Nếu đã gắn JWT Authorizer, hãy gọi API bằng Access Token có scope `netmon-api/read` hoặc `netmon-api/write` thích hợp. Nếu không có token, 401 là kết quả mong đợi.

**Trạng thái:** Đây là kế hoạch kiểm thử đầu-cuối; từ những ảnh đã có, chưa đủ căn cứ khẳng định tất cả thao tác CRUD trên trình duyệt đều thành công.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
