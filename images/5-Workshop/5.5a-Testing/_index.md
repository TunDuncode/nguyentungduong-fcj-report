---
title : "Testing and Pipeline Validation"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.5a. </b> "
---

#### Goal

Add an automated test stage to the pipeline so failures are caught before deployment.

#### Detailed coverage

- Create a `Test` stage in CodePipeline.
- Use AWS CodeBuild for unit and integration tests.
- Fail deployments if tests fail.
- Surface test results clearly in the pipeline.

#### Example buildspec

Place test commands in `buildspec_deploy.yml`:
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

#### Node.js example

For Node.js or frontend tests:
```yaml
phases:
  install:
    commands:
      - npm ci
  build:
    commands:
      - npm test
```

#### Best practices

- Separate unit and integration tests.
- Run the most important tests early.
- Use CodeBuild logs for debugging.
- Name stages and projects clearly.

#### Expected behavior

- test success continues the pipeline,
- test failure stops the pipeline and shows the failure reason.

Note: Add a placeholder image for the test run in `images/5-Workshop/5.5a-Testing/test-run.svg`.
