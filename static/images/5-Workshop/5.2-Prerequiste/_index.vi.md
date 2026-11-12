---
title : "Chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Yêu cầu trước khi bắt đầu

Trước khi bắt đầu pipeline và deployment, hãy đảm bảo bạn có:
- Tài khoản AWS với quyền CloudFormation, S3, IAM, CodePipeline, CodeBuild, Amplify và CloudWatch.
- AWS CLI và AWS SAM CLI đã cài đặt và cấu hình.
- Repository trên GitHub chứa mã nguồn GameHub.
- Quy ước branch và cấu trúc thư mục rõ ràng.

#### Kiểm tra môi trường

1. Mở terminal tại thư mục gốc.
2. Kiểm tra phiên bản AWS CLI và SAM CLI:
```
aws --version
sam --version
```
3. Cấu hình profile AWS:
```
aws configure --profile gamehub
```
4. Xác nhận profile hoạt động:
```
aws sts get-caller-identity --profile gamehub
```

#### Thông tin cần chuẩn bị

- `Region`: ví dụ `ap-southeast-1`.
- `Repository subfolder`: ví dụ `backend` hoặc `frontend`.
- `SSM Prefix`: ví dụ `gamehub/`.
- `Git branch`: ví dụ `main` hoặc `V1`.
- `Template path`: ví dụ `backend/template.yaml`.
- `Stack names`: `GameHub-dev`, `GameHub-prod`, `GameHubPipeline`.

#### Hướng dẫn cài đặt nhanh

1. Cài SAM CLI nếu cần:
```powershell
pip install --user aws-sam-cli
sam --version
```
2. Cài AWS CLI nếu cần:
```powershell
pip install --user awscli
aws --version
```
3. Cấu hình profile workshop:
```powershell
aws configure --profile gamehub
```

#### Gợi ý

- Nếu repository là monorepo, giữ `backend/` và `frontend/` tách biệt.
- Dùng branch deploy riêng để kiểm soát thay đổi.
- Tạo profile `gamehub-dev` và `gamehub-prod` nếu bạn triển khai nhiều môi trường.

Note (hình ảnh): Thêm ảnh `aws configure` và `sam --version` tại `images/5-Workshop/5.2-Prerequiste/aws-config.svg`.
