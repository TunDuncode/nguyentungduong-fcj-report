---
title: "5.3.3. Tạo quy tắc EventBridge chuyển trạng thái Alarm"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.3.3. Tạo quy tắc EventBridge chuyển trạng thái Alarm

## Mục tiêu

Khi CloudWatch Alarm thay đổi trạng thái, EventBridge chuyển sự kiện đến Lambda để lưu lịch sử trong DynamoDB, hỗ trợ theo dõi thời điểm và trạng thái xử lý cảnh báo.

## Thực hiện

1. Đảm bảo bảng `NetworkAlerts` đã tồn tại với Partition Key `eventId` kiểu String.
2. Tạo Lambda Python `netmon-save-alert` và gắn execution role có quyền `dynamodb:PutItem` vào bảng `NetworkAlerts` cùng quyền ghi CloudWatch Logs.

3. Mở **Amazon EventBridge → Event buses → default → Rules → Create rule**. Đặt tên `netmon-alarm-state-rule`, chọn rule trên event bus `default`.

{{< netmonimg src="images/netmon-workshop/28-eventbridge-default-bus-rule-enabled.png" alt="EventBridge default bus và rule" caption="Ảnh 28 – EventBridge default bus và rule" >}}


4. Trong **Custom pattern (JSON editor)** nhập mẫu sau:

{{< netmonimg src="images/netmon-workshop/29-eventbridge-netmon-alarm-state-rule-pattern.png" alt="Mẫu lọc sự kiện CloudWatch Alarm" caption="Ảnh 29 – Mẫu lọc sự kiện CloudWatch Alarm" >}}


```json
{
  "source": ["aws.cloudwatch"],
  "detail-type": ["CloudWatch Alarm State Change"],
  "detail": {
    "alarmName": [
      "netmon-cpu-high-80",
      "netmon-ram-high-80",
      "netmon-disk-high-85"
    ]
  }
}
```

5. Trong **Target**, chọn Lambda `netmon-save-alert`. Kiểm tra resource-based policy cho phép EventBridge invoke Lambda.

{{< netmonimg src="images/netmon-workshop/30-eventbridge-netmon-alarm-state-rule-lambda-target.png" alt="Lambda đích trong EventBridge Rule" caption="Ảnh 30 – Lambda đích trong EventBridge Rule" >}}


6. Kiểm thử bằng một sự kiện CloudWatch hợp lệ hoặc chuyển trạng thái alarm có kiểm soát trong môi trường demo, sau đó vào **DynamoDB → Explore items → NetworkAlerts → Scan → Run**.

## Kiểm tra kết quả

Bản ghi cần có `eventId`, `alarmName`, `alarmState`, `eventTime` và trường nhận diện thiết bị nếu code có lưu. Dữ liệu test và dữ liệu thật nên được phân biệt bằng `isTest`. Nhóm đã từng thấy một bản ghi thử nghiệm (`isTest=true`) và một bản ghi sự kiện (`isTest=false`) trong bảng.

> Lỗi hay gặp: `AccessDeniedException` với `dynamodb:PutItem`. Hãy sửa chính xác policy execution role và test lại, không tạo bảng mới chỉ vì thiếu quyền.


---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
