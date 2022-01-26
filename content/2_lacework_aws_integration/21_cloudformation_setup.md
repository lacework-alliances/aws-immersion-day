---
title: "CloudTrail and AWS Configuration Integration via Console and CloudFormation"
chapter: false
draft: false
weight: 21
pre: "<b>2.1 </b>"
---

The Lacework platform platform at a minimum requires integration with the AWS configuration for an account in order to check security posture of resources. CloudTrail is recommended in order to monitor user, API and resource activity for suspicious behavior. AI/ML are applied to this activity in order to detect anomalous behavior.
![Lacework Cloud Accounts CFN](/images/lacework-cloud-accounts-cfn.png)

1. Navigate to **Settings > Integrations > Cloud Accounts** in your console.
2. Click **+ Create New**.
3. From the Cloud Account drop-down, select **AWS**.
4. From the Type drop-down, select **CloudTrail+Config** or **Config** and click **Next**.
5. Enter a name for the integration and click **Next**.
6. Click on the **RUN CLOUDFORMATION TEMPLATE** to be taken to the CloudFormation console.
7. View the CloudFormation stack parameters, but don't execute in this session.

![Lacework CloudFormation Console](/images/lacework-cloudformation-console.png)