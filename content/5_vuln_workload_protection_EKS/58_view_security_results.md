---
title: "View Security Results in Lacework"
chapter: false
weight: 58
pre: "<b>5.8 </b>"
---

1. Go to **Vulnerabilities > Containers** in the Lacework Console.
2. View the images for _demo-app_ and _log4j-app_.
3. Notice the severity of the CVEs for each image.
4. Click on the row to access the CVE list and details.
   ![log4j-cves](/images/log4j-cves.png)
5. On the details tab, click on Active Containers. This indicates that this image with vulnerabilities is in active containers.
   ![log4j-details](/images/log4j-details.png)
6. Scroll down to List of Active Containers to see the location of the vulnerable active containers.
