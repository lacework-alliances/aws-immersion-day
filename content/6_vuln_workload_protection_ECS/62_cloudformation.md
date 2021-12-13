---
title: "Lacework, CodePipeline, CodeBuild, ECR & ECS in CloudFormation"
chapter: false
weight: 62
pre: "<b>6.2 </b>"
---

Lacework, CodePipeline, CodeBuild, ECR & EKS for our CI/CD pipeline is provisioned using CloudFormation. We will review these CloudFormation templates.


1. Go to https://github.com/jefferyfry/aws-immersion-day-with-lacework-code in your browser.
   ![Lacework Code Github](/images/lacework-code-github.png)
2. Go to the _templates_ directory and view the _setup-pipelines.template.yml_. This CloudFormation template provisions CodePipeline, CodeBuild & ECR resources.
3. CodeBuild requires _buildspec_ files. Go to the _app_ directory and view the codebuild-scan-push.yaml and codebuild-deploy-ecs.yaml files. codebuild-scan-push.yaml has the commands to perform a docker build, Lacework image vulnerability scan and docker push to ECR. codebuild-deploy-eks.yaml deploys the container to the ECS cluster.
4. Go to the _templates_ directory and view the _setup-ecs.template.yml_. This CloudFormation template our ECS cluster with the Lacework agent for runtime protection.

These templates have already been executed in your AWS environment. We can now view these resources in your AWS console.