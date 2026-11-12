---
title : "Cấu hình Repository và Stage"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

#### Mục tiêu

Phần này giúp bạn cấu hình chính xác repository và stage để pipeline SAM hoạt động ổn định.

#### Những thông tin quan trọng

- `Repository subfolder`: thư mục chứa backend, ví dụ `backend`.
- `Template path`: đường dẫn tới file SAM/CloudFormation, ví dụ `backend/template.yaml`.
- `SSM Prefix`: ví dụ `gamehub/`.
- `Stack name` Dev/Prod: `GameHub-dev`, `GameHub-prod`.
- `Git branch`: `main`, `V1`, hoặc nhánh deploy.

#### Chi tiết cấu hình

1. Khi SAM hỏi `Repository root path`, nhập `backend` nếu backend ở đó.
2. Nếu repository là monorepo, đảm bảo chỉ trỏ pipeline tới thư mục backend.
3. Kiểm tra `template path` trỏ đúng file SAM template.

#### Quản lý stage

- Dev stage để thử nghiệm nhanh và deploy tự động.
- Prod stage để deploy khi đã kiểm thử ổn định.
- Giữ tên stage và stack nhất quán cho dễ theo dõi.

#### Kiểm tra lại

- Mở `pipeline/samconfig.toml` và kiểm tra `stage`/`region`.
- Mở `pipeline/codepipeline.yaml` để xác nhận template path.
- Nếu cần, điều chỉnh `samconfig.toml` rồi chạy lại pipeline.

#### Gợi ý commit

```bash
git add .
git commit -m "ci: add sam pipeline configuration for GameHub"
git push origin main
```

Note (hình ảnh): Thêm ảnh `pipeline file list` và `samconfig preview` vào `images/5-Workshop/5.4-S3-onprem/pipeline-files.svg`.
