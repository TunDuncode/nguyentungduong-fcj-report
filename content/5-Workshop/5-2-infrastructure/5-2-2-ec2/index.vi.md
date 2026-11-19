---
title: "5.2.2. Tạo máy chủ Ubuntu EC2"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.2.2. Tạo máy chủ Ubuntu EC2

## Mục tiêu

Khởi tạo máy chủ Ubuntu phục vụ kiểm thử giám sát CloudWatch mà vẫn hạn chế rủi ro truy cập trái phép.

## Các bước

1. Mở **EC2 → Instances → Launch instances**.
2. Tên máy chủ: `netmon-ec2-server` (đã sử dụng trong quá trình thử nghiệm).
3. Chọn **Ubuntu Server 24.04 LTS** và loại instance phù hợp với ngân sách, hạn mức hiện có.

4. Trong **Network settings**, chọn VPC và Public subnet dự kiến; kiểm tra lựa chọn Public IP theo nhu cầu kết nối.

5. Cấu hình **Security Group**: không mở SSH `22` đến toàn Internet (`0.0.0.0/0`). Chỉ cho phép IP quản trị đáng tin cậy hoặc sử dụng Systems Manager Session Manager khi phù hợp.

6. Giữ EBS ở mức tối thiểu đáp ứng thực hành; nhớ rằng EBS có thể tính phí ngay cả khi EC2 đã Stop.
7. Khởi tạo instance, chờ **Status checks passed** (ví dụ 3/3 nếu Console hiển thị ba kiểm tra). Gắn IAM instance profile nếu CloudWatch Agent cần gửi metrics/logs.

{{< netmonimg src="images/netmon-workshop/18-ec2-instances-netmon-list.png" alt="Danh sách EC2 Instances" caption="Ảnh 18 – Danh sách EC2 Instances" >}}

{{< netmonimg src="images/netmon-workshop/19-ec2-netmon-ec2-server-details.png" alt="Thông tin máy EC2 netmon-ec2-server" caption="Ảnh 19 – Thông tin máy EC2 netmon-ec2-server" >}}

## Kiểm tra

- Instance ở trạng thái `Running` khi cần giám sát.
- CloudWatch hiển thị CPUUtilization cho đúng InstanceId.
- Chụp Instance name, loại instance, subnet, Security Group, status checks (che địa chỉ không muốn công khai).

> `Stop` EC2 thường dừng phí compute theo thời gian chạy nhưng không đồng nghĩa dừng toàn bộ phí EBS hoặc IP công cộng.

## Đưa EC2 vào danh sách thiết bị

Xác định Instance ID từ trang **Instances**, IP phù hợp và Region. Khi đăng ký thiết bị trên NetMon, lưu mã thiết bị riêng (`deviceId`) và `instanceId` dùng để truy vấn CloudWatch. Chọn nguồn AWS EC2 theo cấu hình giao diện, không nhập CPU/RAM mô phỏng cho máy chủ này. Nếu EC2 dừng hoặc thiếu metric, hiển thị trạng thái hoặc dữ liệu chưa có thay vì tự gán 0%.


[← Về chương](../)
