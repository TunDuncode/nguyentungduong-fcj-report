---
title: "3.1. Xây dựng API quản lý thiết bị mạng với AWS Serverless"
date: 2026-11-12T00:00:00+07:00
weight: 1
chapter: false
draft: false
---

## 1. Vì sao em chọn Serverless cho phần quản lý thiết bị?

Trong đề tài NetMon, nhóm cần lưu thông tin thiết bị mạng và cung cấp chức năng **thêm, xem, sửa, xóa** cho người quản trị. Em phụ trách phần backend, gồm **AWS Lambda, Amazon API Gateway và Amazon DynamoDB**. Vì đây là mô hình học tập và mô phỏng, giải pháp Serverless giúp nhóm tập trung vào logic xử lý mà không phải tự duy trì một máy chủ API riêng.

Em sử dụng Region **us-east-1**, triển khai các tài nguyên cơ bản và thử gọi API từ giao diện chạy trên máy cá nhân. Phần EC2/VPC là công việc của thành viên khác và không phải nơi chạy Lambda API.

## 2. Kiến trúc xử lý yêu cầu

`Trình duyệt → API Gateway (HTTP API) → Lambda netmon-api → DynamoDB NetworkDevices`

Các thành phần đảm nhận nhiệm vụ:

- **API Gateway:** cung cấp các route HTTP cho phần mềm quản lý.
- **Lambda (`netmon-api`):** nhận sự kiện API, xác định phương thức, kiểm tra dữ liệu và xử lý CRUD.
- **DynamoDB (`NetworkDevices`):** lưu bản ghi thiết bị dưới khóa `deviceId`.
- **IAM role:** cấp cho Lambda quyền cần thiết để thao tác với bảng, không dùng tài khoản AWS cá nhân trong mã nguồn.

## 3. Thiết kế dữ liệu thiết bị

Một bản ghi mô phỏng có các trường:

| Trường | Mục đích |
|---|---|
| `deviceId` | Mã thiết bị, dùng làm khóa chính |
| `deviceName` | Tên hiển thị |
| `deviceType` | Router, Switch, Server hoặc loại khác |
| `ipAddress` | Địa chỉ IP của thiết bị |
| `location` | Vị trí đặt thiết bị |
| `status` | Trạng thái đang mô phỏng/theo dõi |
| `cpuUsage`, `memoryUsage` | Tỷ lệ sử dụng CPU và RAM mẫu |
| `lastUpdated` | Thời điểm cập nhật gần nhất |

Dữ liệu CPU/RAM của các thiết bị mô phỏng **không đồng nghĩa** với số liệu CloudWatch thu thập trực tiếp từ EC2. Đây là hai nguồn cần phân biệt khi viết báo cáo.

## 4. Các chức năng API

| Phương thức | Route ví dụ | Ý nghĩa |
|---|---|---|
| `GET` | `/devices` | Xem danh sách thiết bị |
| `GET` | `/devices/{id}` | Xem chi tiết một thiết bị |
| `POST` | `/devices` | Thêm thiết bị |
| `PUT` | `/devices/{id}` | Sửa thông tin |
| `DELETE` | `/devices/{id}` | Xóa thiết bị |

*Các route là cách tổ chức dự kiến; khi tích hợp cần đối chiếu route thực tế của API Gateway.*

Trong Lambda Python, thư viện `boto3` giúp làm việc với DynamoDB. Khi đọc danh sách bằng `scan()`, em lưu ý rằng một lần quét có thể chưa trả toàn bộ kết quả. Vì vậy phải kiểm tra `LastEvaluatedKey` để lấy tiếp các trang dữ liệu.

Ví dụ minh họa cách phân trang:

```python
import boto3

table = boto3.resource("dynamodb").Table("NetworkDevices")

def list_devices():
    items = []
    options = {}
    while True:
        response = table.scan(**options)
        items.extend(response.get("Items", []))
        if "LastEvaluatedKey" not in response:
            break
        options["ExclusiveStartKey"] = response["LastEvaluatedKey"]
    return items
```

Đây là mã minh họa nguyên tắc, không phải bản sao đầy đủ của Lambda đang triển khai.

## 5. Những vấn đề gặp khi kết nối giao diện

Lúc thử truy cập API từ trình duyệt, em phải kiểm tra **CORS**, URL của stage, phương thức HTTP và định dạng dữ liệu trả về. Với DynamoDB, số thập phân có thể được Python biểu diễn bằng `Decimal`, nên cần chuyển sang định dạng JSON phù hợp trước khi trả về.

Em dùng trang HTML chạy trên localhost để gọi API, thay vì phụ thuộc hoàn toàn vào Postman. Một lần thử thành công ở AWS Console chưa đủ để khẳng định frontend đã tích hợp xong; cần kiểm tra cả request từ trình duyệt, thông báo lỗi và quyền truy cập.

## 6. Kết quả và bài học

Qua phần việc của mình, em đã thực hành thiết kế bảng dữ liệu, xây dựng Lambda và HTTP API, kiểm tra các thao tác quản lý thiết bị. Em rút ra ba kinh nghiệm: cần thống nhất cấu trúc JSON giữa frontend/backend; quản lý quyền IAM theo mức cần thiết; và phân biệt việc API đã chạy với việc toàn bộ giao diện đã hoàn thiện.

**Hướng cải thiện:** kiểm tra dữ liệu đầu vào chặt hơn, bổ sung nhật ký thao tác, phân trang phù hợp với dữ liệu lớn, và kiểm thử đồng bộ các luồng CRUD.

## 7. Tài liệu tham khảo

- [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [DynamoDB: Scan và phân trang](https://docs.aws.amazon.com/boto3/latest/reference/services/dynamodb/table/scan.html)
- [DynamoDB với Python và Boto3](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/programming-with-python.html)

*Trạng thái bài viết: Bản thảo cá nhân, chưa xuất bản lên AWS Study Group.*
