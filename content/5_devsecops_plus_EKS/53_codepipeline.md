---
title: "CodePipeline: A DevSecOps Pipeline"
chapter: false
weight: 53
pre: "<b>5.3 </b>"
---

AWS CodePipeline orchestrates our CI/CD process. It pulls our code from a S3 bucket and then uses AWS CodeBuild to build, scan and push our application container image.

1. Go to [AWS CodePipeline in your AWS console](https://console.aws.amazon.com/codesuite/codepipeline/pipelines).
![AWS Codepipeline](/images/aws-codepipeline.png)
2. Click on the _AWSSecuredPipeline_ pipeline. This pipeline has 11 phases:
   
   - **Source**: pulls the application source code from Amazon S3. 
   - **ScanCode** performs a Java code analysis and identifies security issues.
   - **ScanIaC** scans the CloudFormation and Kubernetes manifest to identify security misconfigurations.
   - **BuildScanPush** builds our Docker image, scans for OS and package security vulnerabilities and then pushes it to our ECR repository.
   - **ScanStagingImage** scans our staging repository to identify additional OS and package security vulnerabilities.
   - **DeployToStaging** deploys our application to our EKS staging environment.
   - **ScanStagingConfig** scans our staging environment for security misconfigurations.
   - **ApprovalStage** provides a manual approval step before deploying the application to the production environment.
   - **PromoteToProductionRepo** promotes our application from our staging repository to our production repository.
   - **ScanProductionImage** scans our production repository to identify additional OS and package security vulnerabilities.
   - **DeployToProduction** deploys our application to our EKS production environment.
   
   ![AWS Codepipeline EKS](/images/aws-codepipeline-eks.png)
3. Click the **Release Change** button to execute the build if it has not already executed. For each phase, you can click on the **Details** link to see the execution logs.

Let's examine these phases in detail.