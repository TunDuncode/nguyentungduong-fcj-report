---
title: "5.5.1. Tạo Cognito User Pool và Web Client"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.5.1. Tạo Cognito User Pool và Web Client

## Mục tiêu

Tạo cơ chế đăng nhập cho người quản lý NetMon bằng Amazon Cognito, thay vì để giao diện truy cập API không kiểm soát.

## Các bước

1. Mở **Amazon Cognito → User pools**. Tạo User Pool hoặc chọn pool đã tạo ở Region `us-east-1`.
2. Tạo **App client** cho loại **Single-page application (SPA)**, đặt tên `netmon-web-client`.
3. Chọn đăng nhập bằng **email**, không mở self-registration nếu đây là hệ thống chỉ dành cho thành viên được cấp quyền.

![Tạo Cognito cho ứng dụng SPA]({{< relURL "images/netmon-workshop/cognito-create.webp" >}})

*Hình minh chứng: Tạo Cognito cho ứng dụng SPA. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

4. Đặt **Allowed callback URLs** thành `http://localhost:5500/`. Nếu giao diện chạy ở port khác, phải cập nhật callback và origin tương ứng.

![Cognito xác nhận User Pool và App Client được tạo]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Hình minh chứng: Cognito xác nhận User Pool và App Client được tạo. Ảnh từ quá trình thực hành NetMon, đã cắt bỏ phần nhận diện tài khoản trên thanh AWS Console.*

5. Chọn **Authorization code grant** và cấu hình Cognito domain cho Managed Login. Với SPA, sử dụng **Authorization Code + PKCE**, không nhúng client secret vào JavaScript.
6. Vào **User management → Users → Create user**, tạo tài khoản email được nhóm cho phép sử dụng. Khi đăng nhập lần đầu bằng mật khẩu tạm thời, người dùng cần đổi mật khẩu.

## Kiểm tra

Sau khi đăng nhập thành công, Cognito sẽ chuyển hướng về callback URL với `?code=...`. Trang frontend phải đang chạy tại `localhost:5500` và xử lý PKCE để đổi code lấy token. Nếu hiện `ERR_CONNECTION_REFUSED`, thường là chưa có server local đang lắng nghe ở cổng này, không phải Lambda hỏng.

> Mã `code` và token là dữ liệu nhạy cảm tạm thời; không đưa vào ảnh chụp báo cáo.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
