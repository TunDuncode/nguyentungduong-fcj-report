---
title: "5.3.1. Thu thập các chỉ số CPU, RAM và Disk"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.3.1. Thu thập các chỉ số CPU, RAM và Disk

## Mục tiêu

Hiển thị CPU, RAM và Disk của máy chủ EC2 trong CloudWatch, làm dữ liệu đầu vào cho cảnh báo.

## Thực hiện

1. Vào **CloudWatch → Metrics → All metrics**; tìm metric `AWS/EC2 → CPUUtilization` theo InstanceId. CPU là metric EC2 tiêu chuẩn.
2. Đối với RAM và Disk, triển khai **Amazon CloudWatch Agent** trên Ubuntu. Agent cần IAM role cho phép xuất metrics, ví dụ policy phù hợp với `CloudWatchAgentServerPolicy`.

![Cài đặt CloudWatch Agent bằng Systems Manager Run Command]({{< relURL "images/netmon-workshop/ec2-role.webp" >}})

*Hình minh chứng: Cài đặt CloudWatch Agent bằng Systems Manager Run Command. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. Tạo cấu hình agent thu thập `mem_used_percent` và `disk_used_percent`; xác định namespace và dimensions nhất quán. Trong ảnh thực hành nhóm đã sử dụng namespace **`NetMon/EC2`**.

![Màn hình giám sát CloudWatch của nhóm]({{< relURL "images/netmon-workshop/cloudwatch-dashboard.webp" >}})

*Hình minh chứng: Màn hình giám sát CloudWatch của nhóm. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Kiểm tra metrics trong CloudWatch: `mem_used_percent` cùng InstanceId; `disk_used_percent` có thể kèm `path`, `device`, `fstype`.

![Biểu đồ metric trên CloudWatch]({{< relURL "images/netmon-workshop/cloudwatch-metric.webp" >}})

*Hình minh chứng: Biểu đồ metric trên CloudWatch. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. Chọn `Statistic: Average`, `Period: 5 minutes` khi thiết lập cảnh báo, theo cấu hình nhóm đã sử dụng.

## Vì sao RAM/Disk khác CPU?

Amazon EC2 không tự gửi metric phần trăm RAM hoặc sử dụng ổ đĩa cấp hệ điều hành trong bộ metric mặc định. CloudWatch Agent phải chạy và gửi dữ liệu thì mới có đủ thông tin.

## Kiểm tra kết quả

- Có đường biểu đồ CPUUtilization ở namespace `AWS/EC2`.
- Có dữ liệu `mem_used_percent`, `disk_used_percent` ở namespace đã chọn.
- Nếu biểu đồ hiển thị **No data available**, kiểm tra Agent, execution role, đúng Region và dimensions trước khi tạo alarm.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
