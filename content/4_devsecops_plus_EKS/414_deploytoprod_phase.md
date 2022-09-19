---
title: "DeployToProduction Phase"
chapter: false
weight: 414
pre: "<b>4.14 </b>"
---

In the final phase, DeployToProduction, we deploy our application to our production environment.
This is done by applying a Kubernetes deployment manifest (the one that was previously scanned as part of IaC security) that
pulls our production image.

![deploy-to-production](/images/deploy-to-production.png)

The Cloudformation specification of the DeployToProduction phase is as follows:
```yaml
        - Name: DeployToProduction
          Actions:
            - Name: DeployToProduction
              ActionTypeId:
                Category: Build
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildDeployProductionProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: DeployProductionOutput
              RunOrder: 11
```

This phase is backed by an AWS CodeBuild project CodeBuildDeployProductionProject:

```yaml
  CodeBuildDeployProductionProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: DeployToProduction
      Description: "Deploy to Production"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-deploy-prod.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        EnvironmentVariables:
          - Name: AWS_ACCOUNT_ID
            Value: !Ref AWS::AccountId
          - Name: AWS_REGION
            Value: !Ref AWS::Region
          - Name: DOCKER_REG
            Value: !Sub "${AWS::AccountId}.dkr.ecr.${AWS::Region}.amazonaws.com"
          - Name: EKS_CLUSTER
            Value: !Sub "${AWS::AccountId}-eks-${LaceworkAccountName}"
          - Name: IMAGE_NAME
            Value: "prod-demo-app"
          - Name: IMAGE_TAG
            Value: "latest"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-deploy-prod.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-deploy-prod.yaml) that has the actual commands:

```yaml
version: 0.2
phases:
  post_build:
    commands:
      - aws eks update-kubeconfig --region $AWS_REGION --name $EKS_CLUSTER --role-arn arn:aws:iam::$AWS_ACCOUNT_ID:role/eks-codebuild-kubectl-role
      - sed "s|imageName|$DOCKER_REG/$IMAGE_NAME:$IMAGE_TAG|g" deployment.yaml > prod-deployment.yaml
      - cat prod-deployment.yaml
      - kubectl apply -f prod-deployment.yaml -n prod-demo-app
      - while [ -z "$url" ]; do url=$(kubectl describe service demo-app -n prod-demo-app | grep 'LoadBalancer Ingress:' | awk '{printf "http://%s",$3;}'); sleep 2; done
      - echo "$url"
      - echo "Prod Demo App launched!"
```

In this buildspec file, we authenticate with the EKS cluster, make a minor edit to the Kubernetes deployment manifest for the new image and then apply the manifest to deploy the application.

You can view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.
