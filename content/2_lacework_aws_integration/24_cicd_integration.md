---
title: "CI/CD Integration"
chapter: false
draft: false
weight: 24
pre: "<b>2.4 </b>"
---

With Lacework, you can also discover software vulnerabilities during your software build process. This is done through use 
of the Lacework inline scanner. The Lacework inline scanner can be integrated with many CI/CD tools including AWS CodePipeline and CodeBuild.
You can see AWS CodePipeline and CodeBuild examples in the DevSecOps modules. Similar to the container registry scanning, the inline scanner
can detect software vulnerabilities in OS and software packages.The inline scanner is configured in the Container Registries settings menu:

1. Navigate to **Settings > Integrations > Container Registries**.
2. Click **+ Create New**.
3. From the **Registry** Type drop-down, select **Inline Scanner** and click **Next**.
4. Name the integration and click **Next**.
5. Complete any optional settings and click **Save**.
6. This displays a window that provides the inline scanner’s download URL and authorization token.
7. Click the **Authorization Token**’s Copy to clipboard icon. This is the integration’s associated token. You need this to configure the inline scanner.

Examples of how to integrate the inline scanner with the following CI/CD tools are available:

* [Jenkins](https://docs.lacework.com/integrate-the-lacework-inline-scanner-with-ci-pipelines#integrate-with-jenkins)
* [TravisCI](https://docs.lacework.com/integrate-the-lacework-inline-scanner-with-ci-pipelines#integrate-with-travisci)
* [GitHub Actions](https://docs.lacework.com/integrate-the-lacework-inline-scanner-with-ci-pipelines#integrate-with-github-actions)
* [Bitbucket Pipelines](https://docs.lacework.com/integrate-the-lacework-inline-scanner-with-ci-pipelines#integrate-with-bitbucket-pipelines)