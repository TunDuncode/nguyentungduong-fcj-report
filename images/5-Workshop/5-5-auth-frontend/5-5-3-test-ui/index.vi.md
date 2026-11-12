---
title: "5.5.3. Xây dựng trang kiểm thử trên VS Code"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.5.3. Xây dựng trang kiểm thử trên VS Code

## Mục tiêu

Dùng trang kiểm thử HTML/CSS/JavaScript chạy trên VS Code để đăng nhập Cognito, gọi API và kiểm tra dữ liệu thật; không cần chờ giao diện cuối cùng của Mạnh Quân.

## Chuẩn bị

1. Mở dự án `NetMon-API-Test` đã chuẩn bị trong VS Code, hoặc sử dụng một frontend có triển khai PKCE tương đương.
2. Tại thư mục chứa `index.html`, chạy server cục bộ:

```bash
python -m http.server 5500
```

3. Mở `http://localhost:5500/` và xác nhận giao diện tải được **trước khi** bấm đăng nhập Cognito.

![Minh chứng lỗi localhost khi chưa chạy web server]({{< relURL "images/netmon-workshop/frontend-localhost.webp" >}})

*Hình minh chứng: Minh chứng lỗi localhost khi chưa chạy web server. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Nhập đúng **Cognito domain**, **App Client ID**, **API Gateway Invoke URL**. Đừng điền AWS Secret Key hoặc Cognito client secret vào trang web.
5. Bấm nút đăng nhập do frontend cung cấp. Sau khi Cognito redirect về `/?code=...`, JavaScript xử lý PKCE và nhận Access Token.
6. Gọi thử `GET /devices` và `GET /alerts`. Nếu thành công, tiếp tục tạo thiết bị `TEST-SW01`, sửa thông tin, xem chi tiết rồi xóa đúng thiết bị này.

## Các lỗi và cách đọc kết quả

| Hiện tượng | Gợi ý kiểm tra |
|---|---|
| `ERR_CONNECTION_REFUSED` | Server localhost:5500 chưa chạy |
| `401 Unauthorized` | Thiếu, sai hoặc hết hạn token |
| `403 Forbidden` | Access Token thiếu scope của route |
| CORS blocked | Origin hoặc headers trong API Gateway CORS chưa đúng |
| `500` | Lambda, DynamoDB, IAM hoặc CloudWatch Logs |

> Không gửi ảnh chụp URL có `?code=` còn hiệu lực hoặc token thật. Trước khi ghép sang giao diện chính, kiểm tra lại 8 Routes có trả đúng dữ liệu như Lambda đã xử lý hay không.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
