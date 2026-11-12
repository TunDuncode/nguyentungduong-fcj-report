---
title : "Deploy Frontend with AWS Amplify"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.6. </b> "
---

#### Goal

Deploy the GameHub frontend using AWS Amplify and configure the build process.

#### Step 1: Initialize the Amplify app

1. Open Amplify Console.
2. Click `Deploy an app`.
3. Select `GitHub` as the source provider.
4. Authorize the repo and choose the branch.

#### Step 2: Choose branch and folder

1. Select the deployment branch, e.g. `V1`.
2. If the repo is a monorepo, enable `My app is a monorepo`.
3. Set `Monorepo root directory` to `frontend`.

#### Step 3: Build configuration for Flutter web

Use this configuration to build Flutter web in Amplify:
```yaml
version: 1
applications:
  - frontend:
      phases:
        build:
          commands:
            - ORIGINAL_DIR=$(pwd)
            - which xz || sudo yum install -y xz
            - cd /tmp
            - wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.22.0-stable.tar.xz
            - tar xf flutter_linux_3.22.0-stable.tar.xz
            - export PATH="$PATH:/tmp/flutter/bin"
            - cd $ORIGINAL_DIR
            - flutter doctor
            - flutter config --enable-web
            - flutter channel stable
            - flutter upgrade
            - flutter pub get
            - flutter build web --release --dart-define=COGNITO_REGION=$COGNITO_REGION --dart-define=COGNITO_USER_POOL_ID=$COGNITO_USER_POOL_ID --dart-define=COGNITO_CLIENT_ID=$COGNITO_CLIENT_ID --dart-define=API_GATEWAY_WS_URL=$API_GATEWAY_WS_URL --dart-define=API_GATEWAY_HTTP_URL=$API_GATEWAY_HTTP_URL
      artifacts:
        baseDirectory: build/web
        files:
          - "**/*"
      cache:
        paths: []
    appRoot: frontend
```

#### Step 4: Environment variables

Add these Amplify environment variables:
- `COGNITO_REGION`
- `COGNITO_USER_POOL_ID`
- `COGNITO_CLIENT_ID`
- `API_GATEWAY_HTTP_URL`
- `API_GATEWAY_WS_URL`
- `LOCAL_API_URL`
- `USE_LOCAL_BACKEND`
- `APK_DOWNLOAD_URL`

#### Step 5: Review and deploy

1. Review the app settings.
2. Click `Save and deploy`.
3. Amplify will build and host the frontend.

#### Result

- The frontend will be hosted at an Amplify URL.
- Every push to the deploy branch triggers a build.

Note: Add a placeholder image for Amplify setup in `images/5-Workshop/5.6-Cleanup/amplify-setup.svg`.
