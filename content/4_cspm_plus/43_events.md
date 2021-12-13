---
title: "Lacework Security Events"
chapter: false
draft: false
weight: 43
pre: "<b>4.3 </b>"
---

You don't need to continually monitor your compliance reports for issues in your cloud configuration. Lacework notifies you through security events that gather all of the security context that you need to perform a quick investigation.

1. Go to **Events** in your Lacework Console. The *Events** page displays a timeline of security events and allows you to filter on various attributes including severity.
![Lacework Events](/images/lacework-events.png)
2. Notice that the **LW_S3_16 Ensure the S3 bucket has versioning enabled** security event is present. We saw that this was out of compliance and a security event was generated.
![Lacework S3 Versioning](/images/lacework-s3-versioning.png)
3. Click on this event to see the event summary. This shows you when the event occurred and for which AWS account.
![Lacework event summary](/images/lacework-event-summary.png)
4. Click on the **Details** icon on the event. This will take you to the Event Dossier and provide more detail. It provides the Why, What and When for your security investigation.
![Lacework event dossier](/images/lacework-event-dossier.png)
5. Expand the **MORE DETAIL** link. This shows you the S3 buckets in violation and the new violations.
![Lacework event dossier more detail](/images/lacework-event-dossier-more-detail.png)
6. Scroll further down to see the related events. These are events that are also associated with the resource(s).
![Lacework event dossier related events](/images/lacework-related-events.png)

Lacework events alert you to security issues and provide you the important details for your investigation. Security context details like Why, What and When enable you to quickly resolve the issue.