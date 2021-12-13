---
title: "How It Works"
chapter: false
draft: false
weight: 31
pre: "<b>3.1 </b>"
---

The Lacework AWS Control Tower integration audits and monitors AWS accounts in your AWS Control Tower Landing Zone. Your Landing Zone is your multi-account environment for which you can apply your governance, auditing and monitoring. On initial setup, the Lacework AWS Control Tower integration creates a new cross-account role in the Log Archive account and a new SQS queue is set up in the Audit account. The SQS queue allows Lacework to receive notifications of new audit logs in S3 from the centralized CloudTrail that collects activity from all accounts. Lacework processes these logs for behavior analysis for all AWS accounts.

For new AWS accounts in your organization, AWS Control Tower Account Factory enables easy onboarding of new and existing AWS accounts which triggers the Lacework integration through a new account lifecycle event. A Lambda function launches a stack instance that creates a new cross-account role and allows Lacework to monitor the account via AWS APIs. The combination of CloudTrail log analysis and AWS API access allows Lacework to check your cloud activity and AWS configuration to detect security misconfigurations and anomalous behavior.

![Lacework Control Tower How It Works](/images/lacework-ct-how-it-works.png)

## Setup Flow
1. The Administrator applies Lacework's main Control Tower Integration template in Cloudformation for the initial setup.
2. This template provisions all resources which includes a stack set, roles & permissions, Lambda functions, SQS queues and EventBridge rule.
3. Via LaceworkSetupFunction Lambda, a new cross-account role is set up in the Log Archive account and a new SQS queue is set up in the Audit account. The SQS queue allows Lacework to receive notifications of new audit logs in S3 from the centralized CloudTrail that collects activity from all accounts. Lacework processes these logs for behavior analysis for all AWS accounts.
4. The LaceworkSetupFunction acquires the initial Lacework access token.
5. The LaceworkSetupFunction provisions any existing ACTIVE AWS accounts by sending an SNS message to the StackSet Lambda Function if specified with the Monitor Existing Accounts option.
6. The LaceworkAccountFunction Lambda creates a new Stack instance(s) for the account(s).
7. The Stack instance creates a new cross-account role and allows Lacework to monitor the account via AWS APIs.
8. The Stack instance notifies Lacework of the new account through an SNS custom resource notification, LaceworkSNSCustomResource. The account is created in Lacework.
9. A scheduled event rule periodically triggers the LaceworkAuthFunction Lambda to acquire a temporary access token from Lacework.

## New Account Flow
1. A new AWS account triggers a Control Tower lifecycle event which is picked up by the EventBridge rule.
2. The EventBridge rule triggers the LaceworkAccountFunction Lambda to create a new Stack instance for the account.
3. The LaceworkAccountFunction Lambda creates a new Stack instance(s) for the account(s).
4. The Stack instance creates a new cross-account role and allows Lacework to monitor the account via AWS APIs.
5. The Stack instance notifies Lacework of the new account through an SNS custom resource notification, LaceworkSNSCustomResource. This sends an SNS notification to Lacework and the account is created in Lacework’s platform.