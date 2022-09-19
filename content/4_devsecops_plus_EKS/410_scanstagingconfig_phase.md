---
title: "ScanStagingConfig Phase"
chapter: false
weight: 410
pre: "<b>4.10 </b>"
---

In the ScanStagingConfig phase, we scan our staging environment and check all the active resource configurations to ensure that we
don't have misconfigurations that could make us vulnerable. To do this, we use the 
[Lacework CLI (compliance)] (https://docs.lacework.com/cli/compliance-reports#compliance-for-aws) to run an assessment
and determine if we have any issues.

![scan-staging-config](/images/scan-staging-config.png)

The Cloudformation specification of the ScanStagingConfig phase is as follows:
```yaml
        - Name: ScanStagingConfig
          Actions:
            - Name: ScanStagingConfig
              ActionTypeId:
                Category: Test
                Owner: AWS
                Version: 1
                Provider: CodeBuild
              Configuration:
                ProjectName: !Ref CodeBuildScanStagingConfigProject
              InputArtifacts:
                - Name: App
              RunOrder: 7
```

This phase is backed by an AWS CodeBuild project CodeBuildScanStagingConfigProject:

```yaml
  CodeBuildScanStagingConfigProject:
    Type: AWS::CodeBuild::Project
    Properties:
      Name: ScanStagingConfig
      Description: "Scan Staging Config"
      Artifacts:
        Type: CODEPIPELINE
      Source:
        Type: CODEPIPELINE
        BuildSpec: "codebuild-scan-staging-config.yaml"
      Environment:
        ComputeType: "BUILD_GENERAL1_SMALL"
        Image: "aws/codebuild/standard:5.0"
        Type: "LINUX_CONTAINER"
        EnvironmentVariables:
          - Name: AWS_ACCOUNT_ID
            Value: !Ref AWS::AccountId
      ServiceRole: !Ref CodeBuildServiceRole
```

This is backed by the AWS CodeBuild buildspec file [codebuild-scan-staging-config.yaml](https://github.com/lacework-alliances/aws-immersion-day-code/blob/master/app/codebuild-scan-staging-config.yaml) that has the actual commands:

```yaml
version: 0.2
env:
  parameter-store:
    LW_ACCOUNT: "LW_ACCOUNT"
    LW_API_KEY: "LW_API_KEY"
    LW_API_SECRET: "LW_API_SECRET"
phases:
  install:
    commands:
      - curl https://raw.githubusercontent.com/lacework/go-sdk/master/cli/install.sh | bash
  build:
    commands:
      - export LW_ACCOUNT=$LW_ACCOUNT
      - export LW_API_KEY=$LW_API_KEY
      - export LW_API_SECRET=$LW_API_SECRET
      - lacework compliance aws run-assessment $AWS_ACCOUNT_ID --noninteractive || true
      - lacework compliance aws get-report $AWS_ACCOUNT_ID --json --noninteractive > aws-assessment.json
      - cat aws-assessment.json
      - cat aws-assessment.json | jq '.summary[0].num_severity_1_non_compliance'
```

In this buildspec file, we use the Lacework CLI first run an AWS compliance assessment, we get the report and then parse the report for any non-compliance.

Now let's view the results of this phase by clicking on the **Details** link in CodePipeline. This will take us to the AWS CodeBuild build logs.

Scroll down to the end of the log to see the compliance results.

![scan-staging-config-log](/images/scan-staging-config-log.png)

You can also [view the compliance results in the Lacework console](https://laceworkshop.lacework.net/ui/investigation/cloud/ComplianceDashboard).

![compliance-console](/images/compliance-console.png)

***
# Challenge
{{%expand "Why is it important to have a staging environment?" %}} The staging environment is important because it contains the applications and configurations that you intend to deploy to production. This is your last opportunity to check for vulnerabilities and security misconfigurations before you deploy to production. {{% /expand%}}
