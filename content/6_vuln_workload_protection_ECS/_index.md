---
title: "Vulnerability & Workload Protection (DevSecOps) with CodePipeline, CodeBuild, ECR & ECS"
chapter: false
weight: 6
pre: "<b>6 </b>"
---

In this section, we will set up a CI/CD pipeline with AWS CodePipeline and CodeBuild. Our pipeline will take our code from CodeCommit and build a docker image. It will the image to Amazon Elastic Container Registry (ECR). Then we will deploy it to a staging environment that runs on an Amazon Elastic Container Service (ECS) cluster using CodeBuild. At each stage, Lacework protects your application and cloud environment.

## What We Will Do

* Review the CI/CD architecture.
* Review the CloudFormation template that was used to set up the lab.
* Inspect the configuration of CodePipeline, CodeBuild, CodeDeploy, ECR, ECS and Lacework components.
* Execute the pipeline manually.
* Understand how Lacework protects your DevOps pipeline and multiple stages.

## Pipeline
![Pipeline](/images/pipeline-ecs.png)
