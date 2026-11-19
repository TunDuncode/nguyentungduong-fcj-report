---
title: "5.4.5. Mô phỏng thiết bị và giám sát tự động"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.4.5. Mô phỏng thiết bị và giám sát tự động

## Mục tiêu

Mô phỏng hoạt động của router, switch và server không có nguồn đo thực để kiểm thử giám sát và cảnh báo mà không cần mua thiết bị vật lý. Dữ liệu EC2 vẫn lấy từ CloudWatch, không đưa vào bộ sinh số ngẫu nhiên.

## Bước 1 – Đăng ký thiết bị mô phỏng

Trong trang **Thiết bị**, thêm một thiết bị thử. Có thể dùng dữ liệu mẫu sau nếu API đang sử dụng các trường tương ứng:

```json
{
  "deviceId": "TEST-SW02",
  "deviceName": "Switch Demo",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.250",
  "location": "Tang 1",
  "status": "ONLINE",
  "metricsSource": "SIMULATED"
}
```

Không bắt buộc nhập CPU/RAM nếu backend hỗ trợ tự sinh. Đối chiếu bản ghi `NetworkDevices` trong DynamoDB khi sử dụng AWS thật. Giá trị trong demo cục bộ không đồng nghĩa đã lưu lên AWS.

## Bước 2 – Cập nhật dữ liệu theo chu kỳ

Có hai cơ chế cần phân biệt:

- Trong demo cục bộ, JavaScript có thể cập nhật số liệu mô phỏng để trình diễn trực tiếp trên trình duyệt.
- Trong chế độ AWS, cần một hàm giám sát (ví dụ `netmon-device-monitor`) được kích hoạt định kỳ bằng EventBridge Scheduler hoặc scheduled rule. Hàm đọc danh sách thiết bị mô phỏng, sinh giá trị trong khoảng 0–100%, cập nhật trạng thái và `lastUpdated`, sau đó đánh giá ngưỡng.

Nếu cần triển khai chu kỳ một phút, cấu hình biểu thức `rate(1 minute)` và gắn đúng Lambda target, kiểm tra invocation trong CloudWatch Logs. Không xem chu kỳ làm mới 60 giây của giao diện là bằng chứng Lambda đã được lập lịch. Có thể thay đổi chu kỳ để cân đối chi phí.

Hàm giám sát chỉ cần quyền DynamoDB phù hợp với các bảng đang sử dụng, CloudWatch Logs và `sns:Publish` trên topic nếu cần gửi email. Không sửa hàm CRUD đang hoạt động để thực hiện việc mô phỏng định kỳ nếu có thể tách riêng.

## Bước 3 – Phát hiện cảnh báo

Để kiểm thử có kiểm soát, đặt CPU của thiết bị mô phỏng ở 96% và ngưỡng CPU ở 90%, giữ RAM dưới ngưỡng. Kết quả mong đợi: thiết bị vượt ngưỡng CPU, tạo cảnh báo với ID thiết bị, giá trị, ngưỡng, thời gian và trạng thái xử lý ban đầu. Khi bật thông báo AWS, hàm giám sát cần ghi vào `NetworkAlerts` và gửi SNS theo chính sách chống trùng, chẳng hạn chỉ gửi khi bắt đầu một sự cố.

Nếu muốn thử thiết bị mất kết nối, chuyển trạng thái mô phỏng `OFFLINE`. Điều này không chứng minh thiết bị vật lý mất mạng. Việc phát hiện ngoại tuyến thực tế cần heartbeat, SNMP hoặc agent phù hợp.

## Bước 4 – Kiểm tra và xử lý

1. Mở Trung tâm cảnh báo, xem sự kiện của thiết bị thử.
2. Chọn xử lý cảnh báo; kiểm tra lịch sử, thời điểm và trạng thái.
3. Với AWS, kiểm tra `GET /alerts`, `PUT /alerts/{id}`, DynamoDB, CloudWatch Logs và hộp thư SNS nếu bật.
4. Khôi phục số liệu bình thường, xác nhận không phát sinh cảnh báo lặp liên tục; xóa thiết bị thử nếu không cần nữa.

## Kết quả và giới hạn

Giao diện demo đã được thử với CPU cao, tự sinh dữ liệu và xử lý cảnh báo. Việc lập lịch backend, lưu cảnh báo và gửi SNS tự động cần được xác nhận trên tài khoản AWS đang triển khai. Không gán nhãn dữ liệu mô phỏng là metric đo thực tế.

[← Về chương](../)
