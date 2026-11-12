---
title: "5.6.3. Dọn dẹp CloudWatch, SNS và EventBridge"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.6.3. Dọn dẹp CloudWatch, SNS và EventBridge

## Khi nào thực hiện?

**Chỉ thực hiện sau khi đã demo xong và đã sao lưu toàn bộ minh chứng.** Nếu còn cần nhận cảnh báo, không được xóa alarm, SNS hay rule EventBridge.

## Các bước dọn dẹp

1. Mở **CloudWatch → Alarms**. Chụp cấu hình, lịch sử alarm và đối chiếu tên `netmon-cpu-high-80`, `netmon-ram-high-80`, `netmon-disk-high-85`.

{{< netmonimg src="images/netmon-workshop/21-cloudwatch-alarms-list.png" alt="Danh sách ba CloudWatch Alarm" caption="Ảnh 21 – Danh sách ba CloudWatch Alarm" >}}

2. Nếu chắc chắn không cần nữa, chọn từng alarm và xóa. Hành động này dừng đánh giá alarm, không xóa EC2.

3. Vào **EventBridge → Event buses → default → Rules**, chọn `netmon-alarm-state-rule`, kiểm tra Targets rồi xóa rule sau khi đảm bảo không còn sử dụng.

{{< netmonimg src="images/netmon-workshop/28-eventbridge-default-bus-rule-enabled.png" alt="EventBridge default bus và rule" caption="Ảnh 28 – EventBridge default bus và rule" >}}

4. Vào **SNS → Topics → `netmon-alerts`**, ghi lại danh sách email subscriptions; chỉ xóa subscriptions/topic khi đã kết thúc kịch bản gửi email.

{{< netmonimg src="images/netmon-workshop/26-sns-subscriptions-confirmed-list.png" alt="Danh sách SNS subscriptions" caption="Ảnh 26 – Danh sách SNS subscriptions" >}}


5. Kiểm tra **CloudWatch → Log groups**; xuất log cần giữ và xóa log groups thử nghiệm khi chắc chắn không còn cần đối chiếu lỗi.

## Kiểm tra

Danh sách alarm, rule, topic và log được xử lý theo quyết định của nhóm; không xóa nhầm tài nguyên của dự án khác trong cùng tài khoản AWS.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
