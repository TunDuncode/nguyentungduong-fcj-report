---
title: "5.4.2. Viết Lambda netmon-api bằng Python"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.4.2. Viết Lambda netmon-api bằng Python

## Mục tiêu

Dùng một Lambda Python `netmon-api` để xử lý 8 chức năng HTTP theo phương thức và đường dẫn request, giảm nhu cầu tạo nhiều Lambda nhỏ cho đồ án.

## Các bước

1. Vào **Lambda → Functions → Create function → Author from scratch**; đặt tên `netmon-api`, Runtime Python được AWS hỗ trợ.

{{< netmonimg src="images/netmon-workshop/34-lambda-netmon-api-code-and-api-gateway.png" alt="Hàm netmon-api và kết nối API Gateway" caption="Ảnh 34 – Hàm netmon-api và kết nối API Gateway" >}}

2. Gắn **execution role** cho phép thao tác với hai bảng DynamoDB và `cloudwatch:GetMetricStatistics`, cùng CloudWatch Logs. Nên chỉ định ARN tài nguyên cụ thể cho quyền DynamoDB.

{{< netmonimg src="images/netmon-workshop/53-lambda-netmon-api-execution-role-permissions.png" alt="Execution role của Lambda netmon-api" caption="Ảnh 53 – Execution role của Lambda netmon-api" >}}

{{< netmonimg src="images/netmon-workshop/54-iam-netmon-api-role-permission-policies.png" alt="Danh sách IAM policies của role" caption="Ảnh 54 – Danh sách IAM policies của role" >}}

{{< netmonimg src="images/netmon-workshop/55-iam-netmon-api-access-policy-json.png" alt="JSON chính sách quyền DynamoDB và CloudWatch" caption="Ảnh 55 – JSON chính sách quyền DynamoDB và CloudWatch" >}}

3. Trong mã nguồn, đọc phương thức từ `event.requestContext.http.method` và đường dẫn `event.rawPath` của **HTTP API payload format 2.0**.

4. Sử dụng `boto3.resource('dynamodb')`, kiểm tra dữ liệu đầu vào và trả JSON `statusCode`, `headers`, `body`.
5. Bấm **Deploy** mã nguồn. Vào tab **Test**, tạo sự kiện GET `/devices` theo mẫu:

{{< netmonimg src="images/netmon-workshop/35-lambda-netmon-api-test-succeeded-details-collapsed.png" alt="Kết quả chạy Lambda (chưa mở Details)" caption="Ảnh 35 – Kết quả chạy Lambda (chưa mở Details)" >}}

```json
{
  "version": "2.0",
  "rawPath": "/devices",
  "requestContext": {"http": {"method": "GET", "path": "/devices"}}
}
```

6. Bấm **Test**; kiểm tra `statusCode` và dữ liệu trả về. Các chức năng POST, PUT, DELETE phải được kiểm thử riêng, ưu tiên thiết bị có `deviceId` bắt đầu bằng `TEST-`.

{{< netmonimg src="images/netmon-workshop/36-cloudwatch-logs-netmon-api-6-streams.png" alt="CloudWatch log streams của netmon-api" caption="Ảnh 36 – CloudWatch log streams của netmon-api" >}}

{{< netmonimg src="images/netmon-workshop/37-lambda-netmon-api-get-devices-test-200.png" alt="GET /devices trả về HTTP 200 và dữ liệu thiết bị" caption="Ảnh 37 – GET /devices trả về HTTP 200 và dữ liệu thiết bị" >}}

## Lưu ý kết quả thực tế

Trong quá trình thực hiện, nhóm đã nhận được phản hồi `statusCode: 200` từ một sự kiện test Lambda. Điều này xác nhận hàm xử lý được sự kiện thử, **chưa chứng minh toàn bộ 8 API Routes đã được kiểm thử từ trình duyệt**.

## Lỗi thường gặp

- `AccessDeniedException`: role chưa đủ quyền DynamoDB.
- `KeyError` hoặc `None`: payload từ API Gateway khác test event; kiểm tra `rawPath`, `pathParameters`, `requestContext`.
- `Internal server error`: mở **Monitor → View CloudWatch logs** và đọc stack trace.

## Cách backend NetMon xử lý dữ liệu

- `GET /devices`: đọc danh sách DynamoDB; xử lý `LastEvaluatedKey` nếu Scan có nhiều trang.
- `POST /devices`: kiểm tra mã/tên, lưu vị trí và nguồn dữ liệu; với thiết bị mô phỏng có thể sinh CPU/RAM nếu chưa nhập. Không ghi đè thiết bị trùng ID ngoài ý muốn.
- `PUT /devices/{id}`: cập nhật các trường cho phép và thời gian; không dùng dữ liệu mô phỏng ghi đè metric EC2. `DELETE` chỉ xóa mục đúng ID, `GET` chi tiết đối chiếu khóa.
- `GET /metrics`: tổng hợp CPU/RAM mô phỏng hoặc số liệu CloudWatch theo `instanceId` và trả rõ nguồn; NetworkIn/NetworkOut có thể `null` đối với thiết bị mô phỏng.
- `GET /alerts`, `PUT /alerts/{id}`: đọc và xử lý cảnh báo; kiểm tra giá trị `handlingStatus` được backend hỗ trợ.

Trong bản backend tích hợp, header `X-Netmon-Build: netmon-integrated-v2` giúp đối chiếu bản Lambda đang chạy nếu header này vẫn được giữ. Không thay toàn bộ Lambda đang hoạt động chỉ để thêm dữ liệu; kiểm thử hàm mới hoặc thay đổi từng phần và giữ nguyên JWT/CORS.

Ví dụ test riêng cho chỉ số:

```json
{
  "version": "2.0",
  "rawPath": "/metrics",
  "requestContext": {"http": {"method": "GET", "path": "/metrics"}}
}
```

Xác nhận HTTP 200, trường nguồn và số liệu EC2; test event Console không đi qua JWT Authorizer nên vẫn cần kiểm tra với trình duyệt.


[← Về chương](../)
