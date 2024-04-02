---
title: "Identities"
chapter: false
draft: false
weight: 39
pre: "<b>3.9 </b>"
---

![Lacework Identities](/images/lacework-identities.png)

Identities play an increasingly important role in securing cloud resources and data. Traditional wisdom calls for a least privileged approach to granting access, which means only giving users the permissions they need to perform their jobs. However, approaching this end state is far more complex for cloud-native applications.

Cloud users and entities are typically over-permissioned, with the intention of right-sizing access at a future date. However, this rarely happens. Excess entitlements, dormant identities, and toxic combinations leave organizations highly exposed to cloud breach, account takeover, and data exfiltration.

Lacework’s Identities feature provides a comprehensive view of all identities across your cloud environment. It identifies over-permissioned users, dormant identities, and toxic combinations, and provides actionable insights to remediate these risks.

Lacework provides security teams with the visibility and context to understand their cloud identity architectures and right-size cloud permissions to achieve least privilege goals. Comprehensive Lacework-provided visibility lets you:

* Show all identities - Lacework continuously discovers cloud identities and their associated entitlements dynamically to provide a full and always up-to-date inventory of cloud users, resources, groups, and roles.
* Know precisely who can perform which actions to identify overly permissive identities - Lacework continuously ingests event data from cloud services to determine all of the actions an identity has taken over a given time period.
* Prioritize the greatest risks - Lacework calculates a risk score for each identity based on multiple factors.
* Scope down permissions accordingly to reduce risk - Lacework automatically generates suggested changes for right-sizing permission artifacts.

1. Click on the **Top identity risks** tab to view the top identity risks.
2. View one of the top identity risks to see the details.
   ![Lacework Identities](/images/lacework-identities-detail.png)
3. Click the **Investigate** button to investigate the identity risk.