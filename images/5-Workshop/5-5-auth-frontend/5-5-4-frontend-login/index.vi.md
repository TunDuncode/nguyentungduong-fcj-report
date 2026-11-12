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
3. Khởi chạy web server trước khi đăng nhập, ví dụ `python -m http.server 5500`, rồi kiểm tra `http://localhost:5500/` đã tải được trang.

![Cognito xác nhận User Pool và App Client được tạo]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Hình minh chứng: Cognito xác nhận User Pool và App Client được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Từ giao diện NetMon API Test, bấm **Đăng nhập**: JavaScript tạo `code_verifier` và `code_challenge` (S256), chuyển đến Cognito Managed Login.

![Minh chứng lỗi localhost khi chưa chạy web server]({{< relURL "images/netmon-workshop/frontend-localhost.webp" >}})

*Hình minh chứng: Minh chứng lỗi localhost khi chưa chạy web server. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. Sau khi xác thực, Cognito redirect về URL callback mang query `code=...`. Frontend đổi code lấy token tại OAuth `/oauth2/token` với đúng PKCE verifier.
6. Dùng `Authorization: Bearer <access_token>` khi gọi `GET /devices`; lấy `401`/`403` để phân biệt thiếu token/thiếu scope.

## Khắc phục lỗi thường gặp

- **`ERR_CONNECTION_REFUSED`** tại `localhost:5500`: chưa chạy server hoặc sai port. URL chứa `code` không tự biến thành phiên đăng nhập khi không có frontend xử lý.
- **`invalid_grant`**: code đã hết hạn/đã dùng, redirect URI hoặc PKCE verifier không đúng; tạo lượt đăng nhập mới.
- **CORS**: kiểm tra API Gateway Allow-Origin `http://localhost:5500`, Allow-Headers `authorization`, `content-type`.
- Không đăng token, code hay verifier thật lên GitHub.

**Trạng thái:** Nhóm đã thử đổi mật khẩu và nhận redirect về localhost; phần xử lý PKCE và đọc dữ liệu thật qua web cần được xác minh riêng.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
