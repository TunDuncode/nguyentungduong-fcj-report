---
title: "Blog 3: Cách AWS tối ưu hóa AI cho robot tự hành ngoài thực tế"
date: 2026-07-08
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---


# CÁCH AWS TỐI ƯU HÓA AI CHO ROBOT TỰ HÀNH (CASE STUDY: AIGEN)

Bài blog từ AWS phân tích cách công ty Aigen giải quyết bài toán đưa AI xuống chạy ở môi trường thực tế cho hệ thống robot nông nghiệp tự động diệt cỏ dại chạy bằng năng lượng mặt trời. Hệ thống Edge AI này phải đối mặt với các vấn đề cốt lõi: kết nối Internet ngoài đồng chập chờn nên khó gửi data về server, dữ liệu ảnh khổng lồ gây tốn kém và chậm trễ nếu gán nhãn thủ công, và phần cứng trên robot quá giới hạn để chạy các mô hình AI khổng lồ.

Các điểm chính cần nắm về cách Aigen tối ưu hóa với hệ sinh thái AWS SageMaker:

* Hệ thống dùng GenAI kết hợp các mô hình nền tảng thị giác (như SAM2, Grounding DINO) để tự động phân vùng và vẽ bounding box (Auto-labeling).
* Kỹ thuật Active Learning được áp dụng để hệ thống tự động lọc ra những tấm ảnh khó xử lý nhất (ví dụ: góc sáng lạ, cây bị che khuất) và đẩy cho con người kiểm tra lại.
* Nhờ quy trình tự động hóa này, thời gian xử lý ảnh giảm mạnh từ gần 15 phút xuống vỏn vẹn 41 giây/ảnh, đồng thời cắt giảm chi phí dán nhãn lên tới 22.5 lần.
* Quá trình "chưng cất" mô hình (Model Distillation & Quantization) để giải bài toán phần cứng yếu được chia thành 4 cấp độ từ lớn đến nhỏ.
* Các cấp độ bao gồm: Foundation Models siêu lớn tổng quát chạy trên cloud (Lớp 1), Expert & Student Models được chưng cất nhỏ lại cho các tác vụ cụ thể (Lớp 2, 3), và cuối cùng là Edge Models (Lớp 4).
* Ở Lớp 4, mô hình được ép kiểu (Quantization) về chuẩn INT8 và chuyển sang định dạng TFLite. Khối lượng mô hình lúc này chỉ còn khoảng 2MB và tiêu thụ vỏn vẹn 1.5W điện nhưng vẫn đảm bảo chạy mượt theo thời gian thực trên bo mạch của robot.
* Robot duy trì một vòng lặp cập nhật liên tục (Closed-loop): tải data thô lên AWS S3 khi có mạng -> Tự động gán nhãn -> Train lại mô hình trên cụm GPU mạnh của Cloud -> Đẩy bản cập nhật siêu nhẹ ngược về lại cánh đồng để robot thích nghi ngay với môi trường mới.
* Việc đưa AI ra khỏi phòng lab để chạy mượt trên thực tế đòi hỏi sự kết hợp khéo léo giữa năng lực tính toán cực mạnh của Cloud và kỹ thuật nén mô hình tối đa ở thiết bị Edge.

### 1. Kiến trúc phân tầng và chưng cất mô hình AI
![Ảnh 1: Mô hình đi qua 4 cấp độ chưng cất](/images/3-Blogs/blog3-1.jpeg)
*Chú thích: Mô hình đi qua 4 cấp độ: từ Foundation (siêu lớn, chạy trên Cloud) -> Expert -> Student -> Edge (chỉ còn 2MB, tiêu thụ 1.5W chạy trên bo mạch robot).*

### 2. Vòng lặp khép kín cập nhật dữ liệu (Closed-loop)
![Ảnh 2: Vòng lặp khép kín của AWS SageMaker](/images/3-Blogs/blog3-2.jpeg)
*Chú thích: Dữ liệu thô từ robot tải lên S3 -> tự động gán nhãn -> Train lại mô hình trên Cloud -> đẩy bản cập nhật Edge về cánh đồng.*

**Tham khảo bài viết gốc trên blog AWS:** [How Aigen transformed agricultural robotics for sustainable farming with Amazon SageMaker AI](https://aws.amazon.com/blogs/architecture/how-aigen-transformed-agricultural-robotics-for-sustainable-farming-with-amazon-sagemaker-ai/)