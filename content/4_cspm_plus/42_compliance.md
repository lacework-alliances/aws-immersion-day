---
title: "Cloud Security Compliance"
chapter: false
draft: false
weight: 42
pre: "<b>4.2 </b>"
---

Lacework’s AWS security platform automatically validates all configurations against the controls established as best practices for securing your cloud environment. The first step in preventing an attack is secure your cloud configuration. Lacework monitors your AWS environments and notifies you of security misconfigurations.

![Lacework Dashboard Alerts](/images/ransom-cloud-compliance.png)

1. Go to **Compliance > Cloud** in the Lacework Console to display the Compliance page.
2. Choose the **Group by Policy**.
3. Then for **Service Category** filter choose S3.
4. Click on **LW_S3_2 Ensure the S3 bucket ACL does not grant 'Everyone' WRITE permission [create, overwrite, and delete S3 objects]**. This is a critical severity recommendation and lists S3 buckets that are vulnerable.
   ![Lacework Dashboard Alerts](/images/s3-policy-write.png)
   The noncompliance s3 buckets are identified.
5. Click on the **View context** link to view the steps to resolve the noncompliance.
   ![Lacework Dashboard Alerts](/images/s3-context.png)
6. Click on **LW_S3_16 Ensure the S3 bucket has versioning enabled**. Versioning is a recommendation to protect yourself from ransomware attacks. This lists S3 buckets that should have versioning enabled.
   ![Lacework Dashboard Alerts](/images/s3-versioning.png)

Lacework provides security recommendations for your cloud environments. These can help you prevent attacks before they happen. Let's see how these generate events to notify you of issues that you should address.

***
# Challenge
{{%expand "If you don't know how to remediate, how could you learn how? " %}} Use the Additional Info link on the recommendation to find the steps to remediate. {{% /expand%}}
