---
title: "3.2 Hạn chế sập server và duy trì hệ thống ổn định trên AWS"
weight: 2
chapter: false
---

## Giới thiệu

Không có máy chủ nào đảm bảo hoạt động ổn định tuyệt đối, kể cả khi triển khai trên AWS. Lượng truy cập tăng đột biến, CPU hoặc RAM quá tải, lỗi phần mềm và sự cố hạ tầng đều có thể khiến dịch vụ bị gián đoạn. Vì vậy, ngay từ khi thiết kế hệ thống, chúng ta nên chuẩn bị phương án phòng ngừa và khôi phục sự cố.

## Các giải pháp nên áp dụng trên AWS

- **Amazon CloudWatch:** Theo dõi hiệu suất và thiết lập cảnh báo qua Amazon SNS để phát hiện sớm dấu hiệu bất thường.
- **Elastic Load Balancing (ELB):** Phân phối lượng truy cập đến các máy chủ đang hoạt động tốt, tránh dồn tải vào một máy chủ.
- **EC2 Auto Scaling:** Tự động điều chỉnh số lượng máy chủ theo nhu cầu và thay thế máy chủ lỗi dựa trên kiểm tra sức khỏe.
- **Multi-AZ:** Triển khai máy chủ tại nhiều vùng sẵn sàng trong cùng một Region để giảm ảnh hưởng khi một vùng gặp sự cố.
- **AWS Backup:** Sao lưu dữ liệu định kỳ và kiểm thử khả năng khôi phục để hạn chế mất dữ liệu.

![Kiến trúc EC2 Auto Scaling kết hợp Application Load Balancer](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png)

*Hình 1. Kiến trúc cân bằng tải và triển khai EC2 tại nhiều Availability Zone. Nguồn: [AWS Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/tutorial-ec2-auto-scaling-load-balancer.html).*

Ví dụ, khi một EC2 gặp sự cố, bộ cân bằng tải có thể chuyển yêu cầu mới sang các máy chủ còn khỏe mạnh. Auto Scaling có thể thay thế máy chủ lỗi nếu cấu hình kiểm tra sức khỏe phù hợp. Các máy chủ còn lại cần đủ công suất để phục vụ người dùng, đồng thời dữ liệu cũng phải có phương án dự phòng.

![Quy trình mở rộng số lượng máy chủ EC2](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/scale-out-diagram.png)

*Hình 2. Quy trình đưa EC2 mới vào phục vụ khi mở rộng. Nguồn: [AWS Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-lifecycle.html).*

## Lựa chọn phương án mở rộng phù hợp

| Tiêu chí | Mở rộng theo chiều dọc (Vertical Scaling) | Mở rộng theo chiều ngang (Horizontal Scaling) |
| --- | --- | --- |
| Phương pháp | Tăng CPU, RAM | Tăng số lượng máy chủ |
| Triển khai | Đơn giản hơn | Phức tạp hơn |
| Khả năng chịu lỗi | Hạn chế nếu chỉ có một máy | Tốt hơn nếu có dự phòng |
| Khả năng mở rộng | Giới hạn cấu hình máy | Linh hoạt hơn |

Với hệ thống nhỏ, có thể bắt đầu từ một máy chủ có cấu hình phù hợp, kết hợp giám sát và sao lưu. Đối với dịch vụ quan trọng cần hoạt động liên tục, nên ưu tiên nhiều máy chủ, cân bằng tải và triển khai Multi-AZ nếu ngân sách cho phép.

## Lời khuyên

Theo mình, thay vì cố gắng xây dựng một máy chủ không bao giờ bị sập, chúng ta nên xây dựng một hệ thống có khả năng tiếp tục hoạt động hoặc nhanh chóng khôi phục khi sự cố xảy ra. Hãy chủ động giám sát, kiểm thử khả năng chịu lỗi và lựa chọn giải pháp dự phòng phù hợp với nhu cầu thực tế. Không nhất thiết phải triển khai quá nhiều dịch vụ ngay từ đầu, nhưng không nên đợi đến khi hệ thống gặp sự cố mới chuẩn bị phương án xử lý.

## Link blog của tôi

https://www.facebook.com/groups/awsstudygroupfcj/permalink/2341484523283173/?rdid=ybztwhA7Gy935T5y#

## Tài liệu tham khảo

- [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/)
- [AWS – Thiết lập ứng dụng có cân bằng tải và tự động mở rộng](https://docs.aws.amazon.com/autoscaling/ec2/userguide/tutorial-ec2-auto-scaling-load-balancer.html)
- [AWS Well-Architected – Reliability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html)

#AWS #AWSFCAJ #EC2 #AutoScaling #HighAvailability
