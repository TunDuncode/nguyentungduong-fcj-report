---
title : "Khởi tạo Pipeline SAM"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Bước 1: Khởi tạo Pipeline

1. Mở Terminal tại thư mục gốc dự án.
2. Chạy lệnh:
```
sam pipeline init --bootstrap
```

3. Trả lời các câu hỏi sau:
- `Select a pipeline template`: `1` (AWS Quick Start Pipeline Templates)
- `Select CI/CD system`: `5` (AWS CodePipeline)
- `Which pipeline template would you like to use?`: `2` (Two-stage pipeline)
- `Do you want to go through stage setup process now?`: `y`

#### Bước 2: Thiết lập dev stage

Khi được hỏi thông tin cho stage Dev:
- `Stage configuration name`: `dev`
- `Select a credential source`: `2` (default named profile)
- `Enter the region`: `ap-southeast-1` hoặc region của bạn
- Nếu yêu cầu profile, nhập `gamehub`
- Khi hỏi ARN/roles/artifact buckets, nhấn `Enter` để SAM tạo tự động
- `Does your application contain any IMAGE type Lambda functions?`: `n`

#### Bước 3: Thiết lập prod stage

1. Chọn cấu hình cho stage Prod.
2. `Stage configuration name`: `prod`.
3. `Select a credential source`: `2` hoặc `1`.
4. `Enter the region`: cùng region hoặc region khác tùy chiến lược vận hành.

#### Bước 4: Kiểm tra file pipeline

Chạy:
```
ls pipeline
```
Các file cần có:
- `pipeline/samconfig.toml`
- `pipeline/codepipeline.yaml`
- `buildspec_deploy.yml`

#### Ghi chú

- `sam pipeline init --bootstrap` tạo các tài nguyên bootstrap như S3 artifact bucket.
- `samconfig.toml` chứa cấu hình stage và profile.
- Bạn có thể chỉnh sửa `samconfig.toml` sau khi init để tùy chỉnh stage.

#### Commit và push

```bash
git add pipeline/*
git commit -m "chore(ci): add sam pipeline config for GameHub"
git push origin main
```

Note (hình ảnh): Thêm ảnh `sam pipeline init` và `ls pipeline/` trong `images/5-Workshop/5.3-S3-vpc/sam-init.svg`.
