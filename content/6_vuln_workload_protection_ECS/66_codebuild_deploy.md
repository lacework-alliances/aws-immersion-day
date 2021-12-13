---
title: "CodeBuild: Deploy to ECS"
chapter: false
weight: 66
pre: "<b>6.6 </b>"
---

The Deploy phase pulls our image from the ECR repository and deploys to our ECS cluster. This is done using CodeBuild.

1. Review the [codebuild-deploy-ecs.yaml](https://github.com/jefferyfry/aws-immersion-day-with-lacework-code/blob/master/app/codebuild-deploy-ecs.yaml) again. This file defines this Deploy phase.
2. In your CodePipeline console, expand **Build** and click on **Build projects**.
   ![AWS Codebuild Projects](/images/aws-codebuild-projects.png)
3. Click on the _codebuild-deploy-ecs_ Build project.
   ![AWS Codebuild Build](/images/aws-codebuild-deploy-ecs.png)
4. You can view the **Build history**, **Build details** and **Metrics**.
   ![AWS Codebuild Build](/images/aws-codebuild-metrics.png)
