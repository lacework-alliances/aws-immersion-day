---
title: "ScanCode Phase"
chapter: false
weight: 45
pre: "<b>4.5 </b>"
---

In the ScanCode phase, we check our source code for security issues using [AWS CodeGuru](https://docs.aws.amazon.com/codeguru/index.html). AWS CodeGuru can also recommend code quality improvements.

![scan code](/images/scan-code-phase.png)

The Cloudformation specification of the ScanCode phase is as follows:
```yaml
        - Name: ScanCode
          Actions:
            - Name: ScanCode
              ActionTypeId:
                Category: Test
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildScanCodeProject
              InputArtifacts:
                - Name: App
              OutputArtifacts:
                - Name: CodeScanOutput
              RunOrder: 2
```

This phase is backed by an AWS CodeBuild project CodeBuildScanCodeProject:

```yaml
  CodeBuildScanCodeProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: ScanCode
      Description: "Scan Code"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-scan-code.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        PrivilegedMode: true
      ServiceRole: !Ref CodeBuildServiceRole
```

This is ultimately backed by the AWS CodeBuild buildspec file [codebuild-scan-code.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-scan-code.yaml) that has the actual commands:

```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      java: corretto11
    commands:
      - java -version
      - mvn --version
      - git --version
      - curl -OL https://github.com/aws/aws-codeguru-cli/releases/download/0.2.1/aws-codeguru-cli.zip
      - unzip aws-codeguru-cli.zip
      - export PATH=$PATH:./aws-codeguru-cli/bin
  build:
    commands:
      - aws-codeguru-cli --region us-west-2 --no-prompt  --fail-on-recommendations --root-dir ./ --src src --output ./output || true
      - cat ./output/recommendations.json
```

In this buildspec file, we first install the _aws-codeguru-cli_ and then run the cli against our source code. Notice that we specified _--fail-on-recommendations_ which would ordinarily fail our pipeline on any issues that are found. For our example though, we let it proceed if issues our found.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

![aws-codebuild-scan-code-build-logs](/images/aws-codebuild-scan-code-build-logs.png)

Scroll down the log to find a security issue and Java best practices issue that was discovered in our code.

![aws-codeguru-security-issue](/images/aws-codeguru-security-issue.png)

***
# Challenge
{{%expand "Which languages does CodeGuru support" %}} Python and Java. {{% /expand%}}

