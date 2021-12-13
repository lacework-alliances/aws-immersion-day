---
title: "CodePipeline: A DevSecOps Pipeline"
chapter: false
weight: 63
pre: "<b>6.3 </b>"
---

AWS CodePipeline orchestrates our CI/CD process. It pulls our code from a S3 bucket and then uses AWS CodeBuild to build, scan and push our application container image.

1. Go to [AWS CodePipeline in your AWS console](https://console.aws.amazon.com/codesuite/codepipeline/pipelines).
   ![AWS Codepipeline](/images/aws-codepipeline.png)
2. Click on the _codepipeline-ecs_ pipeline. This pipeline has three phases. The first phase, the **Source** phase, pulls the application source code from Amazon S3. The second phase is the **Build** phase and builds, scans and pushes our image. The third phase is the **Deploy** phase and deploys to ECS.
   ![AWS Codepipeline ECS](/images/aws-codepipeline-ecs.png)

Let's examine the Build and Deploy phases in detail.