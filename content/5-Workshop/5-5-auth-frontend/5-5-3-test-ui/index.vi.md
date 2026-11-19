---
title: "5.5.3. Xây dựng trang kiểm thử trên VS Code"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.5.3. Xây dựng trang kiểm thử trên VS Code

## Mục tiêu

Dùng trang kiểm thử HTML/CSS/JavaScript chạy trên VS Code để đăng nhập Cognito, gọi API và kiểm tra dữ liệu thật; để kiểm tra kết nối trước khi sử dụng giao diện chính.

## Chuẩn bị

1. Mở dự án `NetMon-API-Test` đã chuẩn bị trong VS Code, hoặc sử dụng một frontend có triển khai PKCE tương đương.
2. Tại thư mục chứa `index.html`, chạy server cục bộ:

```bash
python -m http.server 5500
```

3. Mở `http://localhost:5500/` và xác nhận giao diện tải được **trước khi** bấm đăng nhập Cognito.

{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Giao diện đăng nhập Managed Login" caption="Ảnh 48 – Giao diện đăng nhập Managed Login" >}}

4. Nhập đúng **Cognito domain**, **App Client ID**, **API Gateway Invoke URL**. Đừng điền AWS Secret Key hoặc Cognito client secret vào trang web.
5. Bấm nút đăng nhập do frontend cung cấp. Sau khi Cognito redirect về `/?code=...`, JavaScript xử lý PKCE và nhận Access Token.
6. Gọi thử `GET /devices` và `GET /alerts`. Nếu thành công, tiếp tục tạo thiết bị `TEST-SW01`, sửa thông tin, xem chi tiết rồi xóa đúng thiết bị này.

{{< netmonimg src="images/netmon-workshop/41-api-gateway-cors-localhost-5500.png" alt="Cấu hình CORS localhost:5500" caption="Ảnh 41 – Cấu hình CORS localhost:5500" >}}

## Các lỗi và cách đọc kết quả

| Hiện tượng | Gợi ý kiểm tra |
|---|---|
| `ERR_CONNECTION_REFUSED` | Server localhost:5500 chưa chạy |
| `401 Unauthorized` | Thiếu, sai hoặc hết hạn token |
| `403 Forbidden` | Access Token thiếu scope của route |
| CORS blocked | Origin hoặc headers trong API Gateway CORS chưa đúng |
| `500` | Lambda, DynamoDB, IAM hoặc CloudWatch Logs |

> Không gửi ảnh chụp URL có `?code=` còn hiệu lực hoặc token thật. Trước khi ghép sang giao diện chính, kiểm tra lại 8 Routes có trả đúng dữ liệu như Lambda đã xử lý hay không.

## Chạy ứng dụng NetMon trên VS Code

Mở thư mục chứa `index.html` của ứng dụng NetMon, dùng Live Server (hoặc lệnh server ở trên) và chọn đúng `http://localhost:5500/`. Không mở trực tiếp file HTML qua `file://`. Nếu Live Server chạy từ thư mục cha, URL có thể chứa thêm tên thư mục và không khớp callback đã đăng ký.

Trong ứng dụng, chế độ demo giúp trình diễn không cần AWS; chế độ kết nối AWS cần URL API, Cognito và token hợp lệ. Kiểm tra qua tab Network để xác định đang dùng nguồn nào. Website Hugo của báo cáo chỉ chứa tài liệu workshop; nó không tự hosting hoặc khởi chạy giao diện NetMon.


[← Về chương](../)
