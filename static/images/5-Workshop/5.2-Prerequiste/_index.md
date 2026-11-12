---
title : "Prerequisites"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Required preparations

Before starting the pipeline and deployment, ensure you have:
- an AWS account with permissions for CloudFormation, S3, IAM, CodePipeline, CodeBuild, Amplify, and CloudWatch,
- AWS CLI and AWS SAM CLI installed and configured,
- a GitHub repository containing your GameHub source code,
- a clear branch strategy and repository layout.

#### Environment checks

1. Open a terminal in the repo root.
2. Verify AWS CLI and SAM CLI versions:
```bash
aws --version
sam --version
```
3. Configure your AWS profile:
```bash
aws configure --profile gamehub
```
4. Verify the profile works:
```bash
aws sts get-caller-identity --profile gamehub
```

#### Information to prepare

- `Region`, e.g. `ap-southeast-1`.
- `Repository subfolder`, e.g. `backend` or `frontend`.
- `SSM Prefix`, e.g. `gamehub/`.
- `Git branch`, e.g. `main` or `V1`.
- `Template file path`, e.g. `backend/template.yaml`.
- `Stack names`, e.g. `GameHub-dev`, `GameHub-prod`, `GameHubPipeline`.

#### Quick setup

1. Install SAM CLI if needed:
```bash
pip install --user aws-sam-cli
sam --version
```
2. Install AWS CLI if needed:
```bash
pip install --user awscli
aws --version
```
3. Configure the workshop profile:
```bash
aws configure --profile gamehub
```

#### Tips

- In a monorepo, keep `backend/` and `frontend/` clearly separated.
- Use a dedicated deploy branch to manage change flows.
- Create profile aliases like `gamehub-dev` and `gamehub-prod` for multiple environments.

Note: Add a screenshot of `aws configure` and `sam --version` output in `images/5-Workshop/5.2-Prerequiste/aws-config.svg`.
