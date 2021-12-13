---
title: "CodeBuild: Deploy to EKS"
chapter: false
weight: 56
pre: "<b>5.6 </b>"
---

The Deploy phase pulls our image from the ECR repository and deploys to our EKS cluster. This is done using CodeBuild.

1. Review the [codebuild-deploy-eks.yaml](https://github.com/jefferyfry/aws-immersion-day-with-lacework-code/blob/master/app/codebuild-deploy-eks.yaml) again. This file defines this Deploy phase.
2. In your CodePipeline console, expand **Build** and click on **Build projects**.
   ![AWS Codebuild Projects](/images/aws-codebuild-projects.png)
3. Click on the _codebuild-deploy-eks_ Build project.
   ![AWS Codebuild Build](/images/aws-codebuild-deploy-eks.png)
4. You can view the **Build history**, **Build details** and **Metrics**.
   ![AWS Codebuild Build](/images/aws-codebuild-metrics.png)
