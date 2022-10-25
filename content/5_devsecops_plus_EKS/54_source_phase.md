---
title: "Source Phase"
chapter: false
weight: 54
pre: "<b>5.4 </b>"
---

The Source phase use a Codepipeline source action to pull our code from a zipped archive in an S3 bucket. This zipped archive contains our source code, K8s manifests and CodeBuild buildspec files. Other source options are also available such as
Github and Bitbucket are available through [Codestar Connections](https://docs.aws.amazon.com/codepipeline/latest/userguide/action-reference-CodestarConnectionSource.html).

![S3 source](/images/aws-s3-source.png)


The Cloudformation specification of source from a S3 zipped archive for our workshop:
```yaml
      Stages:
        - Name: Source
          Actions:
            - Name: App
              ActionTypeId:
                Category: Source
                Owner: AWS
                Version: 1
                Provider: S3
              Configuration:
                S3Bucket: !Sub "${AWS::AccountId}-app-bucket-${LaceworkAccountName}"
                S3ObjectKey: !Sub "${S3KeyPrefix}/app/app.zip"
                PollForSourceChanges: false
              OutputArtifacts:
                - Name: App
              RunOrder: 1
```

A Github source using AWS Codestar connections:

```yaml
      Stages:
        - Name: Source
          Actions:
            - Name: GitHubRepo
              ActionTypeId:
                Category: Source
                Owner: AWS
                Provider: CodeStarSourceConnection
                Version: 1
              Configuration:
                ConnectionArn: arn:aws:codestar-connections:us-west-2:911290716430:connection/baf6fdba-995f-4e59-8497-49c224c3479b
                FullRepositoryId: lacework-alliances/aws-secured-pipeline
                BranchName: master
              OutputArtifacts:
                - Name: App
              RunOrder: 1
```

Codestar connections for other source code repositories can be created from **Settings > Connections**.

![Codestar connections](/images/codestar-connections.png)

![Codestar connection create](/images/codestar-connection-create.png)

***
# Challenge
{{%expand "Can you simultaneously create a Codestar connection and use it in your AWS CloudFormation?" %}} Unfortunately not. The Codestar connection must be created in the AWS console. The process involves authenticating with the source code provider (like GitHub) and setting up the webhook for commit notifications. But you just need to do this once for an organization and not for every repository. {{% /expand%}}


