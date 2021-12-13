---
title: "Cloud Security Compliance"
chapter: false
draft: false
weight: 42
pre: "<b>4.2 </b>"
---

Lacework’s AWS security platform automatically validates all configurations against the controls established as best practices for securing your cloud environment. The first step in preventing an attack is secure your cloud configuration. Lacework monitors your AWS environments and notifies you of security misconfigurations.

1. Go to **Compliance > AWS > Reports** in the Lacework Console to display the AWS Compliance Reports page. The AWS CIS Benchmark and S3 Report provides S3 configuration validation.
![Lacework CIS S3](/images/lacework-cis-benchmark-s3.png)
2. Scroll down the list to view the S3 recommendations and status. View the **Non-Compliant** and **Compliant** recommendations as well as severity.
![Lacework S3 Recommendations](/images/lacework-s3-recommendations.png)
3. Click on **LW_S3_2 Ensure the S3 bucket ACL does not grant 'Everyone' WRITE permission [create, overwrite, and delete S3 objects]**. This is a critical severity recommendation and lists S3 buckets that are vulnerable.
4. Click on **LW_S3_16 Ensure the S3 bucket has versioning enabled**. Versioning is a recommendation to protect yourself from ransomware attacks. This lists S3 buckets that should have versioning enabled. 

Lacework provides security recommendations for your cloud environments. These can help you prevent attacks before they happen. Let's see how these generate events to notify you of issues that you should address.