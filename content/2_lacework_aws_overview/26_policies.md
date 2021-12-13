---
title: "Policies"
chapter: false
draft: false
weight: 26
pre: "<b>2.6 </b>"
---

Lacework policies provide a framework for validating configuration and behavior in your cloud environment. Lacework provides a set of predefined default policies that are visible from the Lacework Console. You can use the default policies to suppress the generation of unwanted alerts in your environment. Default policy IDs start with the LW_ prefix. You may want to create custom policies that check for unwanted behavior in your environment such as Telnet being used in your environment. You can also customize the triggers and severities for custom policies. Custom policy IDs start with the CUSTOM_ prefix.

1. Go to **Policies** in the Lacework Console. The Policies page displays all policies. It provides a summary and list of all of your default and custom policies. You can use the following methods to refine the list of displayed policies:
   * Use filters to display a subset of specific policies. Click filters along the top of the page to display only the desired policies. Or click the filter icon and select the filters you want to display.
* Use the search function at the top of the page to find specific text in the policy name or ID.
![Lacework Policies](/images/lacework-policies.png)
{{% notice info %}}
When the page displays your desired policies after filtering, you can save the current view by clicking the **Save view** icon in the top right corner. This allows you to access the saved view later through the **Open view** icon.
{{% /notice %}}
2. Scroll through the list of policies. You can disable or enable each policy directly from the policies list. Mousing over a policy displays icons for any available actions such as clone or delete. You can also click a policy to clone it (create a custom policy) or edit a custom policy's queries and parameters.
3. Click a policy to display its details. The **Summary** tab lists details of the policy.
![Lacework Policy Summary](/images/lacework-policy-summary.png)
4. Click on the **Query** detail to view the policy query that is used for validation.
![Lacework Policy Query](/images/lacework-policy-query.png)
5. To create a custom policy, clone an existing policy first. Update the name, summary details and query.
![Lacework Custom Policy](/images/lacework-custom-policy.png)
{{% notice info %}}
For custom policy queries, Lacework allows simple comparison expressions that are created in the console. Learn more about the types of expressions that you can use [here](https://docs.lacework.com/create-policies#create-a-custom-policy).
{{% /notice %}}

Lacework default policies enable out-of-the-box security validation of your AWS environments. But not every organization is the same and custom policies are a great way to add validation specific to your organization's requirements.