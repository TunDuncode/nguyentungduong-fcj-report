---
title : "Create CodePipeline in AWS Console"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Goal

Set up a CodePipeline in the AWS Console that connects GitHub with your GameHub deployment workflow.

#### Create the GitHub connection

1. Open AWS Console → Developer Tools → Connections.
2. Click `Create connection`.
3. Select `GitHub` and authorize the repository.
4. Choose the GameHub repo.
5. Confirm the connection status is `Available`.

#### Create the pipeline

1. Open CodePipeline Console.
2. Click `Create pipeline`.
3. Choose `Use a blueprint` or `Start from scratch`.
4. Select `GitHub (version 2)` as the source provider.
5. Select the connection, repository, and branch.
6. Add a build stage with CodeBuild using `buildspec_deploy.yml`.
7. Add a deploy stage with CloudFormation pointing to `pipeline/codepipeline.yaml`.

#### Notes

- If you initialized the pipeline with `sam pipeline init`, reuse the generated `codepipeline.yaml` file.
- Save the connection ARN for automation.
- Confirm that the template path and branch match your repo structure.

#### Pipeline polish

- Add test and monitoring stages for a production-ready flow.
- Document the pipeline stage names and stack naming conventions.
- Use a stable branch for production deploys.

Note: Add UI screenshots for pipeline creation in `images/5-Workshop/5.5-Policy/create-pipeline.svg` and `images/5-Workshop/5.5-Policy/connection-arn.svg`.
