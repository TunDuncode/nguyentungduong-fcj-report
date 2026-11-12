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

## Tạo JWT Authorizer

1. Vào **API Gateway → netmon-management-api → Authorization → Manage authorizers → Create**.

2. Loại **JWT**, tên `netmon-jwt-authorizer`, Identity source `$request.header.Authorization`.

3. Issuer là `https://cognito-idp.us-east-1.amazonaws.com/USER_POOL_ID` (thay `USER_POOL_ID` bằng giá trị thật). Audience là **App Client ID** của `netmon-web-client`.
4. Gắn authorizer vào tám routes. Đặt **Authorization scopes** như sau:

| Routes | Scope |
|---|---|
| Các route `GET` (`/devices`, `/devices/{id}`, `/alerts`, `/metrics`) | `netmon-api/read` |
| `POST /devices`, `PUT /devices/{id}`, `DELETE /devices/{id}`, `PUT /alerts/{id}` | `netmon-api/write` |

## Lưu ý

Frontend phải yêu cầu scopes này trong luồng đăng nhập và sử dụng **Access Token**, không dùng ID Token để gọi API. Chỉ thêm scope ở App Client không tự phân quyền vai trò cho từng tài khoản; phân quyền người dùng chi tiết cần thiết kế riêng.


---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

## Các ảnh minh chứng liên quan

{{< netmonimg src="images/netmon-workshop/39-api-gateway-jwt-authorizer-read-scope.png" alt="JWT Authorizer và scope netmon-api/read" caption="Ảnh 39 – JWT Authorizer và scope netmon-api/read" >}}

{{< netmonimg src="images/netmon-workshop/45-cognito-resource-server-netmon-api-scopes.png" alt="Resource Server netmon-api và hai scopes" caption="Ảnh 45 – Resource Server netmon-api và hai scopes" >}}

{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito Managed Login và cấu hình OAuth" caption="Ảnh 47 – Cognito Managed Login và cấu hình OAuth" >}}

[← Về chương](../)
