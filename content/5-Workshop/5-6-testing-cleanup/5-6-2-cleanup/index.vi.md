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

{{< netmonimg src="images/netmon-workshop/02-aws-budget-overview.png" alt="Tổng quan ngân sách NetMon" caption="Ảnh 02 – Tổng quan ngân sách NetMon" >}}


{{< netmonimg src="images/netmon-workshop/03-aws-budget-history.png" alt="Lịch sử ngân sách" caption="Ảnh 03 – Lịch sử ngân sách" >}}


{{< netmonimg src="images/netmon-workshop/04-aws-monthly-cost-history.png" alt="Lịch sử chi phí hàng tháng" caption="Ảnh 04 – Lịch sử chi phí hàng tháng" >}}


{{< netmonimg src="images/netmon-workshop/05-budget-alerts-25-50-100.png" alt="Ba ngưỡng cảnh báo 25%, 50%, 100%" caption="Ảnh 05 – Ba ngưỡng cảnh báo 25%, 50%, 100%" >}}

3. Mở **EC2 → Instances**: nếu không cần giám sát, cân nhắc **Stop** instance. Hiểu rằng EBS và một số tài nguyên gắn kèm vẫn có thể tính phí.

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
