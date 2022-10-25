---
title: "DeployToStaging Phase"
chapter: false
weight: 59
pre: "<b>5.9 </b>"
---

In the DeployToStaging phase, we deploy our application to our staging environment - an Amazon Elastic Kubernetes Service (EKS) cluster. 
This is done by applying a Kubernetes deployment manifest (the one that was previously scanned as part of IaC security) that
pulls our staging image.

![deploy-to-staging](/images/deploy-to-staging.png)

The Cloudformation specification of the DeployToStaging phase is as follows:
```yaml
        - Name: DeployToStaging
          Actions:
            - Name: DeployToStaging
              ActionTypeId:
                Category: Build
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildDeployStagingProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: DeployStagingOutput
              RunOrder: 6
```

This phase is backed by an AWS CodeBuild project CodeBuildDeployStagingProject:

```yaml
  CodeBuildDeployStagingProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: DeployToStaging
      Description: "Deploy to Staging"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-deploy-staging.yaml"
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
            Value: "staging-demo-app"
          - Name: IMAGE_TAG
            Value: "latest"
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-deploy-staging.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-deploy-staging.yaml) that has the actual commands:

```yaml
version: 0.2
phases:
  post_build:
    commands:
      - aws eks update-kubeconfig --region $AWS_REGION --name $EKS_CLUSTER --role-arn arn:aws:iam::$AWS_ACCOUNT_ID:role/eks-codebuild-kubectl-role
      - sed "s|imageName|$DOCKER_REG/$IMAGE_NAME:$IMAGE_TAG|g" deployment.yaml > staging-deployment.yaml
      - cat staging-deployment.yaml
      - kubectl apply -f staging-deployment.yaml -n staging-demo-app
      - while [ -z "$url" ]; do url=$(kubectl describe service demo-app -n staging-demo-app | grep 'LoadBalancer Ingress:' | awk '{printf "http://%s",$3;}'); sleep 2; done
      - echo "$url"
      - echo "Staging Demo App launched!"
```

In this buildspec file, we authenticate with the EKS cluster, make a minor edit to the Kubernetes deployment manifest for the new image and then apply the manifest to deploy the application.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

Scroll down the log to the deployment output.

![scan-deploy-staging-log](/images/deploy-staging-log.png)
