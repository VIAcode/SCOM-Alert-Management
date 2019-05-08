# SCOM Alert Management solution

## Overview

The SCOM Alert Management solution extends capabilities of Microsoft Alert Management solution with automation of alert rules creation for System Center Operations Manager management group connected to the Log Analytics workspace. The solution creates an alert rule for each SCOM alert type. After Alert rule is available on Azure Monitor, you can manage them as standard scheduled query rules. At the same time, the solution closes SCOM Alerts generated by standard Alert Management solution. Key Scenarios, not available in the Microsoft Alert Management solution:

- Automatically create Azure Alert Rules for all SCOM alerts.
- Propagate SCOM Alert description into Azure Alert events.
- Support enabling and disabling of Azure Alert generation for corresponding SCOM Alerts.
- Support integration scenarios, such as webhooks, action groups, etc.

## Prerequisites

Before starting, review the following requirements.

- Download and set up System Center Operation Manager from [here](https://docs.microsoft.com/en-us/system-center/scom/manage-operations-guide-overview?view=sc-om-1807).
- Create a Log Analytics workspace in the Azure portal from [here](https://docs.microsoft.com/en-us/azure/azure-monitor/learn/quick-create-workspace).
- Connect Operations Manager to Azure Monitor from [here](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/om-agents).
- Add the Alert Management solution to your Log Analytics workspace.

Let's consider the following case when an error has occurred on the client's side.

The error on the client side:

![Testdb offline](./media/testdb_offline.jpg)

The alert in SCOM:

![SCOM alert](./media/SCOM2016RTMs_alert.jpg)

1. In the portal, select **Monitor** and under the Monitor section - choose **Alerts**.

![Monitor Alerts](./media/monitor_alerts.jpg)

2. You will land on the Alerts Summary page, which gives you an overview of all your alert instances across Azure.

<!--jpg without rule -->

As you can see, the alert raised in Azure does not have a correspondent alert rule, so you cannot manage this alerts - you cannot disable them, change severity, assign an action group.

## Install SCOM Alert Management solution

### Install from the Portal

1. Log in to the Azure portal.
2. Open **All Services** and locate **Solutions**.
3. Click **Add** and find **SCOM Alert Management** solution.

![Add solution](./media/add_solution.jpg)

4. Click **Create** to start the installation process.

![Create SCOM Alert Management solution](./media/scom_am_create_page.jpg)

5. When the installation process starts, you're prompted to provide required configuration.

### Configuration

1. Configure basic settings

![Basics](./media/create_basics_example.jpg)

- Select a Subscription to link to by selecting from the drop-down list if the default selected is not appropriate.
- For Resource Group, choose to use an existing empty resource group or create a new one.
- Select the same Location as in Log Analytics.

2. Log Analytics Settings

![Log Analytics Settings](./media/log_analytics_settings_example.jpg)

- Type the Log Analytics workspace Resource Group name
- Type the Log Analytics workspace name

3. Summary

![Summary page](./media/summary.jpg)

- You're prompted to provide information such as the resource group and location in addition to values for any parameters in the solution

4. Buy

- User can read Terms of Use and [Private Policy](https://www.viacode.com/viacode-privacy-statement)

### Install from the Marketplace

1. Open Azure Marketplace
2. Select **Management Tools** and find **SCOM Alert Management** solution

![Marketplace Management Tools](./media/marketplace_management_tools.jpg)

3. Click **Create** to start the installation process.

## Verify monitoring solution deploy

The solution is in a separate resource group and includes two logic apps.

- [x] **AlertCreator** creates a new alert rule.
- [x] **CloseAlerts** closes the original Alert Management solution (unmanageable alerts).

![Demo Solution RG](./media/demo_solution_rg.jpg)

## Automatically create Azure Alert Rules for all SCOM alerts

1. In the portal, select **Monitor** and under the Monitor section - choose **Alerts**.

![Monitor Alert](./media/monitor_alerts.jpg)

2. You'll will see auto created alert rule.

![Alert Rule](./media/alert_rule.jpg)

3. Click on **Total alert rules** to show the Rules page.

![total alert rules](./media/rule.jpg)

4. Select the rule

![SCOM Alert rule](./media/Rule_drillon.JPG)

<!-- <Description?> -->

## Manage alert rules

### Enable or Disable the generation of Azure Alerts for corresponding SCOM Alerts.

You can manage alerts by enabling and disabling them in the alert rule section.
<!-- In the Rule page , you can select multiple alert rules and enable/disable them. This might be useful when certain target resources need to be put under maintenance-->

 - If the alert is no longer required, click on **Disable** button. 

![Disable rule](./media/disable_rule.jpg)

- In that case you won't see it in the **Alert** page.

<!-- -->

### Log query

You can view and manage log queries by clicking on the **Condition** value.

![Log query](./media/log_query.jpg)

### ITSM

