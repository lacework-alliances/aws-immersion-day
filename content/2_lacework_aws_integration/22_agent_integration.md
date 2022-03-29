---
title: "Agent Integration"
chapter: false
draft: false
weight: 22
pre: "<b>2.2 </b>"
---

For hosts, container services and Kubernetes, optional agents can be installed to enable security monitoring at the edge of the cloud. Lacework agents are lightweight and send network and process telemetry for security analysis. Lacework agents are supported on most x86, ARM and container runtimes. The Lacework Agent also supports AWS Graviton processors and is **AWS Graviton Ready**.
![Lacework Integrates AWS Agent](/images/lacework-integrates-aws-agent.png)
Deploying an agent requires an agent access token and using the installation method that is appropriate for your environment.

1. In the Lacework Console, navigate to **Settings > Configuration > Agents**.
   ![Lacework Agents](/images/lacework-agents.png)
2. Click **+ Add New**.
3. In the **Name** field, enter a unique logical name for the agent token. You can use the agent access token name to logically separate your deployments, for example, by environment types (QA, Dev, etc.) or system types (CentOS, RHEL, etc.).
4. In the **Description** field, you can optionally specify a description.
5. Click **Save**.
6. Click on the **... > Install** link to see the deployment options.

![Lacework Agent Installation](/images/lacework-agent-install-options.png)