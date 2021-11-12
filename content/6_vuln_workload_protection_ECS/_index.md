---
title: "Vulnerability & Workload Protection (DevSecOps) with CodePipeline, CodeBuild, ECR & ECS"
chapter: false
weight: 5
pre: "<b>5 </b>"
---

In this section, we will set up a CI/CD pipeline with AWS CodePipeline and CodeBuild. Our pipeline will take our code from CodeCommit and build a docker image. It will the image to Amazon Elastic Container Registry (ECR). Then we will deploy it to a staging environment that runs on an Amazon Elastic Kubernetes Service (EKS) cluster using a Lambda function. At each stage, Lacework protects your application and cloud environment.

## What We Will Do

* Setup Lacework to protect our AWS cloud environment.
* Clone our example code to our CodeCommit repo.
* Create a repository for our application in Amazon ECR and scan it with Lacework.
* Create an ECS "staging" cluster and secure it with Lacework.
* Use CloudFormation to create our CodePipeline, CodeBuild stage, Lacework vulnerability scan and Lambda deployment stage.

## Architecture
![Overview Architecture](images/devsecops-architecture.png)

## Pipeline
![Pipeline](images/devsecops-pipeline.png)


