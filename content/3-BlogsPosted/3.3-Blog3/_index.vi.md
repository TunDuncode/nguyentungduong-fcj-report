---
title: "3.3. Đăng nhập Amazon Cognito và bảo vệ API bằng JWT"
date: 2026-11-12T00:00:00+07:00
weight: 3
chapter: false
draft: false
---

## 1. Vì sao NetMon cần đăng nhập?

Trong ứng dụng quản lý thiết bị mạng, các thao tác như thêm hoặc xóa thiết bị không nên cho phép thực hiện tự do. Vì vậy, khi ghép giao diện với API, nhóm tìm hiểu cách sử dụng **Amazon Cognito** để quản lý người dùng và **JWT Authorizer của API Gateway** để kiểm tra yêu cầu gọi API.

Đây là bước tiếp theo sau khi phần Lambda và DynamoDB đã có thể xử lý dữ liệu. Em muốn người dùng đăng nhập trước, sau đó mới xem danh sách thiết bị và các cảnh báo của hệ thống.

## 2. Vai trò các dịch vụ

`Người dùng → Cognito User Pool (đăng nhập) → nhận token → giao diện → API Gateway JWT Authorizer → Lambda → DynamoDB`

- **Cognito User Pool:** quản lý tài khoản và quy trình xác thực người dùng.
- **Cognito App Client:** đại diện cho ứng dụng kết nối tới User Pool.
- **Cognito managed login/Hosted UI:** giao diện đăng nhập do Cognito cung cấp.
- **API Gateway JWT Authorizer:** xác minh chữ ký, issuer, audience/client ID, thời hạn token và scope nếu route yêu cầu.
- **Lambda:** chỉ nhận yêu cầu đã qua lớp xác thực của route được bảo vệ, rồi thực hiện logic nghiệp vụ.

Cần lưu ý: **đăng nhập thành công không có nghĩa toàn bộ API đã được phân quyền đúng**. Mỗi route vẫn cần cấu hình authorization phù hợp.

## 3. Quy trình tích hợp trên giao diện

Các bước em tìm hiểu và thực hành gồm:

1. Tạo **User Pool** trong Amazon Cognito.
2. Tạo **App Client** phù hợp với ứng dụng trình duyệt.
3. Cấu hình domain đăng nhập và địa chỉ callback.
4. Tạo tài khoản thử nghiệm và kiểm tra quy trình đăng nhập, đổi mật khẩu ban đầu nếu được yêu cầu.
5. Cấu hình **JWT Authorizer** cho các route cần bảo vệ ở HTTP API Gateway.
6. Sau khi đăng nhập, gửi token hợp lệ trong header `Authorization: Bearer ...` khi gọi API.
7. Kiểm tra phản hồi khi thiếu token, token hết hạn hoặc route chưa được phép truy cập.

Ví dụ request minh họa:

```http
GET /devices HTTP/1.1
Host: example.execute-api.us-east-1.amazonaws.com
Authorization: Bearer <valid-access-token>
```

Không chép token thật, mật khẩu, Client Secret hoặc mã định danh tài khoản riêng vào bài công khai. Với ứng dụng chạy trực tiếp trong trình duyệt, nên dùng App Client phù hợp với **public client** và quy trình đăng nhập an toàn.

## 4. Khó khăn khi kiểm thử

Một số lỗi thường làm người mới học AWS nhầm lẫn là:

- **Sai Callback URL:** đăng nhập xong không quay về đúng trang ứng dụng.
- **Sai issuer hoặc audience:** API Gateway từ chối token dù trang Cognito vẫn đăng nhập được.
- **CORS:** trình duyệt chặn request dù backend và quyền xác thực về cơ bản có thể đã đúng.
- **Token hết hạn:** cần xử lý phiên đăng nhập và đăng xuất hợp lý.
- **Quyền theo route:** `GET` có thể được phép nhưng `DELETE` cần kiểm soát chặt hơn.

Khi thử hệ thống, em tách việc kiểm tra thành ba mức: **đăng nhập Cognito**, **gọi API có token**, và **thao tác trên giao diện**. Cách này giúp biết lỗi nằm ở đâu thay vì sửa nhiều dịch vụ cùng lúc.

## 5. Những gì em rút ra

Phần Cognito giúp em hiểu thêm về ranh giới giữa **xác thực (authentication)** và **phân quyền (authorization)**. Việc có trang đăng nhập đẹp chưa đủ; API phải kiểm tra token, quy tắc truy cập và cả dữ liệu đầu vào ở phía backend.

**Hướng hoàn thiện:** thống nhất cơ chế chuyển trang sau đăng nhập, kiểm thử phiên đăng nhập hết hạn, bảo vệ các thao tác CRUD nhạy cảm và chuẩn hóa thông báo khi người dùng không có quyền.

## 6. Tài liệu tham khảo

- [Amazon Cognito User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools.html)
- [JWT Authorizer cho API Gateway HTTP API](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html)

*Trạng thái bài viết: Bản thảo cá nhân, chưa xuất bản lên AWS Study Group.*
