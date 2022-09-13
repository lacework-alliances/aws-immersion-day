---
title: "Multi-Account Onboarding with AWS Control Tower"
chapter: false
draft: false
weight: 22
pre: "<b>2.2 </b>"
---

With Lacework and AWS Control Tower, enrolling a new AWS account now means security best practices and monitoring are automatically applied consistently across your organization. Account administrators can automatically add Lacework's security auditing and monitoring to AWS accounts seamlessly. All the required Lacework and AWS account configurations that allow access to AWS configuration and CloudTrail logs are managed for you by Lacework’s AWS Control Tower integration.

![Lacework Control Tower](/images/lacework-control-tower-diagram.png)

The Lacework AWS Control Tower integration audits and monitors AWS accounts in your AWS Control Tower Landing Zone. Your Landing Zone is your multi-account environment for which you can apply your governance, auditing and monitoring. On initial setup, the Lacework AWS Control Tower integration creates a new cross-account role in the Log Archive account and a new SQS queue is set up in the Audit account. The SQS queue allows Lacework to receive notifications of new audit logs in S3 from the centralized CloudTrail that collects activity from all accounts. Lacework processes these logs for behavior analysis for all AWS accounts.

For new AWS accounts in your organization, AWS Control Tower Account Factory enables easy onboarding of new and existing AWS accounts which triggers the Lacework integration through a new account lifecycle event. A Lambda function launches a stack instance that creates a new cross-account role and allows Lacework to monitor the account via AWS APIs. The combination of CloudTrail log analysis and AWS API access allows Lacework to check your cloud activity and AWS configuration to detect security misconfigurations and anomalous behavior.

![Lacework Control Tower How It Works](/images/lacework-ct-how-it-works.png)

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
