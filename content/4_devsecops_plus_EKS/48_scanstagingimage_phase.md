---
title: "ScanStagingImage Phase"
chapter: false
weight: 48
pre: "<b>4.8 </b>"
---

In the ScanStagingImage phase, we scan our staging repository for software and OS vulnerabilities. Why do we do this? In our example application,
we have just one image. But in a real world application you will likely have dozens of images - some authored by your teams while other are 3rd party and 
open-source. These all need to be checked. Again, we will use the [Lacework CLI (registry scanning)](https://docs.lacework.com/console/different-types-of-scanning#public-registry-scanning) to check for vulnerabilities in the staging repository.

![scan-staging-image](/images/scan-staging-image.png)

The Cloudformation specification of the ScanStagingImage phase is as follows:
```yaml
        - Name: ScanStagingImage
          Actions:
            - Name: ScanStagingImage
              ActionTypeId:
                Category: Test
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildScanStagingImageProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: ScanStagingImage
              RunOrder: 5
```

This phase is backed by an AWS CodeBuild project CodeBuildScanStagingImageProject:

```yaml
  CodeBuildScanStagingImageProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: ScanStagingImage
      Description: "Scan Staging Image"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-scan-staging-image.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        EnvironmentVariables:
          - Name: IMAGE_NAME
            Value: "staging-demo-app"
          - Name: DOCKER_REG
            Value: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-scan-staging-image.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-scan-staging-image.yaml) that has the actual commands:

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

In this buildspec file, we use the Lacework CLI to scan our staging ECR repository.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

Scroll down the log to find security issues in the staging repository. We see many vulnerabilities identified.

![scan-staging-log](/images/scan-staging-log.png)

You can also [view these vulnerabilities in the Lacework console](https://laceworkshop.lacework.net/ui/investigation/container/VulnerabilityDashboard).

![vulnerabilities-console](/images/vulnerabilities-console.png)

***
# Challenge
{{%expand "Why is it important to have a staging repository?" %}} The staging repository contains all the released applications that are ready to go to production. It becomes the last archive of images to check before they move to production. {{% /expand%}}
