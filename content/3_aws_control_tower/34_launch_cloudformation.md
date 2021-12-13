---
title: "Launch the AWS CloudFormation Template"
chapter: false
draft: false
weight: 34
pre: "<b>3.4 </b>"
---

The Lacework AWS Control Tower integration uses CloudFormation to install StackSets, IAM roles, Lambda functions and SQS queues that support the integration. Follow the next steps to install the integration through your AWS CloudFormation console.

1. Login in to AWS master account with Administrator permissions.
2. Select the AWS region where your AWS Control Tower is deployed.
3. Click on the following Launch Stack button to go to your CloudFormation console and launch the AWS Control Integration template.
<a href="https://console.aws.amazon.com/cloudformation/home?#/stacks/create/review?templateURL=https://lacework-alliances.s3.us-west-2.amazonaws.com/lacework-control-tower-cfn/templates/control-tower-integration.template.yml"><img src="https://dmhnzl5mp9mj6.cloudfront.net/application-management_awsblog/images/cloudformation-launch-stack.png"></img></a>
For most deployments, you only need the **Basic Configuration** parameters. Use the **Advanced Configuration** for customization.
![cloudformation-basic-configuration.png](/images/lacework-ct-basic-configuration.png)
4. Specify the following **Basic Configuration** parameters:
    * Enter a **Stack name** for the stack.
    * Enter **Your Lacework URL**.
    * Enter your **Lacework Sub-Account Name** if you are using Lacework Organizations.
    * Enter your **Lacework Access Key ID** and **Secret Key** that you copied from your previous API Keys file.
    * For **Capability Type**, the recommendation is to use **CloudTrail+Config** for the best capabilities.
    * Choose whether you want to **Monitor Existing Accounts**. This will set up monitoring of ACTIVE existing AWS accounts.
    * Enter the name of your **Existing AWS Control Tower CloudTrail Name**.
    * If your CloudTrail S3 logs are encrypted, specify the **KMS Key Identifier ARN**.
    * Update the Control Tower **Log Account Name** and **Audit Account Name** if necessary.
5. Click **Next** through to your stack **Review**.
6. Accept the AWS CloudFormation terms and click **Create stack**.
7. Monitor the progress of the CloudFormation deployment. It takes several minutes for the stack to create the resources that enable the Lacework AWS Control Tower Integration.
8. When successfully completed, the stack shows **CREATE_COMPLETE**.
