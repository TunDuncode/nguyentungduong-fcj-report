---
title: "5.1.3. Thiết lập AWS Budgets và kiểm soát chi phí"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.1.3. Thiết lập AWS Budgets và kiểm soát chi phí

## Mục tiêu

Thiết lập mức theo dõi chi phí khi học tập trên AWS. **Budget 20 USD là ngưỡng theo dõi, không phải số tiền đã chi và cũng không tự khóa tài nguyên**.

## Các bước thao tác

1. Tại AWS Console, mở **Billing and Cost Management → Budgets → Create budget**; chọn **Cost budget**.
2. Chọn chu kỳ **Monthly** và nhập mức dự kiến **20 USD**. Điền tên rõ nghĩa, chẳng hạn `netmon-monthly-budget`.

{{< netmonimg src="images/netmon-workshop/02-aws-budget-overview.png" alt="Tổng quan ngân sách NetMon" caption="Ảnh 02 – Tổng quan ngân sách NetMon" >}}

3. Cấu hình thông báo theo phần trăm budget. Trong quá trình thực hành, nhóm đã sửa một mốc xuống **25%**; có thể đặt thêm 50% và 100% theo chính sách nhóm.

{{< netmonimg src="images/netmon-workshop/05-budget-alerts-25-50-100.png" alt="Ba ngưỡng cảnh báo 25%, 50%, 100%" caption="Ảnh 05 – Ba ngưỡng cảnh báo 25%, 50%, 100%" >}}

4. Điền email người nhận cảnh báo; xác nhận email nếu AWS yêu cầu.
5. Vào **Cost Explorer** hoặc **Bills** để xem chi phí thật của EC2, EBS, CloudWatch, DynamoDB và các dịch vụ đã bật.

{{< netmonimg src="images/netmon-workshop/03-aws-budget-history.png" alt="Lịch sử ngân sách" caption="Ảnh 03 – Lịch sử ngân sách" >}}


{{< netmonimg src="images/netmon-workshop/04-aws-monthly-cost-history.png" alt="Lịch sử chi phí hàng tháng" caption="Ảnh 04 – Lịch sử chi phí hàng tháng" >}}


## Kiểm tra kết quả

- Budget nằm trong danh sách và email người nhận chính xác.
- Xác nhận đơn vị tiền tệ, chu kỳ tháng và mức cảnh báo.
- Chụp trang Budget, nhưng che địa chỉ email nếu công khai lên GitHub Pages.

> Chú ý: EC2 chạy liên tục, EBS, public IPv4, NAT Gateway (nếu có) và CloudWatch vượt hạn mức là các nguồn chi phí cần xem kỹ. Không khẳng định toàn bộ hệ thống là miễn phí.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
