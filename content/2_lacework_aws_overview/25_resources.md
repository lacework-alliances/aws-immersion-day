---
title: "Resources"
chapter: false
draft: false
weight: 25
pre: "<b>2.5 </b>"
---

The Lacework Console provides visibility into AWS resources that are integrated with Lacework. A resource can be any entity within the cloud deployment, such as an S3 bucket, security group, or EC2 instance. The Resource Inventory page allows you to view and monitor in-use AWS resources’ risk, compliance, and configuration changes and provides visibility for team members with limited or no access to the AWS Management Console. Because Lacework takes regular snapshots of your resources, you can track their changes (diffs) through the Lacework Console.

1. Go to **Resources > Cloud > AWS CloudTrail** in the Lacework Console. Lacework analyzes the use and API activity from AWS CloudTrail logs.
![Lacework CloudTrail](/images/lacework-cloudtrail.png)
2. View the **Timeline** panel on the right to observe anomalous events detected from the CloudTrail activity.
![Lacework Anomalous Events](/images/lacework-anomalous-events.png)
3. Scroll down to the **Polygraph** panel. Lacework's Patented Polygraph feature graphs your user and API activity and enables you to see the sequence of behaviors. Additionally, anomalous behavior is flagged and highlighted as RED.
![Lacework Polygraph](/images/lacework-polygraph.png)
4. Use the **Search** field to filter the Polygraph on services, resources API calls, accounts, users and responses.
5. Use the **DIFF** button on the right to compare the current Polygraph snapshot to the previous (1 hour). This helps you understand the changes that have occurred.
![Lacework Polygraph Diff](/images/lacework-polygraph-diff.png)
6. Go to **Resources > Cloud > Inventory**. The Resource Inventory page allows you to view and monitor in-use AWS resources’ risk, compliance, and configuration changes.
![Lacework Resource Inventory](/images/lacework-resource-inventory.png)
7. Click on a resource to view the resource configuration details. When a diff is present, it is always compared to the current configuration. If more than two configuration histories exist, click **View more** to display the **Configuration History** page.
![Lacework Resource Config Detail](/images/lacework-resource-config-detail.png)

Lacework inventories all of your cloud resources and tracks their configuration changes. This can help you determine if recent configuration changes are the source of issues.