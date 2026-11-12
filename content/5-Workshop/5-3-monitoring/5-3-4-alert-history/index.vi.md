---
title: "5.3.4. Lambda lưu lịch sử cảnh báo vào DynamoDB"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.3.4. Lambda lưu lịch sử cảnh báo vào DynamoDB

## Mục tiêu

Lưu từng sự kiện **CloudWatch Alarm State Change** vào bảng `NetworkAlerts` để biết cảnh báo xảy ra lúc nào và đã xử lý hay chưa.

## Các bước thao tác

1. Mở **DynamoDB → Tables** và kiểm tra bảng `NetworkAlerts`, Partition key `eventId` (String).
2. Mở **Lambda → Functions → `netmon-save-alert`**. Chọn `lambda_function.py`, bấm **Deploy** sau khi hoàn thiện mã đọc `event.detail.alarmName`, `event.detail.state.value`, `event.id` và thời gian sự kiện.

{{< netmonimg src="images/netmon-workshop/31-lambda-netmon-save-alert-code-overview.png" alt="Mã nguồn hàm netmon-save-alert" caption="Ảnh 31 – Mã nguồn hàm netmon-save-alert" >}}


3. Trong **Configuration → Permissions**, mở role. Cấp **`dynamodb:PutItem`** chỉ với ARN bảng `NetworkAlerts`, đồng thời giữ quyền ghi CloudWatch Logs.

4. Tạo test event dạng EventBridge và chạy thử. Nếu xuất hiện `AccessDeniedException` cho `PutItem`, cần sửa role của Lambda (không phải role của người đăng nhập AWS Console).
5. Sau khi Test thành công, vào **DynamoDB → Explore items → NetworkAlerts → Scan → Run** để xem bản ghi.

{{< netmonimg src="images/netmon-workshop/32-dynamodb-networkalerts-7-items.png" alt="Các bản ghi trong NetworkAlerts" caption="Ảnh 32 – Các bản ghi trong NetworkAlerts" >}}


6. Kiểm tra trường `eventId`, `alarmName`, `alarmState`, `eventTime`, `handlingStatus`, `isTest`. **Không đổi trạng thái `New` thành `Handled` nếu chưa có người xử lý**.

## Kết quả đã ghi nhận

Trong quá trình làm đồ án đã có bản ghi test `netmon-test-001` và ít nhất một bản ghi sự kiện với `isTest=false` được hiển thị trong `NetworkAlerts`. Đây là bằng chứng lưu lịch sử, không tự chứng minh rằng mọi alarm đều đã kích hoạt khi tải thực tế tăng.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
