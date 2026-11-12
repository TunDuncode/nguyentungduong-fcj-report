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
7. Khởi tạo instance, chờ **2/2 status checks passed** (hoặc trạng thái kiểm tra tương ứng trên Console). Gắn IAM instance profile nếu CloudWatch Agent cần gửi metrics/logs.

{{< netmonimg src="images/netmon-workshop/18-ec2-instances-netmon-list.png" alt="Danh sách EC2 Instances" caption="Ảnh 18 – Danh sách EC2 Instances" >}}


{{< netmonimg src="images/netmon-workshop/19-ec2-netmon-ec2-server-details.png" alt="Thông tin máy EC2 netmon-ec2-server" caption="Ảnh 19 – Thông tin máy EC2 netmon-ec2-server" >}}


## Kiểm tra

- Instance ở trạng thái `Running` khi cần giám sát.
- CloudWatch hiển thị CPUUtilization cho đúng InstanceId.
- Chụp Instance name, loại instance, subnet, Security Group, status checks (che địa chỉ không muốn công khai).

> `Stop` EC2 thường dừng phí compute theo thời gian chạy nhưng không đồng nghĩa dừng toàn bộ phí EBS hoặc IP công cộng.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
