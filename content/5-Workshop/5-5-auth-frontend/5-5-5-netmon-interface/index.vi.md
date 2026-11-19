---
title: "5.5.5. Vận hành giao diện quản lý NetMon"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.5.5. Vận hành giao diện quản lý NetMon

## Bước 1 – Cấu hình và kết nối

Mở NetMon bằng Live Server tại `http://localhost:5500/` và đăng nhập theo mục 5.5.4. Chọn **Cấu hình & kết nối**, kiểm tra Invoke URL, Region `us-east-1`, các route và thông tin Cognito. Trong ảnh, ngưỡng hiển thị CPU/RAM là 80% và chu kỳ làm mới 60 giây. Bấm **Lưu cấu hình** nếu thay đổi. Các thiết lập này lưu tại trình duyệt, không tự sửa ngưỡng CloudWatch hay Lambda; không nhập AWS Secret Access Key.

{{< netmonimg src="images/netmon-workshop/69-netmon-configuration-connection.png" alt="Cấu hình API, ngưỡng hiển thị và chu kỳ làm mới" caption="Ảnh 69 – Cấu hình API, ngưỡng hiển thị và chu kỳ làm mới" >}}

## Bước 2 – Tổng quan hệ thống

Chọn **Tổng quan**. Dashboard hiển thị số thiết bị, số đang hoạt động, số bất thường, số cảnh báo chưa xử lý và xu hướng CPU/RAM lấy mẫu tại trình duyệt. Ở ảnh minh chứng ban đầu, cả 5 thiết bị hoạt động, không có thiết bị bất thường.

{{< netmonimg src="images/netmon-workshop/58-netmon-dashboard-overview.png" alt="Tổng quan hệ thống với 5 thiết bị đang hoạt động" caption="Ảnh 58 – Tổng quan hệ thống với 5 thiết bị đang hoạt động" >}}

Cuộn xuống để xem cảnh báo gần đây và trạng thái tích hợp AWS. Ảnh cho thấy API Gateway/DynamoDB, dữ liệu cảnh báo và CloudWatch Metrics có phản hồi; SNS vẫn ở trạng thái chưa xác nhận từ frontend, không thể dùng ảnh này để kết luận email đã gửi.

{{< netmonimg src="images/netmon-workshop/59-netmon-dashboard-aws-integration.png" alt="Cảnh báo gần đây và trạng thái tích hợp AWS" caption="Ảnh 59 – Cảnh báo gần đây và trạng thái tích hợp AWS" >}}

## Bước 3 – Quản lý thiết bị

Chọn **Quản lý thiết bị**. Có thể tìm theo tên, mã, IP hoặc vị trí và lọc theo trạng thái. Khi dùng nguồn AWS, thao tác CRUD đi qua API Gateway → Lambda → DynamoDB.

{{< netmonimg src="images/netmon-workshop/60-netmon-device-list.png" alt="Danh sách và bộ lọc thiết bị" caption="Ảnh 60 – Danh sách và bộ lọc thiết bị" >}}

### 3.1. Thêm thiết bị

Bấm **Thêm thiết bị**, nhập mã `TEST005`, tên `Switch Test`, loại Switch, IP `10.0.0.99`, vị trí tầng 4 và trạng thái ONLINE. Nhập CPU/RAM 95% để kiểm thử ngưỡng, rồi bấm **Lưu thiết bị**. Đây là chỉ số mô phỏng, không phải phép đo từ Switch vật lý.

{{< netmonimg src="images/netmon-workshop/61-netmon-add-device.png" alt="Thêm thiết bị Switch Test với CPU và RAM 95%" caption="Ảnh 61 – Thêm thiết bị Switch Test với CPU và RAM 95%" >}}

Sau khi lưu, dòng thiết bị xuất hiện với nhãn Cảnh báo và hai chỉ số 95%. Nhãn hiển thị có thể khác với trạng thái ONLINE trong bản ghi do vượt ngưỡng cấu hình.

{{< netmonimg src="images/netmon-workshop/62-netmon-device-warning.png" alt="Switch Test được đánh dấu cảnh báo ở mức 95%" caption="Ảnh 62 – Switch Test được đánh dấu cảnh báo ở mức 95%" >}}

### 3.2. Xem chi tiết

Bấm **Xem** ở dòng TEST005 để kiểm tra mã, tên, IP, vị trí, trạng thái và chỉ số.

{{< netmonimg src="images/netmon-workshop/63-netmon-device-detail.png" alt="Xem chi tiết thiết bị TEST005" caption="Ảnh 63 – Xem chi tiết thiết bị TEST005" >}}

### 3.3. Chỉnh sửa thiết bị

Bấm **Sửa**, điều chỉnh thông tin cần thiết rồi bấm **Lưu thiết bị**. Ảnh minh họa biểu mẫu chỉnh sửa; chưa chứng minh riêng việc lưu một giá trị mới.

{{< netmonimg src="images/netmon-workshop/64-netmon-edit-device.png" alt="Biểu mẫu chỉnh sửa thiết bị" caption="Ảnh 64 – Biểu mẫu chỉnh sửa thiết bị" >}}

### 3.4. Xóa thiết bị

Bấm **Xóa** tại dòng Switch Test và chọn OK trong hộp thoại xác nhận. Chỉ xóa thiết bị thử nghiệm.

{{< netmonimg src="images/netmon-workshop/65-netmon-delete-confirmation.png" alt="Hộp thoại xác nhận xóa Switch Test" caption="Ảnh 65 – Hộp thoại xác nhận xóa Switch Test" >}}

Sau khi xóa, kiểm tra danh sách trở về 5 thiết bị và không còn TEST005.

{{< netmonimg src="images/netmon-workshop/66-netmon-device-list-after-delete.png" alt="Danh sách trở về 5 thiết bị sau khi xóa" caption="Ảnh 66 – Danh sách trở về 5 thiết bị sau khi xóa" >}}

## Bước 4 – Giám sát và phát hiện bất thường

Theo dõi CPU/RAM ở Tổng quan và mở **Hiệu năng & Metrics** để kiểm tra dữ liệu theo nguồn. EC2 sử dụng chỉ số CloudWatch khi có cấu hình tương ứng; Router/Switch dùng dữ liệu mô phỏng. Tại lần chụp khác, Dashboard có 6 thiết bị, 1 thiết bị bất thường: Router-A002 CPU 93%, RAM 94%. Số cảnh báo chưa xử lý vẫn là 0; nhãn bất thường trên UI không đồng nghĩa đã tạo cảnh báo AWS hoặc gửi SNS.

{{< netmonimg src="images/netmon-workshop/70-netmon-dashboard-abnormal-device.png" alt="Dashboard phát hiện Router-A002 có CPU 93% và RAM 94%" caption="Ảnh 70 – Dashboard phát hiện Router-A002 có CPU 93% và RAM 94%" >}}

## Bước 5 – Trung tâm cảnh báo

Chọn **Cảnh báo & sự cố**, xem thời điểm, thiết bị, sự cố, mức độ và trạng thái. Dữ liệu được hiển thị từ NetworkAlerts qua API Gateway. Ảnh ghi nhận các sự kiện đã xử lý và đã trở về OK. Khi có sự cố mới, kiểm tra trước khi xác nhận; xác nhận không tự đặt CloudWatch Alarm về OK.

{{< netmonimg src="images/netmon-workshop/67-netmon-alert-center.png" alt="Trung tâm cảnh báo và sự cố" caption="Ảnh 67 – Trung tâm cảnh báo và sự cố" >}}

## Bước 6 – Sơ đồ mạng và hạ tầng

Mở **Sơ đồ hạ tầng** để tham khảo mô hình được thiết kế. Các Router/Switch mô phỏng không chứng minh kết nối vật lý hoặc khả năng tự khám phá topology. Chưa có ảnh riêng của trang này trong bộ minh chứng.

## Bước 7 – Nhật ký lịch sử

Chọn **Nhật ký lịch sử** để tìm thao tác hoặc thiết bị. Ảnh cho thấy thao tác thêm TEST005 lúc 15:48:50 và xóa lúc 15:49:37 ngày 18/11/2026, nguồn Trình duyệt. Phân biệt nhật ký thao tác cục bộ với lịch sử cảnh báo AWS/DynamoDB; không coi log trình duyệt là audit log tập trung. Dùng **Tải lại lịch sử AWS** để cập nhật phần dữ liệu AWS.

{{< netmonimg src="images/netmon-workshop/68-netmon-history-log.png" alt="Nhật ký thao tác trên trình duyệt" caption="Ảnh 68 – Nhật ký thao tác trên trình duyệt" >}}

## Kết quả ghi nhận

Giao diện NetMon Cloud minh họa việc xem danh sách, thêm, xem chi tiết, mở biểu mẫu chỉnh sửa, xóa thiết bị thử, đánh dấu bất thường, xem cảnh báo, nhật ký và cấu hình. Để xác minh lưu dữ liệu ở AWS, đối chiếu DynamoDB và log Lambda. Kiểm thử email SNS, số liệu EC2 chi tiết và sơ đồ cần minh chứng riêng.

[← Về chương](../)
