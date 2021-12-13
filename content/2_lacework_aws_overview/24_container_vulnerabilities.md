---
title: "Container and Host Vulnerabilities"
chapter: false
draft: false
weight: 24
pre: "<b>2.4 </b>"
---

Lacework provides the ability to assess, identify, and report vulnerabilities found on hosts, containers, registries and pods within your environment. This means you can identify and take action on software vulnerabilities in your environment and manage that risk proactively. 

Lacework continuously assesses vulnerability risks, identifies OS packages, and correlates them with publicly known vulnerabilities with risk ratings by severity and CVSS scores.

In this section, we will explore container vulnerabilities. Lacework several types of container/image scanning as well as providing runtime protection. Lacework provides similar capabilities for hosts such as EC2 instances.
{{% notice info %}}
Lacework provides Public Registry Scanning, Private Registry Scanning, Continuous Integration (CI) Scanning and Local Scanning.
{{% /notice %}}

1. Select **Vulnerabilities > Containers** in the Lacework Console. By default, the page displays **Fixable** and **Active** vulnerabilities.
![Lacework Container Vulnerabilities](/images/lacework-container-vulnerabilities.png)
2. Observe the **Open Vulnerabilities** panel. depicts open vulnerabilities. Hover your mouse over the **Open Vulnerabilities** chart to see the critical, high, medium, and low vulnerabilities.
3. View the **Vulnerabilties List** panel. It shows the list of images with vulnerabilities.
![Lacework Vulnerabilities List](/images/lacework-vulnerabilities-list.png)
4. Click on an image in the list to view the image assessment details.
![Lacework Image Assessment Details](/images/lacework-image-assessment-details.png)
5. View the summary and list of CVEs in the **CVE** tab.
6. Click on the **Details** tab. This provides image details.
7. This image is deployed and is an active container. Scroll down and click on the **Active Containers** link.
8. This Container Dossier provides the details and activity. Scroll down to the **List of Active Containers** panel to see where the container is deployed.
   ![Lacework Active Containers](/images/lacework-active-containers.png)

Lacework's Container Security features enable you to shift your cloud security left into your software delivery process at multiple stages. You can prevent security vulnerabilities from being deployed.
