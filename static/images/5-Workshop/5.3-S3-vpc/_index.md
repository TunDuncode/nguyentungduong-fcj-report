---
title : "Initialize SAM Pipeline"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Step 1: Initialize the pipeline

1. Open a terminal in the project root.
2. Run:
```bash
sam pipeline init --bootstrap
```

3. Answer the prompts as follows:
- `Select a pipeline template`: `1` (AWS Quick Start Pipeline Templates)
- `Select CI/CD system`: `5` (AWS CodePipeline)
- `Which pipeline template would you like to use?`: `2` (Two-stage pipeline)
- `Do you want to go through stage setup process now?`: `y`

#### Step 2: Configure the Dev stage

When prompted for the Dev stage:
- `Stage configuration name`: `dev`
- `Select a credential source`: `2` (default named profile)
- `Enter the region`: `ap-southeast-1` or your chosen region
- If prompted for profile, enter `gamehub`
- For role and artifact bucket prompts, press `Enter` to let SAM create defaults
- `Does your application contain any IMAGE type Lambda functions?`: `n`

#### Step 3: Configure the Prod stage

1. Configure the Prod stage if you use a two-stage pipeline.
2. `Stage configuration name`: `prod`.
3. `Select a credential source`: `2` or `1`.
4. `Enter the region`: same region or a different region depending on your deployment strategy.

#### Step 4: Verify the pipeline files

Run:
```bash
ls pipeline
```
The expected files include:
- `pipeline/samconfig.toml`
- `pipeline/codepipeline.yaml`
- `buildspec_deploy.yml`

#### Notes

- `sam pipeline init --bootstrap` bootstraps an S3 artifact bucket and related resources.
- `samconfig.toml` contains stage and profile settings.
- You can edit `samconfig.toml` after initialization to customize stage parameters.

#### Commit and push

```bash
git add pipeline/*
git commit -m "chore(ci): add sam pipeline config for GameHub"
git push origin main
```

Note: Add a placeholder image for the init flow in `images/5-Workshop/5.3-S3-vpc/sam-init.svg`.
