---
title: "Agentless Workload Scanning"
chapter: false
draft: false
weight: 24
pre: "<b>2.4 </b>"
---

Agentless workload scanning enables you to quickly gain comprehensive visibility into vulnerability risks and secrets across your cloud workloads — without the need to install agents. With this option, you have more flexibility and choice to scan and detect vulnerabilities and secrets across all hosts and container images to meet your coverage needs.

Lacework's agentless scanning technology is designed to be private by design. Snapshots are created in a customer account and then shared / copied to a customer managed cloud account. The data in the snapshot does not leave the customer environment.

What access does Lacework have? The only access Lacework has is to the S3 bucket where the scan results (meta-data only) have been written to. Lacework does NOT have access to the raw snapshot or data.

![Agentless Private By Design](/images/agentless-private-by-design.png)

