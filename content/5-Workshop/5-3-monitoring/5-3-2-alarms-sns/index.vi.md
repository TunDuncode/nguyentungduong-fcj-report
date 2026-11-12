---
title: "5.3.2. Tạo CloudWatch Alarm và gửi SNS Email"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.3.2. Tạo CloudWatch Alarm và gửi SNS Email

## Mục tiêu

Tạo ba alarm CPU/RAM/Disk và kết nối SNS để gửi thông báo khi một chỉ số vượt ngưỡng.

## Tạo SNS Topic

1. Mở **Amazon SNS → Topics → Create topic** (Standard), đặt tên `netmon-alerts`.
2. Vào topic → **Create subscription** → Protocol `Email`, nhập email nhận cảnh báo.
3. Mở thư từ AWS SNS và bấm **Confirm subscription**. Nếu còn `Pending confirmation`, SNS chưa thể chuyển email đến subscription đó.

{{< netmonimg src="images/netmon-workshop/25-sns-new-subscription-confirmed.png" alt="SNS subscription đã được xác nhận" caption="Ảnh 25 – SNS subscription đã được xác nhận" >}}


{{< netmonimg src="images/netmon-workshop/26-sns-subscriptions-confirmed-list.png" alt="Danh sách SNS subscriptions" caption="Ảnh 26 – Danh sách SNS subscriptions" >}}


{{< netmonimg src="images/netmon-workshop/27-sns-netmon-alerts-new-email-confirmed.png" alt="Topic SNS netmon-alerts với email đã xác nhận" caption="Ảnh 27 – Topic SNS netmon-alerts với email đã xác nhận" >}}

4. Dùng **Publish message** gửi thông báo thử; kiểm tra Inbox và Spam. Trong quá trình thực hành, nhóm đã nhận thư thử thành công.

## Tạo CloudWatch Alarms

| Alarm | Metric | Điều kiện thực hành |
|---|---|---|
| `netmon-cpu-high-80` | `AWS/EC2 / CPUUtilization` | Greater than 80% |
| `netmon-ram-high-80` | `NetMon/EC2 / mem_used_percent` | Greater than 80% |
| `netmon-disk-high-85` | `NetMon/EC2 / disk_used_percent` | Greater than 85% |

Với mỗi alarm, vào **CloudWatch → Alarms → Create alarm → Select metric**. Chọn **Average**, **5 minutes**, **1 out of 1 datapoint**, trạng thái `In alarm` gửi thông báo vào SNS topic `netmon-alerts`. Những ngưỡng trên là cấu hình thử nghiệm, không phải khuyến nghị chung cho mọi máy chủ.

## Kiểm tra

Trong **CloudWatch → Alarms**, xem đủ ba alarm và trạng thái `OK`, `ALARM` hoặc `INSUFFICIENT_DATA`. `OK` chỉ cho biết metric chưa vượt ngưỡng tại thời điểm xét; không chứng minh SNS hay EventBridge đã chạy một cách đầy đủ.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

## Các ảnh minh chứng liên quan

{{< netmonimg src="images/netmon-workshop/21-cloudwatch-alarms-list.png" alt="Danh sách ba CloudWatch Alarm" caption="Ảnh 21 – Danh sách ba CloudWatch Alarm" >}}

{{< netmonimg src="images/netmon-workshop/22-cloudwatch-disk-high-85-details.png" alt="Alarm disk vượt 85%" caption="Ảnh 22 – Alarm disk vượt 85%" >}}

{{< netmonimg src="images/netmon-workshop/23-cloudwatch-ram-high-80-details.png" alt="Alarm RAM vượt 80%" caption="Ảnh 23 – Alarm RAM vượt 80%" >}}

{{< netmonimg src="images/netmon-workshop/24-cloudwatch-cpu-high-80-details.png" alt="Alarm CPU vượt 80%" caption="Ảnh 24 – Alarm CPU vượt 80%" >}}

[← Về chương](../)
