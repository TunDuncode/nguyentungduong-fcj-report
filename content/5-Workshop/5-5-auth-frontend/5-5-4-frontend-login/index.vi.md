---
title: "5.5.4. Đăng nhập bằng PKCE và gọi API bảo vệ"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.5.4. Đăng nhập bằng PKCE và gọi API bảo vệ

## Mục tiêu

Kết nối trang NetMon HTML/JavaScript với Cognito và lấy **Access Token** đúng chuẩn Authorization Code + PKCE.

## Chuẩn bị cấu hình

1. Trong **Cognito → App clients → `netmon-web-client`**, bảo đảm ứng dụng là SPA, dùng **Authorization code grant**.
2. Cấu hình callback chính xác `http://localhost:5500/`, các scope `openid email netmon-api/read netmon-api/write`; không dùng client secret trong trình duyệt.

{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito Managed Login và cấu hình OAuth" caption="Ảnh 47 – Cognito Managed Login và cấu hình OAuth" >}}

3. Khởi chạy web server trước khi đăng nhập, ví dụ `python -m http.server 5500`, rồi kiểm tra `http://localhost:5500/` đã tải được trang.

4. Từ giao diện NetMon API Test, bấm **Đăng nhập**: JavaScript tạo `code_verifier` và `code_challenge` (S256), chuyển đến Cognito Managed Login.

{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Giao diện đăng nhập Managed Login" caption="Ảnh 48 – Giao diện đăng nhập Managed Login" >}}

5. Sau khi xác thực, Cognito redirect về URL callback mang query `code=...`. Frontend đổi code lấy token tại OAuth `/oauth2/token` với đúng PKCE verifier.
6. Dùng `Authorization: Bearer <access_token>` khi gọi `GET /devices`; lấy `401`/`403` để phân biệt thiếu token/thiếu scope.

{{< netmonimg src="images/netmon-workshop/49-cognito-users-confirmed-enabled.png" alt="Hai tài khoản được xác minh trong Cognito" caption="Ảnh 49 – Hai tài khoản được xác minh trong Cognito" >}}

## Đăng nhập trên phiên bản NetMon Cloud V2.5

Nhập email của tài khoản Cognito đã được cấp, bấm **Next**.

{{< netmonimg src="images/netmon-workshop/56-cognito-sign-in-email.png" alt="Đăng nhập Cognito bằng email" caption="Ảnh 56 – Đăng nhập Cognito bằng email" >}}

Nhập mật khẩu, bấm **Continue**. Sau khi xác thực thành công, quay về ứng dụng và kiểm tra API hoạt động. Không công khai mật khẩu hoặc token.

{{< netmonimg src="images/netmon-workshop/57-cognito-sign-in-password.png" alt="Nhập mật khẩu tại Cognito" caption="Ảnh 57 – Nhập mật khẩu tại Cognito" >}}

## Khắc phục lỗi thường gặp

- **`ERR_CONNECTION_REFUSED`** tại `localhost:5500`: chưa chạy server hoặc sai port. URL chứa `code` không tự biến thành phiên đăng nhập khi không có frontend xử lý.
- **`invalid_grant`**: code đã hết hạn/đã dùng, redirect URI hoặc PKCE verifier không đúng; tạo lượt đăng nhập mới.
- **CORS**: kiểm tra API Gateway Allow-Origin `http://localhost:5500`, Allow-Headers `authorization`, `content-type`.
- Không đăng token, code hay verifier thật lên GitHub.

**Trạng thái:** Nhóm đã thử đổi mật khẩu và nhận redirect về localhost; phần xử lý PKCE và đọc dữ liệu thật qua web cần được xác minh riêng.

## Sau khi đăng nhập

Frontend dùng Access Token gửi trong header Authorization; kiểm tra danh sách thiết bị và chỉ số thay vì chỉ thấy trang Dashboard. Khi token hết hạn, đăng nhập lại hoặc dùng cơ chế làm mới hợp lệ nếu ứng dụng hỗ trợ. Khi đăng xuất, xóa trạng thái xác thực của ứng dụng và kết thúc phiên Cognito theo URL đã cấu hình. Không dùng ID token thay cho Access Token có custom scopes.

Chế độ demo và kiểm thử backend đã có kết quả; việc trao đổi PKCE và toàn bộ API qua trình duyệt AWS vẫn cần kiểm thử riêng với phiên bản giao diện đang dùng.


[← Về chương](../)
