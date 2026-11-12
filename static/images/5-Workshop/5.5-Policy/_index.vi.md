---
title : "Tạo CodePipeline trên AWS Console"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Mục tiêu

Thiết lập CodePipeline trên AWS Console để kết nối GitHub, build và deploy ứng dụng GameHub.

#### Tạo kết nối GitHub

1. Mở AWS Console → `Developer Tools` → `Connections`.
2. Nhấn `Create connection`.
3. Chọn `GitHub` và cấp quyền truy cập.
4. Chọn repository của GameHub.
5. Đảm bảo trạng thái kết nối là `Available`.

#### Tạo pipeline trên Console

1. Mở CodePipeline Console.
2. Chọn `Create pipeline`.
3. Chọn `Use a blueprint` hoặc `Start from scratch`.
4. Source provider: `GitHub (version 2)`.
5. Chọn connection, repository và branch.
6. Thêm stage Build với CodeBuild dùng `buildspec_deploy.yml`.
7. Thêm stage Deploy với CloudFormation trỏ tới `pipeline/codepipeline.yaml`.

#### Lưu ý khi dùng SAM

- Nếu bạn đã chạy `sam pipeline init`, tái sử dụng `codepipeline.yaml` do SAM tạo.
- Lưu ARN connection để sử dụng trong tự động hoá.
- Kiểm tra template path và branch có khớp với repo.

#### Kết nối với các phần khác

- Trước khi tạo pipeline, hãy hoàn thành cấu hình stage trong SAM.
- Thêm kiểm thử và giám sát để pipeline hoạt động toàn diện.

Note (hình ảnh): Chụp màn hình `Create pipeline` và `Connection ARN` vào `images/5-Workshop/5.5-Policy/`.
