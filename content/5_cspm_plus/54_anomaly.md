---
title: "The Lacework Anomaly Detection"
chapter: false
draft: false
weight: 53
pre: "<b>5.3 </b>"
---

In the previous sections, we looked at prevention - identifying issues that make you vulnerable to an attack. Now we will look at Lacework's anomaly detection events with Polygraph. The Lacework Polygraph analyzes an array of cloud factors to detect breaches. There are currently six Lacework polygraph analysis groups:

* Application/process communications
* Application launches
* Machine communications
* Machine servers
* Privilege changes
* Insider behaviors

1. Go to **Events** in your Lacework Console.
2. In the **Timeline**, filter on the **Last 7 days** and **Anomalies**. This filters on anomaly events.
![Lacework Events Anomalies](/images/lacework-events-anomalies.png)
{{% notice info %}}
Anomaly events are detected through Lacework's Polygraph machine learning technology. Polygraph tracks the user and API activities and detects anomalous and potentially malicious behavior.
{{% /notice %}}
3. Find the event **New AWS User** with name _badguy_. This is event ID 184. You can also use the **Search** field.
4. Click on this event to see the event summary. This shows you when the event occurred and for which AWS account.
   ![Lacework event summary](/images/anom-lacework-event-summary.png)
5. Click on the **Details** icon on the event. This will take you to the Event Dossier and provide more detail. 
   ![Lacework event dossier](/images/anom-lacework-event-dossier.png)
6. Expand the **MORE DETAIL** link. 
7. API Calls to s3:ListBuckets along with a kms:GenerateDataKey shows the user searching S3 buckets and then initiating a large KMS encryption task.
