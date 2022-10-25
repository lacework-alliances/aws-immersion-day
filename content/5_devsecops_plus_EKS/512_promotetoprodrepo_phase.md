---
title: "PromoteToProdRepo Phase"
chapter: false
weight: 512
pre: "<b>5.12 </b>"
---

In the PromoteToProdRepo phase, we promote our image from a staging to production. Some applications will have multiple images that must be promoted.
Depending on the type of Docker registry, promotion may involve special tagging or copying images between repositories. For ECR, we push the image
to a production repository.

![promote-to-production-repo](/images/promote-to-production-repo.png)

The Cloudformation specification of the ScanStagingConfig phase is as follows:
```yaml
        - Name: PromoteToProductionRepo
          Actions:
            - Name: PromoteToProductionRepo
              ActionTypeId:
                Category: Build
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildPromoteProductionRepoProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: PromoteProductionRepoOutput
              RunOrder: 9
```

This phase is backed by an AWS CodeBuild project CodeBuildPromoteProductionRepoProject:

```yaml
  CodeBuildPromoteProductionRepoProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: PromoteProductionRepo
      Description: "Promote Production Repo"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-promote-production-repo.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        PrivilegedMode: true
        EnvironmentVariables:
          - Name: AWS_REGION
            Value: !Ref AWS::Region
          - Name: STAGING_IMAGE_NAME
            Value: "staging-demo-app"
          - Name: PROD_IMAGE_NAME
            Value: "prod-demo-app"
          - Name: IMAGE_TAG
            Value: "latest"
          - Name: DOCKER_REG
            Value: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-promote-production-repo.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-promote-production-repo.yaml) that has the actual commands:

```yaml


version: 0.2
phases:
  build:
    commands:
      - aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $DOCKER_REG
      - docker pull "$DOCKER_REG/$STAGING_IMAGE_NAME"
      - docker tag "$DOCKER_REG/$STAGING_IMAGE_NAME:latest" "$DOCKER_REG/$PROD_IMAGE_NAME:latest"
      - docker image push -a "$DOCKER_REG/$PROD_IMAGE_NAME"
```

In this buildspec file, we execute Docker commands to pull and push to our production repository.

You can view the results of this phase by clicking on the **Details** link in CodePipeline.