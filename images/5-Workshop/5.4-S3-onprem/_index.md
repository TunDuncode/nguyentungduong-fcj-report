---
title : "Configure Repository and Stage"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Goal

This section helps you configure the repository and stage settings exactly so the SAM pipeline runs correctly.

#### Important details

- `Repository subfolder`: the backend folder, e.g. `backend`.
- `Template path`: the SAM or CloudFormation template path, e.g. `backend/template.yaml`.
- `SSM Prefix`: e.g. `gamehub/`.
- `Stack names`: `GameHub-dev`, `GameHub-prod`.
- `Git branch`: `main`, `V1`, or your deployment branch.

#### Configuration steps

1. When SAM asks for `Repository root path`, enter `backend` if your backend is stored there.
2. In a monorepo, point the pipeline to the backend folder only.
3. Ensure the `template path` points to the correct SAM template file.

#### Stage management

- Dev stage is for testing and fast deployments.
- Prod stage is for stable production deployments.
- Keep stage and stack names aligned for easier tracking.

#### Verify settings

- Review `pipeline/samconfig.toml` for stage and region values.
- Review `pipeline/codepipeline.yaml` to confirm the template reference.
- Adjust `samconfig.toml` if you need to change stage names or regions.

#### Commit recommendation

```bash
git add .
git commit -m "ci: add sam pipeline configuration for GameHub"
git push origin main
```

Note: Add placeholder images for the pipeline file list and samconfig preview in `images/5-Workshop/5.4-S3-onprem/pipeline-files.svg`.
