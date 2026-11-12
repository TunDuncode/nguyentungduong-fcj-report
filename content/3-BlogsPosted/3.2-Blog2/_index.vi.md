---
title: "3.2. Giám sát EC2 và ghi nhận cảnh báo trên AWS"
date: 2026-11-12T00:00:00+07:00
weight: 2
chapter: false
draft: false
---

## 1. Bài toán giám sát trong đồ án NetMon

Trong hệ thống quản lý mạng, chỉ có danh sách thiết bị là chưa đủ. Người quản trị còn cần biết máy chủ có đang hoạt động ổn định không, khi nào xuất hiện chỉ số bất thường và sự cố đã được xử lý hay chưa. Vì vậy, nhóm kết hợp **Amazon CloudWatch, Amazon SNS, Amazon EventBridge, AWS Lambda và DynamoDB** để triển khai luồng theo dõi và ghi nhận cảnh báo.

Phần EC2 và CloudWatch được nhóm thực hành trên máy chủ **`netmon-ec2-server`** chạy Ubuntu 24.04, kết hợp dữ liệu mô phỏng của các thiết bị mạng khác. Trong quá trình phối hợp, em tập trung tìm hiểu cách dữ liệu cảnh báo được chuyển tới API và trang lịch sử của ứng dụng.

## 2. Luồng giám sát và cảnh báo

**Luồng gửi thông báo:**

`EC2 → CloudWatch metrics → CloudWatch Alarm → Amazon SNS → Email`

**Luồng lưu lịch sử sự kiện:**

`Alarm đổi trạng thái → Amazon EventBridge → Lambda netmon-save-alert → DynamoDB NetworkAlerts`

Hai luồng này phục vụ những mục đích khác nhau: **SNS** giúp người quản trị biết sớm có cảnh báo, còn **DynamoDB** giúp tra cứu lịch sử, thời điểm nhận cảnh báo và trạng thái xử lý trên dashboard.

## 3. Các chỉ số được theo dõi

- **CPU:** thể hiện mức sử dụng bộ xử lý của máy chủ EC2.
- **RAM:** thể hiện tình trạng sử dụng bộ nhớ hệ điều hành.
- **Ổ đĩa:** giúp phát hiện nguy cơ hết dung lượng lưu trữ.
- **Trạng thái Alarm:** ví dụ `OK`, `ALARM`, `INSUFFICIENT_DATA`.

Một điều em cần lưu ý là CloudWatch có metric `CPUUtilization` cho EC2, nhưng **RAM và mức sử dụng hệ thống tệp không phải lúc nào cũng có sẵn**. Để thu thập số liệu RAM/đĩa từ hệ điều hành, thường cần cài và cấu hình **CloudWatch Agent** hoặc tự xuất custom metrics. Không nên mô tả RAM là metric mặc định của EC2.

## 4. Thiết lập ngưỡng và thử nghiệm

Trong bài thực hành, nhóm đã tạo các CloudWatch Alarms và thử cơ chế thông báo qua SNS. Khi thiết lập Alarm, cần quan tâm bốn yếu tố:

1. **Metric và dimension:** có đúng instance hoặc nguồn giám sát hay không.
2. **Ngưỡng và phép so sánh:** giá trị bao nhiêu thì coi là bất thường.
3. **Evaluation periods:** điều kiện phải duy trì bao lâu trước khi Alarm chuyển trạng thái.
4. **Action:** Alarm có gửi đến đúng SNS topic đã xác nhận subscription hay không.

Các ngưỡng trong môi trường demo cần giải thích là cấu hình thử nghiệm, **không phải ngưỡng tối ưu cho mọi doanh nghiệp**. Khi thay đổi ngưỡng, nên ghi lại để tránh nhầm với cảnh báo chi phí trên AWS Budgets — hai loại cảnh báo này hoàn toàn khác nhau.

## 5. Lưu lịch sử vào DynamoDB

Nhóm sử dụng bảng **`NetworkAlerts`** để ghi lại sự kiện cảnh báo. Một mục lịch sử nên có các thông tin như tên Alarm, tên thiết bị/EC2 liên quan, thời gian, mức độ, trạng thái và thời điểm cập nhật.

Trong giao diện, em đề xuất phân biệt **Mới tiếp nhận** và **Đã xử lý** để người quản trị không chỉ đọc được email mà còn theo dõi vòng đời sự cố. Khi xử lý sự kiện tự động, cũng cần cân nhắc các thông báo lặp, định dạng thời gian và cách định danh duy nhất cho mỗi sự kiện.

## 6. Kinh nghiệm rút ra

Từ bài thực hành, em hiểu rằng giám sát không đơn giản là vẽ một biểu đồ CPU. Hệ thống cần liên kết được **dữ liệu đo → ngưỡng phát hiện → thông báo → lịch sử → thao tác xử lý**. Việc kiểm thử trên EC2 thực giúp dễ phát hiện sai khác so với chỉ mô phỏng trên giao diện.

**Hướng cải thiện:** chuẩn hóa định dạng bản ghi lịch sử, kiểm soát thông báo trùng, bổ sung bộ lọc thời gian và thống kê trạng thái cảnh báo. Chi phí CloudWatch, lưu log, Lambda, DynamoDB và EC2 cần được theo dõi qua AWS Billing/Budgets trong suốt quá trình thử nghiệm.

## 7. Tài liệu tham khảo

- [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [Metric RAM/ổ đĩa từ CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/metrics-collected-by-CloudWatch-agent.html)
- [Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)

*Trạng thái bài viết: Bản thảo cá nhân, chưa xuất bản lên AWS Study Group.*
