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

{{< netmonimg src="images/netmon-workshop/50-ec2-netmon-monitoring-cpu-network-metrics.png" alt="Biểu đồ giám sát CPU và mạng của EC2" caption="Ảnh 50 – Biểu đồ giám sát CPU và mạng của EC2" >}}

2. Đối với RAM và Disk, triển khai **Amazon CloudWatch Agent** trên Ubuntu. Agent cần IAM role cho phép xuất metrics, ví dụ policy phù hợp với `CloudWatchAgentServerPolicy`.

3. Tạo cấu hình agent thu thập `mem_used_percent` và `disk_used_percent`; xác định namespace và dimensions nhất quán. Trong ảnh thực hành nhóm đã sử dụng namespace **`NetMon/EC2`**.

4. Kiểm tra metrics trong CloudWatch: `mem_used_percent` cùng InstanceId; `disk_used_percent` có thể kèm `path`, `device`, `fstype`.

{{< netmonimg src="images/netmon-workshop/51-cloudwatch-netmon-ec2-ram-mem-used-percent.png" alt="Biểu đồ RAM mem_used_percent" caption="Ảnh 51 – Biểu đồ RAM mem_used_percent" >}}

{{< netmonimg src="images/netmon-workshop/52-cloudwatch-netmon-ec2-disk-used-percent.png" alt="Biểu đồ Disk disk_used_percent" caption="Ảnh 52 – Biểu đồ Disk disk_used_percent" >}}

5. Chọn `Statistic: Average`, `Period: 5 minutes` khi thiết lập cảnh báo, theo cấu hình nhóm đã sử dụng.

## Vì sao RAM/Disk khác CPU?

Amazon EC2 không tự gửi metric phần trăm RAM hoặc sử dụng ổ đĩa cấp hệ điều hành trong bộ metric mặc định. CloudWatch Agent phải chạy và gửi dữ liệu thì mới có đủ thông tin.

## Kiểm tra kết quả

- Có đường biểu đồ CPUUtilization ở namespace `AWS/EC2`.
- Có dữ liệu `mem_used_percent`, `disk_used_percent` ở namespace đã chọn.
- Nếu biểu đồ hiển thị **No data available**, kiểm tra Agent, execution role, đúng Region và dimensions trước khi tạo alarm.

## Đọc chỉ số từ giao diện NetMon

API `GET /metrics` có hai nguồn: dữ liệu mô phỏng từ DynamoDB và số liệu EC2 từ CloudWatch. Với EC2, truy vấn `CPUUtilization`, `NetworkIn`, `NetworkOut` ở `AWS/EC2` và `mem_used_percent` ở `NetMon/EC2`, đúng InstanceId và khoảng thời gian. Disk được theo dõi bằng CloudWatch Agent; chỉ hiển thị trên giao diện nếu API thực sự trả trường tương ứng.

Ở lần kiểm thử backend sau khi sửa namespace RAM, EC2 trả CPU khoảng **0,54%**, RAM **27,14%**, NetworkIn **45.479 bytes** và NetworkOut **37.426 bytes**. Đây là một mẫu tại thời điểm test, không phải giá trị cố định hoặc tốc độ truyền. Nếu tính tốc độ, cần dùng tổng bytes và khoảng đo phù hợp. Dữ liệu thiếu nên hiển thị `—` thay vì 0 hoặc số giả.


[← Về chương](../)
