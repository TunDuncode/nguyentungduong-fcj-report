---
title: "5.6.2. Kiểm tra chi phí và sao lưu minh chứng"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.6.2. Kiểm tra chi phí và sao lưu minh chứng

## Mục tiêu

Kết thúc buổi thực hành mà không tạo ra chi phí ngoài ý muốn, đồng thời giữ lại những tài nguyên nhóm còn cần cho demo.

## Kiểm tra chi phí

1. Mở **Billing → Cost Explorer / Bills** và ghi lại chi phí thực tế theo dịch vụ và theo Region.
2. Xem lại **AWS Budgets** và địa chỉ email nhận thông báo, nhất là khi gần ngưỡng 25%, 50%, 100% của kế hoạch 20 USD/tháng.
3. Mở **EC2 → Instances**: nếu không cần giám sát, cân nhắc **Stop** instance. Hiểu rằng EBS và một số tài nguyên gắn kèm vẫn có thể tính phí.

![Ba CloudWatch Alarm đã được tạo]({{< relURL "images/netmon-workshop/cloudwatch-alarms.webp" >}})

*Hình minh chứng: Ba CloudWatch Alarm đã được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Kiểm tra EBS Volumes/Snapshots, IP công cộng, NAT Gateway (nếu có), CloudWatch Logs retention và các tài nguyên tạo thử.
5. Không xóa `NetworkDevices`, `NetworkAlerts`, `netmon-api`, `netmon-save-alert` hoặc Cognito User Pool khi còn dùng cho demo và báo cáo.

## Khi kết thúc hẳn đồ án

- Xuất bản báo cáo và ảnh minh chứng cần thiết vào repository (đã che secrets).
- Ghi lại những tài nguyên phụ thuộc lẫn nhau: API Gateway → Lambda → DynamoDB; EventBridge → Lambda → DynamoDB; CloudWatch → SNS.
- Chỉ sau khi nhóm xác nhận không còn cần sử dụng, mới xóa tài nguyên theo thứ tự phụ thuộc và kiểm tra trang Billing ở kỳ tiếp theo.
- Không coi việc `Stop` EC2 là thao tác xóa toàn bộ tài nguyên hoặc chấm dứt tất cả khoản phí.

## Tổng kết

Workshop NetMon cung cấp quy trình thực hành từ VPC và EC2, giám sát CloudWatch, gửi cảnh báo SNS, lưu lịch sử bằng EventBridge/Lambda/DynamoDB đến bảo vệ HTTP API bằng Cognito. Kết quả cuối cùng cần được chứng minh bằng kịch bản kiểm thử đầu cuối thực tế.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
