---
title: "Execute the Pipeline"
chapter: false
weight: 57
pre: "<b>5.7 </b>"
---

We have reviewed the phases of our pipeline. Let's execute it! We will execute our pipeline manually, but it can execute automatically when the code has been updated.

1. Go to [AWS CodePipeline in your AWS console](https://console.aws.amazon.com/codesuite/codepipeline/pipelines).
   ![AWS Codepipeline](/images/aws-codepipeline.png)
2. Click on the _codepipeline-eks_ pipeline. 
   ![AWS Codepipeline EKS](/images/aws-codepipeline-eks.png)
3. Click on the **Release change** button. This will cause the pipeline to execute.
   ![AWS Codebuild Progress](/images/aws-codebuild-progress.png)
4. The CodePipeline console will automatically show the progress of the build. For each phase, you can click on the **Details** link to see the CodeBuild logs. Do this for the **Build** phase.
   ![AWS Codebuild Build Details](/images/aws-codebuild-build-details.png)
5. Scroll down through the log to see the build output. Notice the Lacework scan output and the vulnerabilities found.
6. Go back and view the logs for the Deploy phase. Notice the Kubernetes manifest that deploys the application.
   ![AWS Codebuild Deploy Logs](/images/aws-codebuild-deploy-eks-log.png)
7. Copy the URL at the bottom of the log and paste in your browser to view the application.
   ![AWS Codebuild Deploy Logs](/images/demo-app.png)