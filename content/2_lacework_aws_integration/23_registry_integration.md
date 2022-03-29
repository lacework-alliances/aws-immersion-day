---
title: "Container Registry Integration"
chapter: false
draft: false
weight: 23
pre: "<b>2.3 </b>"
---

If your development teams are doing microservices development and delivering container images, Lacework can be enabled to scan your
images for software vulnerabilities. Lacework can scan OS and software packages and alert you to vulnerabilities. 
Lacework supports the most popular container registries including Amazon Elastic Container Registry (ECR). 

![Lacework Integrates AWS ECR](/images/lacework-integrates-aws-ecr.png)

Lacework also has a proxy scanner which allows Lacework to perform container vulnerability assessments for your on-premises Docker container 
image registries without exposing them to external connectivity. You can learn more about the Lacework Proxy Scanner [here](https://docs.lacework.com/integrate-proxy-scanner).

1. Navigate to **Settings > Integrations > Container Registries**.
   ![Lacework Container Registries](/images/lacework-container-registries.png)
2. Click **+ Add New**.
3. Select a registry type.
   ![Lacework Container Registries](/images/lacework-container-registry-type.png)
4. Select the registry integration type and click **Next**.
5. Complete any settings and click **Save**.

![Lacework Container Registries](/images/lacework-container-registry-save.png)