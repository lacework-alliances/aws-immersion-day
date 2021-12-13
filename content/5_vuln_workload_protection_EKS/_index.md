---
title: "Vulnerability & Workload Protection (DevSecOps) with CodePipeline, CodeBuild, ECR & EKS"
chapter: false
weight: 5
pre: "<b>5 </b>"
---

In this section, we will set up a CI/CD pipeline with AWS CodePipeline and CodeBuild. Our CodePipeline pipeline will take our code from S3 and build a docker image with CodeBuild. CodeBuild will also scan the image for vulnerabilities and then push it to Amazon Elastic Container Registry (ECR). Then we will deploy it to a staging environment that runs on an Amazon Elastic Kubernetes Service (EKS) cluster using CodeBuild. At each stage, Lacework protects your application and cloud environment.

## What We Will Do

* Review the CI/CD architecture.
* Review the CloudFormation template that was used to set up the lab.
* Inspect the configuration of CodePipeline, CodeBuild, ECR, EKS and Lacework components.
* Execute the pipeline manually.
* Understand how Lacework protects your DevOps pipeline and multiple stages.

## Pipeline
![Pipeline](/images/pipeline-eks.png)


