---
title : "Triển khai Frontend với AWS Amplify"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.6. </b> "
---

#### Mục tiêu

Triển khai frontend tĩnh của GameHub bằng AWS Amplify và cấu hình build phù hợp.

#### Bước 1: Khởi tạo app Amplify

1. Vào Amplify Console.
2. Nhấn `Deploy an app`.
3. Chọn `GitHub` làm source provider.
4. Xác thực GitHub và chọn repository.

#### Bước 2: Chọn branch và thư mục

1. Chọn nhánh deploy, ví dụ `V1`.
2. Nếu repo là monorepo, bật `My app is a monorepo`.
3. Nhập `frontend` vào `Monorepo root directory`.

#### Bước 3: Cấu hình build

Sử dụng cấu hình sau để build Flutter web trên Amplify:
```yaml
version: 1
applications:
  - frontend:
      phases:
        build:
          commands:
            - ORIGINAL_DIR=$(pwd)
            - which xz || sudo yum install -y xz
            - cd /tmp
            - wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.22.0-stable.tar.xz
            - tar xf flutter_linux_3.22.0-stable.tar.xz
            - export PATH="$PATH:/tmp/flutter/bin"
            - cd $ORIGINAL_DIR
            - flutter doctor
            - flutter config --enable-web
            - flutter channel stable
            - flutter upgrade
            - flutter pub get
            - flutter build web --release --dart-define=COGNITO_REGION=$COGNITO_REGION --dart-define=COGNITO_USER_POOL_ID=$COGNITO_USER_POOL_ID --dart-define=COGNITO_CLIENT_ID=$COGNITO_CLIENT_ID --dart-define=API_GATEWAY_WS_URL=$API_GATEWAY_WS_URL --dart-define=API_GATEWAY_HTTP_URL=$API_GATEWAY_HTTP_URL
      artifacts:
        baseDirectory: build/web
        files:
          - "**/*"
      cache:
        paths: []
    appRoot: frontend
```

#### Bước 4: Biến môi trường

Thêm biến sau trong Amplify Console:
- `COGNITO_REGION`
- `COGNITO_USER_POOL_ID`
- `COGNITO_CLIENT_ID`
- `API_GATEWAY_HTTP_URL`
- `API_GATEWAY_WS_URL`
- `LOCAL_API_URL`
- `USE_LOCAL_BACKEND`
- `APK_DOWNLOAD_URL`

#### Bước 5: Review và deploy

1. Kiểm tra cấu hình ứng dụng.
2. Nhấn `Save and deploy`.
3. Amplify sẽ tự động build và deploy frontend.

#### Kết quả

- Frontend được host dưới URL Amplify.
- Mỗi lần push lên branch deploy sẽ kích hoạt build tự động.

Note (hình ảnh): Thêm ảnh `amplify-setup.png` vào `images/5-Workshop/5.6-Cleanup/amplify-setup.svg`.
