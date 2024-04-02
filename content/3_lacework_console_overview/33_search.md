---
title: "Search"
chapter: false
draft: false
weight: 33
pre: "<b>3.3 </b>"
---

In the Discovery left navigation section of the Lacework Console, Lacework lets you perform a global search of assets known to Lacework.

![Lacework Search](/images/search.png)

To start a search, click **Search** and enter text in the search bar. Constrain the search using any of the available filters.

Lacework returns results when the search finds any assets that match the entered string, within the following time constraints:

* Alerts created in the last 180 days.
* Networks, Kubernetes clusters, pods, and namespaces accessed in the last 7 days.
* All other assets created or accessed in the last 30 days.

***
# Challenge
{{%expand "Use Search to locate the user 'ec2-user'. How many alerts are related to this user?" %}} Actual number may vary. {{% /expand%}}
