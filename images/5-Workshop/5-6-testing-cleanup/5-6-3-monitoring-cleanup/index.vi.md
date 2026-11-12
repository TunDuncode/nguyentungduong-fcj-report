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
2. Nếu chắc chắn không cần nữa, chọn từng alarm và xóa. Hành động này dừng đánh giá alarm, không xóa EC2.

![Ba CloudWatch Alarm đã được tạo]({{< relURL "images/netmon-workshop/cloudwatch-alarms.webp" >}})

*Hình minh chứng: Ba CloudWatch Alarm đã được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. Vào **EventBridge → Event buses → default → Rules**, chọn `netmon-alarm-state-rule`, kiểm tra Targets rồi xóa rule sau khi đảm bảo không còn sử dụng.
4. Vào **SNS → Topics → `netmon-alerts`**, ghi lại danh sách email subscriptions; chỉ xóa subscriptions/topic khi đã kết thúc kịch bản gửi email.

![Quy tắc EventBridge trong dự án NetMon]({{< relURL "images/netmon-workshop/eventbridge-rule.webp" >}})

*Hình minh chứng: Quy tắc EventBridge trong dự án NetMon. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. Kiểm tra **CloudWatch → Log groups**; xuất log cần giữ và xóa log groups thử nghiệm khi chắc chắn không còn cần đối chiếu lỗi.

## Kiểm tra

Danh sách alarm, rule, topic và log được xử lý theo quyết định của nhóm; không xóa nhầm tài nguyên của dự án khác trong cùng tài khoản AWS.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
