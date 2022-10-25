---
title: "BuildScanPush Phase"
chapter: false
weight: 57
pre: "<b>5.7 </b>"
---

In the BuildScanPush phase, we build our Docker image, scan it for software package and OS library security vulnerabilities and if it passes, we push it to ECR. The scanning for software and OS vulnerabilities is also performed by the [Lacework CLI (inline scanner)](https://docs.lacework.com/onboarding/integrate-inline-scanner).

![build-scan-push](/images/build-scan-push.png)

The Cloudformation specification of the BuildScanPush phase is as follows:
```yaml
        - Name: BuildScanPush
          Actions:
            - Name: BuildScanPush
              ActionTypeId:
                Category: Build
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildBuildScanPushProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: BuildScanPushOutput
              RunOrder: 4
```

This phase is backed by an AWS CodeBuild project CodeBuildBuildScanPushProject:

```yaml
  CodeBuildBuildScanPushProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: BuildScanPush
      Description: "Build, Scan, Push"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-build-scan-push.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        PrivilegedMode: true
        EnvironmentVariables:
          - Name: AWS_REGION
            Value: !Ref AWS::Region
          - Name: IMAGE_NAME
            Value: "staging-demo-app"
          - Name: DOCKER_REG
            Value: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-build-scan-push.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-build-scan-push.yaml) that has the actual commands:

```yaml
version: 0.2
env:
  parameter-store:
    LW_ACCOUNT: "LW_ACCOUNT"
    LW_ACCESS_TOKEN: "INLINE_SCANNER_TOKEN"
phases:
  install:
    runtime-versions:
      java: corretto8
    commands:
      - curl -L https://github.com/lacework/lacework-vulnerability-scanner/releases/latest/download/lw-scanner-linux-amd64 -o lw-scanner
      - chmod +x lw-scanner
  build:
    commands:
      - mvn clean install
      - pwd
      - ls
      - ls target
      - docker build -t "$DOCKER_REG/$IMAGE_NAME:$CODEBUILD_BUILD_NUMBER" -t "$DOCKER_REG/$IMAGE_NAME:latest" .
  post_build:
    commands:
      - export LW_ACCOUNT_NAME=$LW_ACCOUNT
      - export LW_ACCESS_TOKEN=$LW_ACCESS_TOKEN
      - export LW_SCANNER_DISABLE_UPDATES=true
      - export LW_SCANNER_SAVE_RESULTS=true
      - rm -rf ./evaluations/$IMAGE_NAME/$CODEBUILD_BUILD_NUMBER/evaluation_*.json || true
      - ./lw-scanner image evaluate $DOCKER_REG/$IMAGE_NAME $CODEBUILD_BUILD_NUMBER --build-id $CODEBUILD_BUILD_NUMBER --data-directory . || true
      - aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $DOCKER_REG
      - docker image push -a "$DOCKER_REG/$IMAGE_NAME"
```

In this buildspec file, we first build our Docker image. Then we install and run the Lacework CLI (inline scanner) to check for software and OS security issues. Then we push the image to our ECR repository.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

Scroll down the log to find security issues in our Docker image. We see many CVEs identified for the Java software libraries used in our application.

![docker-image-issues](/images/docker-image-issues.png)

***
# Challenge
{{%expand "Can you customize the software and OS vulnerability security policies?" %}} YES! https://docs.lacework.com/onboarding/integrate-inline-scanner#container-vulnerability-policy-support. {{% /expand%}}