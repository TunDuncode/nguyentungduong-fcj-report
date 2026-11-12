---
title: "5.1.1. Đăng nhập AWS và chọn Region"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.1.1. Đăng nhập AWS và chọn Region

## Mục tiêu

Chọn đúng Region `us-east-1`, kiểm tra quyền truy cập AWS Console và tạo cảnh báo ngân sách cho việc học tập.

## Các bước thực hiện

1. Đăng nhập AWS Console bằng IAM user hoặc tài khoản được quản trị viên cấp quyền; **không dùng chung root** cho cả nhóm.
2. Ở góc trên bên phải, chọn **United States (N. Virginia) — us-east-1**. Những dịch vụ theo vùng như EC2, DynamoDB, Lambda và API Gateway phải được kiểm tra trong cùng Region.

{{< netmonimg src="images/netmon-workshop/01-aws-region-us-east-1.png" alt="Chọn khu vực us-east-1" caption="Ảnh 01 – Chọn khu vực us-east-1" >}}


3. Mở **Billing and Cost Management → Budgets → Create budget**. Chọn kiểu **Cost budget**, đặt mức ngân sách theo kế hoạch nhóm (trong lần thử nghiệm trước: **20 USD/tháng**).
4. Tạo các thông báo tại ngưỡng **25%, 50% và 100%** nếu phù hợp với cấu hình ngân sách của nhóm. Kiểm tra email người nhận.

5. Vào **Cost Explorer** hoặc **Bills** để đối chiếu số tiền thực tế; đừng ghi ngân sách 20 USD thành chi phí đã phát sinh.

## Kiểm tra kết quả

- AWS Console hiển thị `us-east-1` khi mở các tài nguyên của dự án.
- Budget có thông báo đến địa chỉ email được chỉ định.
- Ghi nhận ảnh màn hình tên budget, ngưỡng cảnh báo và Region (che thông tin nhạy cảm).

> **Lưu ý chi phí:** AWS Budgets chỉ cảnh báo. EC2, EBS, CloudWatch, DynamoDB, SNS và các dịch vụ khác vẫn có thể phát sinh phí tùy cấu hình và mức sử dụng.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
