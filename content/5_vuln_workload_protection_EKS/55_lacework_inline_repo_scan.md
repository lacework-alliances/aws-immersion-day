---
title: "Lacework Container Security: Image and Registry Scanning"
chapter: false
weight: 55
pre: "<b>5.5 </b>"
---

The Build phase includes a Lacework vulnerability scan using the Lacework Inline Scanner. This tool scans Docker images for image and software package vulnerabilities. Additionally, Lacework has been set up to scan the Docker repositories. This allows you to detect vulnerable software and prevent it from being deployed.

1. View the [lines of code in the CodeBuild buildspec](https://github.com/jefferyfry/aws-immersion-day-with-lacework-code/blob/master/app/codebuild-scan-push.yaml#L13) that include the Lacework Inline Scanner.
```
- export LW_ACCOUNT_NAME=$LW_ACCOUNT_NAME
- export LW_ACCESS_TOKEN=$LW_ACCESS_TOKEN
- export LW_SCANNER_DISABLE_UPDATES=true
- rm -rf ./evaluations/$IMAGE_NAME/$CODEBUILD_BUILD_NUMBER/evaluation_*.json || true
- curl -L https://github.com/lacework/lacework-vulnerability-scanner/releases/latest/download/lw-scanner-linux-amd64 -o lw-scanner
- chmod +x lw-scanner
- ./lw-scanner image evaluate $DOCKER_REG/$IMAGE_NAME $CODEBUILD_BUILD_NUMBER --build-id $CODEBUILD_BUILD_NUMBER --data-directory .
```
2. The Docker push command pushes the Docker image to a ECR repository that is automatically scanned by Lacework.
```
- aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $DOCKER_REG
- docker image push -a "$DOCKER_REG/$IMAGE_NAME"
```
3. Go to **Settings > Integrations > Container Registries** in your Lacework Console. This page shows the ECR registry and inline scanner setups.
![Lacework Container Registries](/images/lacework-container-registries.png)
