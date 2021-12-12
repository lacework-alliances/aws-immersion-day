---
title: "Anatomy of the Attack"
chapter: false
draft: false
weight: 41
pre: "<b>4.1 </b>"
---



![anatomy attack](/images/anatomy-attack.png)

In this scenario, we simulate the typical ransomware actions where an attacker gains access to sensitive data.

1. An attacker gains access to a bastion host that is exposed to the internet.
2. From the bastion host, the attacker scans for s3 buckets (using the preinstalled AWS CLI).
3. The attacker discovers an S3 bucket with sensitive documents.
4. The attacker uses encryption keys to encrypt the documents.