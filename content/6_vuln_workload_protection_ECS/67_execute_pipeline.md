---
title: "Execute the Pipeline"
chapter: false
weight: 67
pre: "<b>6.7 </b>"
---

We have reviewed the phases of our pipeline. Let's execute it! We will execute our pipeline manually, but it can execute automatically when the code has been updated.

1. Go to [AWS CodePipeline in your AWS console](https://console.aws.amazon.com/codesuite/codepipeline/pipelines).
   ![AWS Codepipeline](/images/aws-codepipeline.png)
2. Click on the _codepipeline-ecs_ pipeline.
   ![AWS Codepipeline ECS](/images/aws-codepipeline-ecs.png)
3. Click on the **Release change** button. This will cause the pipeline to execute.
   ![AWS Codebuild Progress](/images/aws-codebuild-progress.png)
4. The CodePipeline console will automatically show the progress of the build. For each phase, you can click on the **Details** link to see the CodeBuild logs. Do this for the **Build** phase.
   ![AWS Codebuild Build Details](/images/aws-codebuild-build-details.png)
5. Scroll down through the log to see the build output. Notice the Lacework scan output and the vulnerabilities found.
6. Go back and view the logs for the Deploy phase. For ECS deployment, we provide an imagedefinitions.json with the updated image and tag. This updates the ECS task definition. You can learn more about imagedefinitions.json [here](https://docs.aws.amazon.com/codepipeline/latest/userguide/file-reference.html#pipelines-create-image-definitions).
   ![AWS Codebuild Deploy Logs](/images/aws-codebuild-deploy-ecs-log.png)
7. To view the application, go to your [ECS console](https://us-west-2.console.aws.amazon.com/ecs/home).
   ![AWS ECS Console](/images/aws-ecs-console.png)
8. Click on the ECS cluster.
9. Click on the _demo-app-ecs-service_.
10. Click on the running task.
    ![ECS Task](/images/aws-ecs-task.png)
11. On the task page, find the **Public IP**. Paste this IP address into your browser to view the application.
    ![Demo App](/images/demo-app.png)