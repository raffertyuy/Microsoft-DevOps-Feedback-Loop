# Microsoft-DevOps-Feedback-Loop
Azure Logic Apps that create Azure DevOps work items from Microsoft Sentinel and Defender for Cloud alerts, and dismiss the alert upon completion of the workitem.

## Pre-requisites
Please read the ff. articles to understand the context and usage of the playbooks in this repository.
- [Operations Task Management for Azure Alerts](https://www.raffertyuy.com/raztype/operations-task-management-from-azure-alerts/)

Before deploying the playbooks, the following are required
- Azure DevOps Account
  - Azure DevOps Custom Process with `Issue` and `Problem` work item types containing the following custom properties:
    - Source (string)
    - SourceType (string)
    - SourceID (string)
    - SubscriptionId (string)
  - Azure DevOps Project
  - [Service Hook](https://docs.microsoft.com/en-us/azure/devops/service-hooks/services/webhooks?view=azure-devops) configured on `Work item updated`
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Azure Subscription and AD access to create managed identities and grant permissions (for the feedback loop)

## Playbooks
### Microsoft Sentinel --> Create Azure DevOps Workitems
**Creating from Sentinel Incidents**

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FSentinelIncident-Create-DevOpsItem-LogicApp%2Fazuredeploy.json)

**Creating from Sentinel Alerts**

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FSentinelAlert-Create-DevOpsItem-LogicApp%2Fazuredeploy.json)

### Microsoft Defender for Cloud --> Create Azure DevOps Workitems
>Note: After deploying the logic apps below, the [Workflow Automation](https://docs.microsoft.com/en-us/azure/defender-for-cloud/workflow-automation) in Microsoft Defender for Cloud must be configured.
**Creating from Defender Alerts**

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FDefenderAlert-Create-DevOpsItem-LogicApp%2Fazuredeploy.json)

**Creating from Defender Recommendations**

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FDefenderReco-Create-DevOpsItem-LogicApp%2Fazuredeploy.json)

**Creating from Defender Regulatory Compliance**

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FDefenderCompliance-Create-DevOpsItem-LogicApp%2Fazuredeploy.json)

### Azure DevOps Workitems --> Sentinel and Defender (feedback loop)
Since the Azure DevOps work item can be from Sentinel or Defender, this playbook is combined for both.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fraffertyuy%2FMicrosoft-DevOps-Feedback-Loop%2Fmaster%2FWorkItemUpdate-ResolveAlertOrIncident-LogicApp%2Fazuredeploy.json)