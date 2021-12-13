---
title: "AWS Compliance"
chapter: false
draft: false
weight: 23
pre: "<b>2.3 </b>"
---

Lacework’s AWS security platform automatically validates all configurations against the controls established as best practices for securing your cloud environment. Our interactive reports deliver insights into “passed or failed” controls with recommendations on how to fix out-of-compliance configuration components.

1. Navigate to the Compliance Dashboard page in the Lacework Console, select **Compliance > AWS > Dashboard**. This dashboard provides a view of your AWS accounts that are integrated with Lacework and their related compliance information and details.
![Lacework AWS Compliance Dashbaord](/images/lacework-aws-compliance-dashboard.png)
2. Use the account drop-down to limit the results displayed in the dashboard to a single specific account or for all accounts. The account drop-down is located in the top middle of the panel and defaults to **All Accounts**. The first panel is an at-a-glance Compliance Summary that displays the following:
   * number of accounts analyzed
   * number of resources monitored
   * percentage of resources in violation
   * count of resources in violation
   * number of critical CIS benchmark recommendations in violation
   * number of critical S3 recommendations in violation
3. View a breakdown by section, click the percentage or count of resources in violation in the middle-subpanel. A breakdown of resources in violation are displayed and grouped by the following sections:
   * IAM
   * LOGGING
   * MONITORING
   * NETWORKING
   * S3
   * GENERAL SECURITY
   * ELASTIC SEARCH
4. View the Account Summary panel. It displays an account summary table that provides details about the AWS accounts integrated into Lacework that are in violation. Under Status, the current status of the integration between Lacework and the listed AWS account is displayed.
   * Enabled—The integration between Lacework and the listed AWS account is active.
   * Deleted—At one point, the integration between Lacework and the listed AWS account was active but now that integration has been deleted.
   * Disabled—The integration between Lacework and the listed AWS account has been disabled.
   * Integration Failed—Lacework encountered a problem while attempting to use the integration between Lacework and the AWS account, for example, maybe the correct privileges have not been granted.
5. View the CIS Benchmark Overview and S3 Overview Panels. These panels display an aggregation of data for the selected account(s) correlating to the policy/rules in the associated compliance benchmarks. Details such as severity, recommendation, service, and number/percentage of resources in violation are displayed.
![Lacework CIS S3](/images/lacework-cis-benchmark-s3.png)
6. The top five recommendations are displayed by default. To see all the recommendations sorted by severity, click **View number More Recommendation**.
7. To view additional details about a recommendation, hover over a recommendation row until **View Details DETAILS** displays and click **View Details**.
8. Go to **Compliance > AWS > Reports** in the Lacework Console to display the AWS Compliance Reports page. Lacework provides the following compliance reports for your cloud environments.
   * AWS CIS Benchmark and S3 Report
   * AWS HIPAA Report
   * AWS ISO 27001:2013 Report
   * AWS NIST 800-171 Report
   * AWS NIST 800-53 Report
   * AWS PCI DSS Report
   * AWS SOC 2 Report
   * AWS SOC 2 Report Rev2
![Lacework CIS S3](/images/lacework-aws-compliance-report.png)
9. Use the **Report Type** pull-down to view these reports. Each report provides a summary of non-compliance with severity. Additionally, each report provides a list of recommendations and their status.
![Lacework CIS S3](/images/lacework-compliance-recommendations.png)
10. Go to **Compliance > AWS > Summary** to see an overall summary of compliance across all report types, events, services and resources.

Lacework compliance reports enable you to quickly validate your cloud configurations for vulnerabilities. Default reports allow you to immediately check configuration.