---
title: "4.2. Cloud & AI Infrastructure Meetup – 24/10/2026"
date: 2026-10-24T00:00:00+07:00
weight: 2
chapter: false
---

# 4.2.  Hành trình lên mây của Riot Games

## 1. Thông tin chương trình

- **Tên chính thức:** Recap re 2024 – Hành trình lên mây của Riot Games
- **Ngày:** Thứ Bảy, 14/11/2026
- **Giờ theo thông báo ban tổ chức:** 9:00-12:00 
- **Địa điểm:** Tầng 7, Grand Terra, 36 Cát Linh, Hà Nội (văn phòng AWS Hà Nội)

## 2. Giới thiệu

Ngày 14/11/2026, trong buổi FCAJ Weekly Meetup tôi đã tham dự phần chia sẻ của diễn giả Nhân Nguyễn về hành trình Riot Games chuyển hạ tầng lên AWS. Đây là chủ đề tôi thấy khá gần với những gì mình đang tìm hiểu: một hệ thống lớn vận hành ra sao, khi nào thì nên lên mây, và lên rồi thì giải quyết được gì mà ở lại thì không.

## 3. Nội dung chính
### 3.1. Khó khăn khi chưa lên mây
Không chạy được nhiều game cùng lúc trên một hạ tầng

Mỗi game cần cấu hình và tài nguyên riêng, dẫn đến lãng phí

Khó mở rộng theo mùa hoặc sự kiện vì phải chờ mua và lắp server mới

Server đặt cố định một chỗ, người chơi ở xa chịu độ trễ cao

Vận hành nặng: vá lỗi, sao lưu, nâng cấp từng máy thủ công

Chi phí cố định cao vì datacenter chạy 24/7

### 3.2.  Lên mây giải quyết được gì
Dùng Amazon EKS để chạy nhiều game trên cùng hạ tầng, tự động co giãn theo nhu cầu

Mở rộng nhanh, thêm server trong vài phút thay vì vài tuần

Chuyển cơ sở dữ liệu lên RDS/Aurora để cấp phát nhanh và ổn định hơn

Chi phí linh hoạt, trả theo mức dùng thực tế

Đội ngũ tập trung vào game thay vì vật lộn với hạ tầng
### 3.3.  Dùng gì để không bị độ trễ

AWS Local Zones: đặt server đấu game ngay tại khu đô thị lớn, gần người chơi — không phải "nhảy" ra region xa rồi quay lại

AWS Outposts: phần cứng AWS đặt trong datacenter của Riot ở nơi Local Zones chưa phủ tới, giảm thêm độ trễ đáng kể

AWS Global Accelerator: tối ưu tuyến mạng cho gói tin đi đường ngắn và ổn định nhất đến server gần nhất, không đi qua mạng công cộng thông thường

Kết quả: VALORANT giữ độ trễ dưới 35ms — mục tiêu bắt buộc để không bị "peeker's advantage" (nhìn trước ăn lợi thế) trong game bắn súng phản xạ.
### 3.4.  Chuyển hệ điều hành thì riot gặp khó khăn gì?
Việc chuyển từ Windows sang Linux không hề đơn giản. Vì code C++ cũ đã chạy trên Windows 15 năm, nó chứa nhiều "undefined behavior" (hành vi không xác định) – tức là code chạy được trên Windows theo một cách rất cụ thể, nhưng khi biên dịch và chạy trên Linux lại cho ra kết quả khác.

Một ví dụ thực tế đã xảy ra với tướng Gangplank:

Trên Windows, các thùng thuốc súng của Gangplank được xử lý theo một thứ tự cố định, giúp người chơi thực hiện combo đặt nhiều thùng và kích nổ cùng lúc.

Khi máy chủ chuyển sang Linux, thứ tự xử lý này thay đổi. Kết quả là combo nhiều thùng của Gangplank không còn hoạt động ở những khu vực đã chuyển sang Linux, trong khi vẫn bình thường ở khu vực còn chạy Windows.

Đội ngũ phải truy vết và phát hiện nguyên nhân đến từ một container trong thư viện chuẩn C++ có thứ tự duyệt phần tử khác nhau giữa hai hệ điều hành.

Tóm lại: Riot Games đã chuyển máy chủ game từ Windows sang Linux để tối ưu vận hành, nhưng vẫn dùng C++. Chính việc chuyển hệ điều hành này đã làm lộ ra những lỗi ẩn trong code C++ cũ, gây ra những thay đổi hành vi trong game mà ví dụ điển hình là combo của Gangplank.

## 4. Liên hệ với đề tài AWS NetMon

Chọn region gần người dùng: Riot kéo server gần người chơi để giảm độ trễ — NetMon cũng nên đặt EC2, CloudWatch, Lambda cùng region gần nơi monitoring

CloudWatch là trung tâm: cấu hình Alarm + SNS đúng ngưỡng, đúng quyền, tránh báo động giả hoặc bỏ sót sự cố

Chọn dịch vụ theo bài toán: NetMon quy mô nhỏ chỉ cần Lambda + API Gateway + DynamoDB, không thêm tầng phức tạp

Chi phí ẩn: để ý CloudWatch Logs, số lần gọi API Gateway, dung lượng DynamoDB — dễ vượt dự toán hơn tiền EC2

Kiểm thử khi đổi môi trường: Riot chuyển Windows sang Linux làm lộ lỗi ẩn (combo Gangplank hỏng) — NetMon khi đổi từ local sang Lambda thật cũng phải test lại toàn bộ luồng, không giả định "chạy được ở đây thì chạy được ở kia"

Sau sự kiện, tôi nhận thấy việc chọn công nghệ không chỉ dựa vào tính năng mà còn cần cân nhắc hiệu suất, chi phí và khả năng quản trị khi vận hành thật.

## 5. Hình ảnh minh chứng

**Ảnh 1:** Toàn cảnh buổi Meetup tại tầng 7, Grand Terra ngày 14/11/2026 *(sử dụng ảnh bạn chụp hoặc ảnh ban tổ chức cho phép dùng)*.

![ảnh minh chứng](static/images/minh-chung/event2.jpg)



## 6. Tài liệu tham khảo

- [Trang chương trình, nội dung bài nói và diễn giả](https://ocgroups.dev/cncf/group/d2e22fa/event/5z4fnze)
- [Thông báo chính thức từ VietOpenInfra](https://vn.linkedin.com/posts/voi-vn_vietopeninfra-cloudnativevietnam-awscommunityvietnam-activity-7516060456709550080-yaxC)
- [Bài tổng kết của ban tổ chức](https://vn.linkedin.com/posts/voi-vn_vietopeninfra-cloudnativevietnam-awsfcaj-activity-7521419750535610369-mDaT)

*Lưu ý: Nội dung trên tổng hợp thông tin được công bố. Không mô tả các hoạt động cá nhân chưa có minh chứng, ví dụ phát biểu, nhận giải thưởng hoặc chụp ảnh cùng diễn giả.*
