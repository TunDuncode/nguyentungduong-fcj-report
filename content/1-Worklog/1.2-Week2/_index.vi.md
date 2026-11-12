---
title: "Worklog Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---


### Mục tiêu tuần 2:

* Tìm hiểu kiến trúc mạng cốt lõi của AWS (Amazon VPC).
* Nắm vững các khái niệm về bảo mật luồng mạng và định tuyến.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 7 | - Tìm hiểu kiến trúc mạng AWS cơ bản <br>&emsp; + VPC <br>&emsp; + Subnets (Public/Private) <br>&emsp; + Route Tables <br> | 15/08/2026 | 15/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| chủ nhật | - Tìm hiểu các cổng kết nối mạng <br>&emsp; + Internet Gateway (IGW) <br>&emsp; + NAT Gateway <br> - Vẽ sơ đồ mạng 2 lớp (2-tier) | 16/08/2026 | 16/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - Khái niệm định tuyến CIDR block <br> - Tìm hiểu Security Groups vs Network ACLs <br>&emsp; + Stateful <br>&emsp; + Stateless <br> | 17/08/2026 | 17/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Thực hành:** <br>&emsp; + Tạo VPC tùy chỉnh <br>&emsp; + Cấu hình 1 Public & 1 Private Subnet <br>&emsp; + Gắn Internet Gateway | 18/08/2026 | 18/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Thực hành:** <br>&emsp; + Cấu hình Route Table <br>&emsp; + Triển khai NAT Gateway <br>&emsp; + Kiểm tra kết nối ping/SSH | 19/08/2026 | 19/08/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 2:

* Hiểu rõ kiến trúc mạng AWS và làm chủ các thành phần cốt lõi:
  * VPC (Virtual Private Cloud)
  * Subnets (Public vs Private)
  * Route Tables
  * ...

* Thiết kế thành công sơ đồ kiến trúc mạng 2-tier an toàn và tách biệt.

* Phân biệt rõ ràng các lớp bảo mật mạng:
  * Security Groups (Tường lửa mức Instance)
  * Network ACLs (Tường lửa mức Subnet)
  * ...

* Đã triển khai và cấu hình thành công một VPC tùy chỉnh từ con số không, bao gồm:
  * Phân chia dải IP (CIDR)
  * Internet Gateways
  * NAT Gateways
  * ...

* Kiểm chứng khả năng định tuyến và sự cô lập của mạng thông qua các lệnh ping và SSH thực tế.
* ...