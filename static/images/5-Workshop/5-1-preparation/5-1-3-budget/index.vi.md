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
3. Cấu hình thông báo theo phần trăm budget. Trong quá trình thực hành, nhóm đã sửa một mốc xuống **25%**; có thể đặt thêm 50% và 100% theo chính sách nhóm.
4. Điền email người nhận cảnh báo; xác nhận email nếu AWS yêu cầu.
5. Vào **Cost Explorer** hoặc **Bills** để xem chi phí thật của EC2, EBS, CloudWatch, DynamoDB và các dịch vụ đã bật.

## Kiểm tra kết quả

- Budget nằm trong danh sách và email người nhận chính xác.
- Xác nhận đơn vị tiền tệ, chu kỳ tháng và mức cảnh báo.
- Chụp trang Budget, nhưng che địa chỉ email nếu công khai lên GitHub Pages.

> Chú ý: EC2 chạy liên tục, EBS, public IPv4, NAT Gateway (nếu có) và CloudWatch vượt hạn mức là các nguồn chi phí cần xem kỹ. Không khẳng định toàn bộ hệ thống là miễn phí.



![Sơ đồ minh họa quy trình]({{< relURL "images/netmon-workshop/netmon-cost-flow.png" >}})

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
