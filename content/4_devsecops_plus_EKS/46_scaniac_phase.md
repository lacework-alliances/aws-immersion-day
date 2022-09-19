---
title: "ScanIaC Phase"
chapter: false
weight: 46
pre: "<b>4.6 </b>"
---

In the ScanIaC phase, we check our infrastructure as code (IaC) files for security misconfigurations that could make us vulnerable due to items like mis-configured security groups, IAM policies and more. We use the Lacework CLI to check for IaC misconfigurations. [Lacework IaC security](https://docs.lacework.com/iac/)
can check Terraform, CloudFormation, Helm, Kustomize and Kubernetes manifest files for security issues. Our workshop codebase uses CloudFormation and Kubernetes manifests and these will be scanned.

![scan-iac-phase](/images/scan-iac-phase.png)

The Cloudformation specification of the ScanIaC phase is as follows:
```yaml
        - Name: ScanIaC
          Actions:
            - Name: ScanIaC
              ActionTypeId:
                Category: Test
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildScanIaCProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: IaCScanOutput
              RunOrder: 3
```

This phase is backed by an AWS CodeBuild project CodeBuildScanIaCProject:

```yaml
  CodeBuildScanIaCProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: ScanIaC
      Description: "Scan IaC"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-scan-iac.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        PrivilegedMode: true
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-scan-iac.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-scan-iac.yaml) that has the actual commands:

```yaml
version: 0.2
env:
  parameter-store:
    SOLUBLE_ORG_ID: "SOLUBLE_ORG_ID"
    SOLUBLE_API_TOKEN: "SOLUBLE_API_TOKEN"
phases:
  install:
    commands:
      - curl https://raw.githubusercontent.com/soluble-ai/soluble-cli/master/linux-install.sh | bash
  build:
    commands:
      - export SOLUBLE_ORG_ID=$SOLUBLE_ORG_ID
      - export SOLUBLE_API_TOKEN=$SOLUBLE_API_TOKEN
      - soluble k8s-scan --upload --fail high || true
      - soluble cfn-scan --upload --fail high || true
```

In this buildspec file, we install the Lacework CLI (soluble) and then run the cli against our source code. We can use the _--fail_ which to fail the pipeline.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

Scroll down the log to find security issues in our Kubernetes deployment manifest.

![iac-k8s-issues](/images/iac-k8s-issues.png)

***
# Challenge
{{%expand "Can you customize the IaC security policies?" %}} YES! See https://docs.lacework.com/iac/modify-iac-security-policies. {{% /expand%}}