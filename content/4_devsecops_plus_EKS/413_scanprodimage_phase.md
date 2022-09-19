---
title: "ScanProdImage Phase"
chapter: false
weight: 413
pre: "<b>4.13 </b>"
---

In the ScanProdImage phase, we scan our production repository for software and OS vulnerabilities like we did with the staging repository. Why do we do this? 
It's important to scan your production repositories. In rare cases, application images may mistakenly bypass the software delivery pipeline process and end up in production.
This scan is extra assurance that everything is checked. Again, we will use the [Lacework CLI (registry scanning)](https://docs.lacework.com/console/different-types-of-scanning#public-registry-scanning) to check for vulnerabilities in the repository.

![scan-production-image](/images/scan-production-image.png)

The Cloudformation specification of the ScanProdImage phase is as follows:
```yaml
        - Name: ScanProductionImage
          Actions:
            - Name: ScanProductionImage
              ActionTypeId:
                Category: Test
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildScanProductionImageProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: ScanProductionImageOutput
              RunOrder: 10
```

This phase is backed by an AWS CodeBuild project CodeBuildScanProductionImageProject:

```yaml
  CodeBuildScanProductionImageProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: ScanProductionImage
      Description: "Scan Production Image"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-scan-production-image.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        EnvironmentVariables:
          - Name: DOCKER_REG
            Value: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com"
          - Name: IMAGE_NAME
            Value: "prod-demo-app"
          - Name: IMAGE_TAG
            Value: "latest"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-scan-production-image.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-scan-production-image.yaml) that has the actual commands:

```yaml
version: 0.2
env:
  parameter-store:
    LW_ACCOUNT: "LW_ACCOUNT"
    LW_API_KEY: "LW_API_KEY"
    LW_API_SECRET: "LW_API_SECRET"
phases:
  install:
    commands:
      - curl https://raw.githubusercontent.com/lacework/go-sdk/master/cli/install.sh | bash
  build:
    commands:
      - export LW_ACCOUNT=$LW_ACCOUNT
      - export LW_API_KEY=$LW_API_KEY
      - export LW_API_SECRET=$LW_API_SECRET
      - lacework vulnerability container scan $DOCKER_REG $IMAGE_NAME latest --poll --fail_on_severity critical || true
```

In this buildspec file, we use the Lacework CLI to scan our production ECR repository.

You can view the results of this phase by clicking on the **Details** link in CodePipeline.