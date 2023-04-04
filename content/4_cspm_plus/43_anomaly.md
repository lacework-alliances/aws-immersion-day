---
title: "The Lacework Anomaly Detection"
chapter: false
draft: false
weight: 43
pre: "<b>4.3 </b>"
---

In the previous sections, we looked at prevention - identifying issues that make you vulnerable to an attack. Now we will look at Lacework's anomaly detection events with Polygraph. The Lacework Polygraph analyzes an array of cloud factors to detect breaches. There are currently six Lacework polygraph analysis groups:

* Application/process communications
* Application launches
* Machine communications
* Machine servers
* Privilege changes
* Insider behaviors

1. Click on this [CloudTrail Dossier](https://laceworkshop.lacework.net/ui/investigation/monitor/AlertInbox/11910/investigation?filter=severity%3ACritical+severity%3AHigh+severity%3AMedium&sort=START_TIME%3Adescending&timeRange=start%3A2023-04-03T04%3A11%3A00.000Z+end%3A2023-04-04T04%3A11%3A00.000Z) 
      that represents malicious activity from an AWS user _ec2-user_.
      Anomaly events are detected through Lacework's Polygraph machine learning technology. Polygraph tracks the user and API activities and detects anomalous and potentially malicious behavior.
2. Scroll down to the Polygraph to see a visual representation of the API interactions.
   ![Badguy Polygraph](/images/badguy-polygraph.png)
3. Hover over _ec2-user_ to and click on the _ec2-user_ link to take us to the user's activity.
![Badguy Polygraph](/images/ec2-user-polygraph.png)
4. Scroll down to the _Unique Process Details_ to see what ec2-user was doing.
   ![Badguy Polygraph](/images/ec2-user-process-details.png)

Lacework's anomaly detection can uncover suspicious activity that may be indicative of a breach. This is a powerful tool for identifying anomalous behavior and can help you quickly identify and respond to threats.

