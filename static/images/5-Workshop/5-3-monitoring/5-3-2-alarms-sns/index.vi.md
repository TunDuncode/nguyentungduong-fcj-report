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
4. Dùng **Publish message** gửi thông báo thử; kiểm tra Inbox và Spam. Trong quá trình thực hành, nhóm đã nhận thư thử thành công.

![Biểu mẫu gửi tin thử qua SNS]({{< relURL "images/netmon-workshop/sns-publish.webp" >}})

*Hình minh chứng: Biểu mẫu gửi tin thử qua SNS. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*


## Tạo CloudWatch Alarms

| Alarm | Metric | Điều kiện thực hành |
|---|---|---|
| `netmon-cpu-high-80` | `AWS/EC2 / CPUUtilization` | Greater than 80% |
| `netmon-ram-high-80` | `NetMon/EC2 / mem_used_percent` | Greater than 80% |
| `netmon-disk-high-85` | `NetMon/EC2 / disk_used_percent` | Greater than 85% |

Với mỗi alarm, vào **CloudWatch → Alarms → Create alarm → Select metric**. Chọn **Average**, **5 minutes**, **1 out of 1 datapoint**, trạng thái `In alarm` gửi thông báo vào SNS topic `netmon-alerts`. Những ngưỡng trên là cấu hình thử nghiệm, không phải khuyến nghị chung cho mọi máy chủ.

![Cấu hình ngưỡng CloudWatch Alarm]({{< relURL "images/netmon-workshop/cloudwatch-alarm-form.webp" >}})

*Hình minh chứng: Cấu hình ngưỡng CloudWatch Alarm. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*


## Kiểm tra

Trong **CloudWatch → Alarms**, xem đủ ba alarm và trạng thái `OK`, `ALARM` hoặc `INSUFFICIENT_DATA`. `OK` chỉ cho biết metric chưa vượt ngưỡng tại thời điểm xét; không chứng minh SNS hay EventBridge đã chạy một cách đầy đủ.

![Ba CloudWatch Alarm đã được tạo]({{< relURL "images/netmon-workshop/cloudwatch-alarms.webp" >}})

*Hình minh chứng: Ba CloudWatch Alarm đã được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
