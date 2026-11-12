---
title : "Workshop Overview"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Workshop goals

In this section, you will learn how to:
- initialize a CI/CD pipeline for a serverless backend with AWS SAM,
- configure Dev and Prod stages,
- connect GitHub with CodePipeline,
- deploy a static frontend via AWS Amplify,
- add testing and monitoring to the deployment flow.

#### Key content

1. Initialize the pipeline using `sam pipeline init --bootstrap`.
2. Configure repository paths, template files, and stage settings.
3. Add an automated test stage.
4. Set up CloudWatch monitoring for Lambda and API Gateway.
5. Deploy a Flutter web frontend in Amplify.

#### GameHub architecture

The GameHub sample is a serverless app with:
- AWS Lambda functions for business logic,
- Amazon API Gateway for HTTP endpoints,
- AWS Cognito or custom authentication for users,
- AWS Amplify hosting for the frontend.

#### Notes

- The project name `GameHub` is an example; replace it with your own project name.
- If your backend and frontend are in one repo, use clear folder separation.
- Verify your AWS profile and region before running SAM commands.

Note: Add an architecture diagram here to make the workflow clearer. Placeholder: `images/5-Workshop/5.1-Workshop-overview/gamehub-architecture.svg`.
