---
title: "Alert Channels and Rules"
chapter: false
draft: false
weight: 27
pre: "<b>2.7 </b>"
---

Lacework combines alert channels and alert rules to provide a flexible method for routing alerts. For alert channels (outgoing integrations), you define information about where to send alerts, such as to Jira or Slack. For alert rules, you define information about which alert types to send, such as critical and high severity compliance alerts. This two-part method provides the flexibility to define multiple channels and multiple rules and then have each rule use the channels you specify.

Lacework provides alert channels for the following:

* Amazon CloudWatch
* Amazon S3 Data Export
* Cisco WebEx
* DataDog
* GCP Pub/Sub
* IBM QRadar
* Jira Cloud
* Jira Server
* Microsoft Teams
* New Relic
* PagerDuty
* ServiceNow
* Slack
* Splunk
* VictorOps
* Webhook

1. Navigate to **Settings > Alert Routing > Alert Channels**.
2. Click **+ Create New**.
![Lacework Alert Channel](/images/lacework-alert-channel.png)
3. Select a **Channel Type** and name the channel.
4. Complete the fields to configure the channel.
5. See each channel's separate help for detailed field information.
6. Click **Save**. The new channel appears in the table. Now the alert channel can be used by an alert rule. An alert rule allows you to choose which resource groups and event categories you want to receive alerts for.
7. Navigate to **Settings > Alert Rules**.
8. Click **+ Create New**.
![Lacework Alert Rule](/images/lacework-alert-rule.png)
9. Select an alert channel for the rule to use. The list displays only enabled configured channels. Add additional channels if appropriate.
10. Name the rule and optionally provide a description.
11. Select the severities that you want the rule to apply to.
12. Select the resource groups that you want the rule to apply to.
13. Select the event categories that you want the rule to apply to. If you do not select any categories, the rule applies to all event categories.
14. Click **Save**. The new rule appears in the table.

Alert channel and rules provide a way to send Lacework security events to other tools. Lacework can integrate into your organization's security operations workflow and tools.