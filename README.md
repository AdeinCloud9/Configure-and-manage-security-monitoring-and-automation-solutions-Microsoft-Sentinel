# Configure-and-manage-security-monitoring-and-automation-solutions-Microsoft-Sentinel

This repository contains the steps and resources for implementing Microsoft Sentinel as part of my lab exercise.

## Objectives
- On-board Microsoft Sentinel to a Log Analytics workspace.
- Configure Microsoft Sentinel to use the Azure Activity data connector.
- Create rules and playbooks for automated incident responses.
- Invoke and review incidents in Microsoft Sentinel.

## Skills Learned
- Configuring Microsoft Sentinel and Log Analytics workspaces.
- Using Azure Policy Assignment wizard for data connector configuration.
- Creating and managing security rules and playbooks in Microsoft Sentinel.
- Automating incident responses and reviewing security incidents.

## Tools Used
- Microsoft Sentinel
- Azure Portal
- Log Analytics
- Azure Policy Assignment wizard
- Azure Activity data connector

# Microsoft Sentinel Lab Instructions

### Task 1: On-board Microsoft Sentinel
1. I signed in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).
2. In the search box, I typed `Microsoft Sentinel` and pressed Enter.
3. I selected `Microsoft Sentinel` from the services list and clicked `+ Create`.
4. I added Microsoft Sentinel to a Log Analytics workspace.

### Task 2: Configure Microsoft Sentinel to use the Azure Activity Data Connector
1. I navigated to the `Content hub` in Microsoft Sentinel.
2. I searched for `Azure Activity` and installed the connector.
3. I followed the steps to configure the connector using the Azure Policy Assignment wizard.

### Task 3: Create a Rule using the Azure Activity Data Connector
1. I went to `Analytics` in Microsoft Sentinel.
2. I clicked the `Rule templates` tab and searched for `Suspicious`.
3. I selected the `Suspicious number of resource creation or deployment` template and created the rule.

### Task 4: Create a Playbook
1. In the Azure portal, I searched for `Deploy a custom template`.
2. I loaded the `changeincidentseverity.json` file from the `json` directory.
3. I followed the steps to configure and save the playbook.

### Task 5: Create a Custom Alert and Configure the Playbook as an Automated Response
1. I created a new scheduled query rule named `Playbook Demo`.
2. I used the following query:
    ```sql
    AzureActivity
    | where ResourceProviderValue =~ "Microsoft.Security" 
    | where OperationNameValue =~ "Microsoft.Security/locations/jitNetworkAccessPolicies/delete"
    ```
3. I set the query schedule to run every 5 minutes.
4. I added an automation rule to trigger the playbook when an alert is created.

### Task 6: Invoke an Incident and Review the Associated Actions
1. I navigated to `Microsoft Defender for Cloud` and deleted a Just-in-time VM access policy.
2. I verified that the incident appeared in Microsoft Sentinel.
