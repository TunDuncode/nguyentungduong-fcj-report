---
title: "2. Đề xuất"
date: 2026-11-12
weight: 2
draft: false
---

# ĐỀ XUẤT DỰ ÁN

**Tên đề tài:** Xây dựng hệ thống quản lý và giám sát hạ tầng mạng doanh nghiệp vừa và nhỏ trên AWS tích hợp dịch vụ Serverless.

**Hình thức thực hiện:** Đồ án nhóm (3 sinh viên), triển khai mô phỏng trên AWS tại khu vực **US East (N. Virginia) – `us-east-1`**.

## 1. Tóm tắt điều hành

Đề tài hướng tới xây dựng một hệ thống giúp doanh nghiệp vừa và nhỏ quản lý danh sách thiết bị mạng, theo dõi tài nguyên máy chủ và phát hiện sớm các dấu hiệu bất thường. Thay vì chỉ sử dụng bảng tính để ghi chép thiết bị hoặc đăng nhập vào từng máy chủ để kiểm tra, người quản trị có thể theo dõi thông tin trên một giao diện tập trung.

Nhóm lựa chọn **Amazon VPC và EC2** để mô phỏng hạ tầng mạng; **Amazon CloudWatch** để thu thập chỉ số CPU, RAM và dung lượng đĩa; **Amazon SNS** để gửi cảnh báo qua email; **Amazon EventBridge và AWS Lambda** để ghi nhận sự kiện; **Amazon DynamoDB** để lưu danh sách thiết bị và lịch sử cảnh báo. Phần quản lý thiết bị sử dụng **Amazon API Gateway, AWS Lambda và Amazon Cognito** để cung cấp API và kiểm soát truy cập.

Đề tài kết hợp một máy chủ EC2 với các dịch vụ Serverless, **không phải hệ thống Serverless 100%**. Mục tiêu chính là xây dựng được một mô hình có thể chạy thử, kiểm tra và trình bày rõ quá trình phát hiện — gửi — lưu — xử lý cảnh báo. Đây là mô hình phục vụ học tập, chưa phải sản phẩm triển khai cho doanh nghiệp thực tế.

---

## 2. Tuyên bố vấn đề

### 2.1. Vấn đề hiện tại

Ở các doanh nghiệp quy mô nhỏ, việc quản lý thiết bị và giám sát máy chủ thường phân tán. Thông tin thiết bị có thể được lưu riêng lẻ, tình trạng CPU/RAM khó theo dõi liên tục, còn người quản trị chỉ biết có sự cố khi dịch vụ đã chạy chậm hoặc ngừng hoạt động. Nếu không có nhật ký cảnh báo, việc kiểm tra sự cố đã được xử lý hay chưa cũng mất thời gian.

Ngoài ra, các giải pháp giám sát truyền thống có thể cần máy chủ giám sát riêng, nhân lực bảo trì và quy trình triển khai phức tạp. Với một đồ án giới hạn thời gian và ngân sách, nhóm cần một mô hình đủ đơn giản để tự triển khai nhưng vẫn thể hiện được quy trình quản trị hạ tầng mạng.

### 2.2. Giải pháp đề xuất

Hệ thống tập trung vào bốn chức năng chính:

1. **Quản lý thiết bị:** thêm, xem, chỉnh sửa, xóa và tìm kiếm thông tin thiết bị mạng qua API, dữ liệu lưu tại bảng `NetworkDevices`.
2. **Giám sát tài nguyên:** sử dụng CloudWatch để theo dõi CPU và các chỉ số RAM/đĩa được thu thập qua CloudWatch Agent hoặc chỉ số tùy chỉnh.
3. **Cảnh báo tự động:** cấu hình CloudWatch Alarms; dùng SNS gửi email và EventBridge chuyển sự kiện trạng thái cảnh báo sang Lambda để ghi lịch sử vào bảng `NetworkAlerts`.
4. **Giao diện quản trị:** xác thực với Cognito; hiển thị thiết bị, thông số, cảnh báo và trạng thái xử lý trên dashboard.

### 2.3. Lợi ích dự kiến

Mô hình giúp giảm thao tác kiểm tra thủ công, tập trung hóa thông tin và lưu được lịch sử khi xảy ra cảnh báo. Các dịch vụ được chia thành những khối riêng nên dễ kiểm thử và mở rộng trong tương lai. Chi phí sẽ được theo dõi bằng AWS Budgets; **ngân sách 20 USD/tháng là ngưỡng theo dõi, không phải cam kết hệ thống chỉ tốn 20 USD hoặc tự động dừng tính phí**.

---

## 3. Kiến trúc giải pháp

Hệ thống gồm hai luồng chính: **quản lý thiết bị qua API** và **giám sát — cảnh báo — lưu lịch sử**. Toàn bộ dịch vụ AWS được cấu hình và thử nghiệm chủ yếu tại `us-east-1`.

### 3.1. Sơ đồ kiến trúc hệ thống

{{< netmonarchitecture lang="vi" >}}

*Hình 3.1. Sơ đồ kiến trúc đề xuất cho hệ thống quản lý và giám sát NetMon trên AWS (sơ đồ thiết kế, không phải ảnh chụp AWS Console).*

### 3.2. Các thành phần sử dụng

| Thành phần | Vai trò trong hệ thống |
|---|---|
| **Amazon VPC** | Tạo mạng riêng `netmon-vpc` với CIDR `10.0.0.0/16`, tách public subnet và private subnet. |
| **Amazon EC2** | Chạy máy chủ mô phỏng `netmon-ec2-server` (Ubuntu 24.04 LTS, loại `t3.micro`). |
| **Security Groups và IAM** | Kiểm soát luồng truy cập mạng và quyền của EC2/Lambda theo nhu cầu. |
| **Amazon CloudWatch** | Theo dõi CPU, RAM, dung lượng đĩa, log và ba ngưỡng cảnh báo. |
| **Amazon SNS** | Gửi thông báo cảnh báo tới email đã xác nhận đăng ký. |
| **Amazon EventBridge** | Nhận sự kiện thay đổi trạng thái CloudWatch Alarm và chuyển tới Lambda. |
| **AWS Lambda** | `netmon-api` xử lý API; `netmon-save-alert` ghi sự kiện cảnh báo vào DynamoDB. |
| **Amazon API Gateway** | Cung cấp HTTP API để giao diện gọi các chức năng quản lý thiết bị, cảnh báo và metrics. |
| **Amazon Cognito** | Quản lý người đăng nhập và cung cấp JWT để API Gateway kiểm tra quyền truy cập. |
| **Amazon DynamoDB** | Hai bảng `NetworkDevices` và `NetworkAlerts` lưu thiết bị và nhật ký cảnh báo. |
| **AWS Budgets** | Giám sát mức chi phí so với ngân sách dự kiến. |

### 3.3. Luồng xử lý dữ liệu

**Luồng 1 — Quản lý thiết bị:** Người dùng đăng nhập qua Cognito → giao diện gọi API Gateway kèm token → API Gateway kiểm tra JWT → Lambda `netmon-api` đọc/ghi DynamoDB → trả dữ liệu thiết bị hoặc cảnh báo về giao diện.

**Luồng 2 — Giám sát và cảnh báo:** EC2 cung cấp số liệu CPU/RAM/đĩa → CloudWatch đánh giá ngưỡng → khi trạng thái Alarm thay đổi, hệ thống gửi thông báo qua SNS và phát sinh sự kiện cho EventBridge → Lambda `netmon-save-alert` ghi lại vào bảng `NetworkAlerts` → trang nhật ký hiển thị lịch sử để theo dõi xử lý.

Thiết kế VPC mô phỏng gồm **public subnet `10.0.0.0/20`**, **private subnet `10.0.128.0/20`**, route table riêng và Internet Gateway `netmon-igw`. EC2 thuộc public subnet. Private subnet được sử dụng để minh họa phân vùng mạng; không giả định đã có NAT Gateway hoặc máy chủ trong private subnet.

---

## 4. Triển khai kỹ thuật

### 4.1. Các giai đoạn thực hiện

1. **Khảo sát và chuẩn bị:** tìm hiểu AWS, lựa chọn vùng triển khai, phân chia nhiệm vụ, tạo AWS Budget và thiết kế sơ đồ kiến trúc.
2. **Dựng hạ tầng:** tạo VPC, subnet, route table, Internet Gateway, Security Group, IAM Role và một EC2 Ubuntu để mô phỏng máy chủ cần giám sát.
3. **Xây dựng Serverless API và cơ sở dữ liệu:** tạo `NetworkDevices`, `NetworkAlerts`; viết Lambda Python dùng `boto3`; cấu hình các route HTTP API và xác thực Cognito.
4. **Giám sát và hoàn thiện:** tạo CloudWatch metrics/alarms, SNS email, EventBridge rule, Lambda lưu cảnh báo; xây dựng giao diện và kiểm thử các luồng chức năng.

### 4.2. API và dữ liệu

Các route chính được thiết kế theo phương thức HTTP:

| Phương thức | Route | Mục đích |
|---|---|---|
| GET | `/devices` | Xem danh sách thiết bị. |
| POST | `/devices` | Thêm thiết bị. |
| GET | `/devices/{id}` | Xem chi tiết một thiết bị. |
| PUT | `/devices/{id}` | Cập nhật thiết bị. |
| DELETE | `/devices/{id}` | Xóa thiết bị. |
| GET | `/alerts` | Xem nhật ký cảnh báo. |
| PUT | `/alerts/{id}` | Cập nhật trạng thái xử lý cảnh báo. |
| GET | `/metrics` | Lấy chỉ số giám sát phục vụ dashboard. |

Bảng `NetworkDevices` có các thuộc tính như `deviceId`, `deviceName`, `deviceType`, `ipAddress`, `status`, `instanceId` và `region` tùy thiết bị. Bảng `NetworkAlerts` dùng `eventId` để nhận diện sự kiện; các trường nghiệp vụ gồm `alarmName`, `alarmState`, `alarmType`, `deviceId`, `eventTime` và `handlingStatus`.

### 4.3. Công nghệ và kiểm thử

- **Backend:** AWS Lambda viết bằng Python, dùng thư viện `boto3` làm việc với DynamoDB và CloudWatch.
- **Frontend:** giao diện quản lý dự kiến sử dụng HTML, CSS, JavaScript; phát triển bằng Visual Studio Code và chạy kiểm tra qua localhost.
- **Xác thực:** Cognito User Pool và JWT authorizer trong API Gateway; cấu hình CORS cho địa chỉ giao diện dùng để thử nghiệm.
- **Giám sát:** CloudWatch Alarms gồm `netmon-cpu-high-80`, `netmon-ram-high-80`, `netmon-disk-high-85`.
- **Kiểm thử:** kiểm tra API trả đúng dữ liệu, thao tác CRUD, điều kiện cảnh báo, email SNS, lưu lịch sử vào DynamoDB, phân quyền và giao diện.

Đồ án sử dụng ảnh chụp cấu hình AWS Console và kết quả thử nghiệm làm minh chứng trong phần **5. Workshop**, không coi mọi tính năng dự kiến đã hoàn thiện chỉ vì tài nguyên AWS đã được tạo.

### 4.4. Phân công nhóm

| Thành viên | Công việc chính |
|---|---|
| **Tùng Dương** | VPC, EC2, public/private subnet, route table, Internet Gateway, Security Group và bảo mật hạ tầng. |
| **Xuân Đức** | Lambda, API Gateway, DynamoDB, CRUD thiết bị và tích hợp dữ liệu. |
| **Mạnh Quân** | CloudWatch, cảnh báo, giao diện giám sát và kiểm thử. |

---

## 5. Lộ trình và mốc triển khai

Dự án dự kiến được thực hiện trong **12 tuần**, mỗi tuần một buổi thực hành. Các tuần có thể điều chỉnh theo tiến độ thực tế của nhóm.

| Tuần | Nội dung thực hiện | Kết quả cần có |
|---|---|---|
| **1** | Tìm hiểu đề tài, phạm vi và các dịch vụ AWS. | Xác định yêu cầu và phân công nhóm. |
| **2** | Vẽ kiến trúc tổng quát, chọn region và lập ngân sách. | Sơ đồ hệ thống, AWS Budget. |
| **3** | Tạo VPC, subnet, Internet Gateway và route table. | Mạng mô phỏng cơ bản. |
| **4** | Tạo Security Group, IAM Role và EC2 Ubuntu. | EC2 hoạt động trong VPC. |
| **5** | Thiết kế bảng DynamoDB. | `NetworkDevices`, `NetworkAlerts`. |
| **6** | Viết Lambda xử lý danh sách và CRUD thiết bị. | Lambda `netmon-api` và kiểm thử cơ bản. |
| **7** | Cấu hình API Gateway, các route và CORS. | API có thể được gọi từ client kiểm thử. |
| **8** | Thiết lập CloudWatch metrics và Alarm CPU/RAM/đĩa. | Dữ liệu metrics và ba ngưỡng cảnh báo. |
| **9** | Tích hợp SNS, EventBridge và Lambda ghi lịch sử. | Email cảnh báo, sự kiện lưu trong DynamoDB. |
| **10** | Cấu hình Cognito, JWT authorizer và đăng nhập. | Luồng xác thực cơ bản. |
| **11** | Hoàn thiện giao diện quản lý, nhật ký và kiểm thử tích hợp. | Demo các luồng chính, ghi nhận lỗi còn tồn tại. |
| **12** | Tổng hợp ảnh minh chứng, kiểm tra chi phí, viết tài liệu và báo cáo. | Workshop, đề xuất, kết quả kiểm thử và bài trình bày. |

---

## 6. Ước tính và kiểm soát ngân sách

Nhóm sử dụng AWS ở khu vực `us-east-1` với **AWS Cost Budget 20 USD/tháng** và các mốc thông báo khi chi phí thực tế vượt **25% (5 USD)**, **50% (10 USD)** và **100% (20 USD)** ngân sách. Đây là **mức cảnh báo được cấu hình**, không phải số tiền đã chi hoặc dự toán chi phí chính xác.

| Dịch vụ | Yếu tố có thể phát sinh chi phí | Cách kiểm soát |
|---|---|---|
| **EC2 và EBS** | Thời gian máy hoạt động, ổ đĩa và tài nguyên liên quan. | Dừng máy khi không thử nghiệm; kiểm tra ổ đĩa còn tồn tại. |
| **Địa chỉ IPv4 công khai** | Có thể phát sinh phí theo giờ. | Chỉ giữ địa chỉ khi thực sự cần. |
| **CloudWatch** | Alarm, log, metrics tùy chỉnh và thời gian lưu log. | Giới hạn dữ liệu thử nghiệm, đặt retention hợp lý. |
| **Lambda và API Gateway** | Số lần gọi, thời gian chạy và lưu lượng yêu cầu. | Tránh vòng lặp gọi API hoặc mô phỏng không giới hạn. |
| **DynamoDB** | Số lần đọc/ghi và dung lượng lưu trữ. | Giữ dữ liệu thử nghiệm ở quy mô nhỏ. |
| **SNS, EventBridge và Cognito** | Số sự kiện, thông báo và cách sử dụng dịch vụ. | Theo dõi usage, không tạo lưu lượng thử nghiệm quá mức. |

**Nguyên tắc:** đối chiếu AWS Billing/Cost Explorer với AWS Budgets trong suốt quá trình làm đồ án. Điều kiện Free Tier tùy loại tài khoản và thời điểm; không mặc định mọi dịch vụ đều miễn phí. Cảnh báo ngân sách **không tự động dừng EC2 hoặc các tài nguyên AWS**.

---

## 7. Đánh giá rủi ro

### 7.1. Rủi ro chính

| Rủi ro | Mức ảnh hưởng | Hướng xử lý |
|---|---|---|
| **Cấu hình Security Group quá rộng** | Cao | Không mở SSH (22) ra toàn Internet nếu không cần; áp dụng quyền truy cập tối thiểu. |
| **Lộ khóa hoặc dữ liệu tài khoản AWS khi đẩy GitHub** | Cao | Không commit Access Key, Secret Key, token và ảnh chứa dữ liệu nhạy cảm; che thông tin trước khi công khai. |
| **Lỗi xác thực JWT hoặc CORS** | Trung bình | Kiểm tra issuer, audience, scopes, callback URL và origin thực tế của frontend. |
| **Cảnh báo không gửi email hoặc thiếu lịch sử** | Trung bình | Kiểm tra SNS subscription đã xác nhận, CloudWatch action, EventBridge rule, Lambda permission và logs. |
| **Chi phí tăng ngoài dự kiến** | Trung bình–cao | Thiết lập AWS Budget, kiểm tra chi phí thường xuyên, tắt/xóa tài nguyên không dùng. |
| **Số liệu RAM/đĩa không cập nhật** | Trung bình | Kiểm tra CloudWatch Agent hoặc metric tùy chỉnh, namespace, dimension và quyền IAM. |

### 7.2. Kế hoạch dự phòng

Duy trì bản sao mã nguồn trên GitHub, phân quyền IAM theo nhiệm vụ, sử dụng dữ liệu mô phỏng khi chưa có đủ thiết bị vật lý và lưu lại ảnh thử nghiệm của từng bước. Khi một dịch vụ lỗi, kiểm tra CloudWatch Logs trước, sau đó kiểm thử riêng từng mắt xích trong luồng xử lý. Nếu cảnh báo không phát sinh thực tế, nhóm có thể sử dụng sự kiện thử nghiệm **được đánh dấu là test** để xác minh đường ghi lịch sử; không trình bày dữ liệu thử nghiệm như một sự cố thật.

---

## 8. Kết quả kỳ vọng

- **Quản lý thiết bị:** có API cho thêm, xem, sửa, xóa thiết bị; dữ liệu lưu được trong DynamoDB và hiển thị trên giao diện.
- **Giám sát EC2:** theo dõi được chỉ số CPU, RAM, đĩa và trạng thái máy chủ qua CloudWatch.
- **Phát hiện và thông báo:** cấu hình ngưỡng CPU/RAM 80%, đĩa 85%; SNS gửi email khi cảnh báo thay đổi theo thiết lập.
- **Nhật ký cảnh báo:** EventBridge và Lambda ghi được các sự kiện CloudWatch vào `NetworkAlerts`, kèm thời gian và trạng thái xử lý để tra cứu.
- **Bảo mật truy cập:** sử dụng Cognito và JWT để hạn chế API chỉ cho người dùng hợp lệ; phân quyền IAM phù hợp chức năng.
- **Báo cáo và trình diễn:** có sơ đồ kiến trúc, ảnh cấu hình thực tế, kịch bản thử nghiệm và Workshop có thể xem trên Hugo/GitHub Pages sau khi triển khai.

Kết quả cuối cùng được đánh giá bằng **những chức năng kiểm thử chạy được và bằng chứng trên AWS**, không chỉ dựa vào danh sách dịch vụ đã tạo. Mô hình có thể làm cơ sở phát triển tiếp thành hệ thống giám sát nhiều máy chủ, nhưng chưa thay thế một nền tảng giám sát doanh nghiệp hoàn chỉnh.
