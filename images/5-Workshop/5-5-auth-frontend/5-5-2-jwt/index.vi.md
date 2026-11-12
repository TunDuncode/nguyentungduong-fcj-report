---
title: "5.5.2. Tạo JWT Authorizer và OAuth Scopes"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.5.2. Tạo JWT Authorizer và OAuth Scopes

## Mục tiêu

Yêu cầu Access Token hợp lệ và scope tương ứng trước khi API Gateway cho phép truy cập các chức năng đọc/ghi của NetMon.

## Tạo Resource Server và OAuth scopes

1. Mở **Cognito → User pool → Applications → Resource servers → Create resource server**.
2. Đặt tên `NetMon API`, Identifier `netmon-api`; thêm custom scopes `read` và `write`.
3. Mở **App clients → netmon-web-client → Login pages → Edit**, cho phép `netmon-api/read`, `netmon-api/write` và các OpenID scopes cần thiết (ví dụ `openid`, `email`). Lưu thay đổi.

![Đã chọn hai OAuth scopes cho App Client]({{< relURL "images/netmon-workshop/cognito-scope.webp" >}})

*Hình minh chứng: Đã chọn hai OAuth scopes cho App Client. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*


## Tạo JWT Authorizer

1. Vào **API Gateway → netmon-management-api → Authorization → Manage authorizers → Create**.

![Gắn JWT Authorizer vào các Routes]({{< relURL "images/netmon-workshop/cognito-jwt.webp" >}})

*Hình minh chứng: Gắn JWT Authorizer vào các Routes. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

2. Loại **JWT**, tên `netmon-jwt-authorizer`, Identity source `$request.header.Authorization`.

![Thiết lập quyền cho từng Route]({{< relURL "images/netmon-workshop/cognito-authorization.webp" >}})

*Hình minh chứng: Thiết lập quyền cho từng Route. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

3. Issuer là `https://cognito-idp.us-east-1.amazonaws.com/USER_POOL_ID` (thay `USER_POOL_ID` bằng giá trị thật). Audience là **App Client ID** của `netmon-web-client`.
4. Gắn authorizer vào tám routes. Đặt **Authorization scopes** như sau:

| Routes | Scope |
|---|---|
| Các route `GET` (`/devices`, `/devices/{id}`, `/alerts`, `/metrics`) | `netmon-api/read` |
| `POST /devices`, `PUT /devices/{id}`, `DELETE /devices/{id}`, `PUT /alerts/{id}` | `netmon-api/write` |

## Lưu ý

Frontend phải yêu cầu scopes này trong luồng đăng nhập và sử dụng **Access Token**, không dùng ID Token để gọi API. Chỉ thêm scope ở App Client không tự phân quyền vai trò cho từng tài khoản; phân quyền người dùng chi tiết cần thiết kế riêng.

![Sơ đồ nguyên lý NetMon]({{< relURL "images/netmon-workshop/netmon-scope-flow.png" >}})

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
