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

1. Click on this [CloudTrail Dossier](https://laceworkshop.lacework.net/ui/home?dossierTemplate=CloudTrailDossier&filters=eyJzdGFydFRpbWUiOjE2NTM0Mjk2MDAwMDAsImVuZFRpbWUiOjE2NTM0MzMyMDAwMDAsImZpbHRlcnMiOnsiQ2xvdWRUcmFpbEZpbHRlcnMuQVdTX1VTRVJOQU1FIjp7ImluY2x1ZGVzIjpbIklBTVVzZXIvOTExMjkwNzE2NDMwOmJhZGd1eSJdfX19&params=eyJkb3NzaWVyVGVtcGxhdGUiOiJDbG91ZFRyYWlsRG9zc2llciIsImRpc3BsYXlOYW1lIjoic3JjX3VzZXJuYW1lIiwiZGlzcGxheVZhbHVlIjoiSUFNVXNlci85MTEyOTA3MTY0MzA6YmFkZ3V5Iiwia2V5cyI6eyJmaWx0ZXJzIjpbeyJmaWVsZCI6IkNsb3VkVHJhaWxGaWx0ZXJzLkFXU19VU0VSTkFNRSIsInZhbHVlIjoiSUFNVXNlci85MTEyOTA3MTY0MzA6YmFkZ3V5IiwidHlwZSI6ImVxIn1dfX0=&ci=LACEWORK_C589473C94849FA7EEEE1C5F4C888811610291125E817EC) 
      that represents malicious activity from an AWS user _badguy_.
   {{% notice info %}} 
      Anomaly events are detected through Lacework's Polygraph machine learning technology. Polygraph tracks the user and API activities and detects anomalous and potentially malicious behavior. 
   {{% /notice %}}
2. Scroll down to the Polygraph to see a visual representation of the API interactions.
   ![Badguy Polygraph](/images/badguy-polygraph.png)
3. Scroll back to the top and click on the **Details** icon on the event. This will take you to the Event Dossier and provide more detail.
4. Expand the **MORE DETAIL** link for the _WHO_, _WHAT_ and _WHERE_.
   ![Lacework event dossier](/images/anom-lacework-event-dossier.png)
5. API Calls to s3:ListBuckets along with a kms:GenerateDataKey shows the user searching S3 buckets and then initiating a large KMS encryption task.

