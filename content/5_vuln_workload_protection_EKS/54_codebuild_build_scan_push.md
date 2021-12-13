---
title: "CodeBuild: Build, Scan & Push"
chapter: false
weight: 54
pre: "<b>5.4 </b>"
---

The Build phase includes the commands to build, scan and push our image. CodeBuild uses a build project which can be defined through a YAML file. 

1. Review the [codebuild-scan-push.yaml](https://github.com/jefferyfry/aws-immersion-day-with-lacework-code/blob/master/app/codebuild-scan-push.yaml) again. This file defines this Build phase.
2. In your CodePipeline console, expand **Build** and click on **Build projects**.
![AWS Codebuild Projects](/images/aws-codebuild-projects.png)
3. Click on the _codebuild-build_ Build project.
![AWS Codebuild Build](/images/aws-codebuild-build.png)
4. You can view the **Build history**, **Build details** and **Metrics**.
![AWS Codebuild Build](/images/aws-codebuild-metrics.png)
