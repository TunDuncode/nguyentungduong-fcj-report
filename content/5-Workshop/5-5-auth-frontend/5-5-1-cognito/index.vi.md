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

{{< netmonimg src="images/netmon-workshop/43-cognito-user-pool-overview.png" alt="Tổng quan Cognito User Pool" caption="Ảnh 43 – Tổng quan Cognito User Pool" >}}

2. Tạo **App client** cho loại **Single-page application (SPA)**, đặt tên `netmon-web-client`.

{{< netmonimg src="images/netmon-workshop/44-cognito-app-client-netmon-web-client.png" alt="Cognito App Client netmon-web-client" caption="Ảnh 44 – Cognito App Client netmon-web-client" >}}

3. Chọn đăng nhập bằng **email**, không mở self-registration nếu đây là hệ thống chỉ dành cho thành viên được cấp quyền.

4. Đặt **Allowed callback URLs** thành `http://localhost:5500/`. Nếu giao diện chạy ở port khác, phải cập nhật callback và origin tương ứng.

5. Chọn **Authorization code grant** và cấu hình Cognito domain cho Managed Login. Với SPA, sử dụng **Authorization Code + PKCE**, không nhúng client secret vào JavaScript.

{{< netmonimg src="images/netmon-workshop/45-cognito-resource-server-netmon-api-scopes.png" alt="Resource Server netmon-api và hai scopes" caption="Ảnh 45 – Resource Server netmon-api và hai scopes" >}}


{{< netmonimg src="images/netmon-workshop/46-cognito-domain-managed-login-issuer.png" alt="Cognito Domain và Issuer" caption="Ảnh 46 – Cognito Domain và Issuer" >}}


{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito Managed Login và cấu hình OAuth" caption="Ảnh 47 – Cognito Managed Login và cấu hình OAuth" >}}


{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Giao diện đăng nhập Managed Login" caption="Ảnh 48 – Giao diện đăng nhập Managed Login" >}}

6. Vào **User management → Users → Create user**, tạo tài khoản email được nhóm cho phép sử dụng. Khi đăng nhập lần đầu bằng mật khẩu tạm thời, người dùng cần đổi mật khẩu.

{{< netmonimg src="images/netmon-workshop/49-cognito-users-confirmed-enabled.png" alt="Hai tài khoản được xác minh trong Cognito" caption="Ảnh 49 – Hai tài khoản được xác minh trong Cognito" >}}


## Kiểm tra

Sau khi đăng nhập thành công, Cognito sẽ chuyển hướng về callback URL với `?code=...`. Trang frontend phải đang chạy tại `localhost:5500` và xử lý PKCE để đổi code lấy token. Nếu hiện `ERR_CONNECTION_REFUSED`, thường là chưa có server local đang lắng nghe ở cổng này, không phải Lambda hỏng.

> Mã `code` và token là dữ liệu nhạy cảm tạm thời; không đưa vào ảnh chụp báo cáo.

---

> **Lưu ý khi xuất bản:** Không đăng ảnh nguyên gốc có email, mã đăng nhập hoặc token. Hình trong bộ này được lấy từ các ảnh quá trình thực hành và cắt bỏ thanh tài khoản; hãy tự kiểm tra lại trước khi đưa lên website công khai.

[← Về chương](../)
