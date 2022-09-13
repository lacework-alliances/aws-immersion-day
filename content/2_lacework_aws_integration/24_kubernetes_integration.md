---
title: "EKS (Kubernetes) Control Plane Integration"
chapter: false
draft: false
weight: 24
pre: "<b>2.4 </b>"
---

All Kubernetes activities, whether manual activities with the kubectl tool, or automated, results in one or more API calls to the Kubernetes API server. Lacework can ingest these events to monitor activities, including kubectl exec, port-forwarding, deployment of new resources such as workloads, Kubernetes roles and role bindings, deletion of resources, authentication issues, forbidden API calls, and more. The Lacework Polygraph Data Platform surface the most important events such as the execution of rogue containers, the deployment of misconfigured workloads, the addition of dangerous roles, or manual login to containers.

![Lacework Integrates EKS Control Plane](/images/lacework-integrates-eks-cp.png)

1. Navigate to **Settings > Integrations > Cloud Accounts** in your console.
2. Click **+ Add New**.
3. Select **AWS**.
4. Select **EKS Audit Log** and click **Next**.
5. Select **CloudFormation**.
6. Click on the **Run CloudFormation Template** to be taken to the CloudFormation console.
   ![Lacework Cloud Accounts CFN](/images/lacework-cloud-accounts-eks-cp.png)
7. View the CloudFormation stack parameters, but don't execute in this session.

![Lacework CloudFormation Console](/images/lacework-eks-cloudformation-console.png)