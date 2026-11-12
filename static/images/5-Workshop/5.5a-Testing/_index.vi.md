---
title : "Kiểm thử và Pipeline Testing"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.5a. </b> "
---

#### Mục tiêu

Thêm bước kiểm thử tự động vào pipeline để phát hiện lỗi trước khi deploy ứng dụng.

#### Nội dung chi tiết

- Tạo stage `Test` trong pipeline.
- Dùng CodeBuild để chạy unit test và integration test.
- Dừng pipeline nếu kiểm thử thất bại.
- Báo cáo kết quả kiểm thử rõ ràng.

#### Cấu hình buildspec

Sử dụng `buildspec_deploy.yml` để chạy test:
```yaml
version: 0.2
phases:
  install:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - pytest tests/
artifacts:
  files:
    - '**/*'
```

#### Với Node.js

Nếu bạn dùng Node.js hoặc frontend test:
```yaml
phases:
  install:
    commands:
      - npm ci
  build:
    commands:
      - npm test
```

#### Lời khuyên

- Phân chia test thành unit và integration.
- Chạy test quan trọng ở stage đầu để tiết kiệm thời gian.
- Xem CodeBuild logs để tìm nguyên nhân lỗi.
- Dùng kết quả kiểm thử làm gate trước deploy.

#### Kết quả

- Test pass: pipeline tiếp tục tới deploy.
- Test fail: pipeline dừng và báo lỗi.

Note (hình ảnh): Thêm ảnh `test-run.png` vào `images/5-Workshop/5.5a-Testing/`.
