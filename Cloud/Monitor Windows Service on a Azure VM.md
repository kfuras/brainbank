# How to monitor Windows Service in Azure VM  

The requirement is to track a Windows Service running on a Virtual Machine on Azure. When the service was stopped (or crashed), generate an  
alert to the support team.  

## Prerequisites

You will need a **Log Analytics** **Workspace** and **Automation** service to store configuration and generate alerts.  

## Step 1: Enable VM Inventory and Change Tracking 

This feature monitors the Virtual Machine for changes in software,  
files, windows registry and windows services.  

1. On the desired Virtual Machine in the Azure Portal, select **Inventory** under **Configuration** **Management**.
2. Select your **Log Analytics** **Workspace** and **Automation Account**, then click **Enable**.

[![](https://www.smcculloch.com/static/2dda83a6c1a9e72ffefffa52d297ad0a/fcda8/inventory.png)](https://www.smcculloch.com/static/2dda83a6c1a9e72ffefffa52d297ad0a/fcda8/inventory.png)
Enable inventory and tracking in Azure  

This will allow Azure to collect inventory on your virtual machine and monitor for changes.  

> Note: on my account, it took a few hours for all windows services to show up.  

When fully configured, the **Inventory** will show a tab with all Windows Services and their current state:  

[![](https://www.smcculloch.com/static/6451555399420f4ad8e59e567f527b68/fcda8/win-services.png)](https://www.smcculloch.com/static/6451555399420f4ad8e59e567f527b68/fcda8/win-services.png)

Window Services tracking - Virtual Machines  

The default collection of windows service states are 30 minutes. This  
might be too slow for monitoring purposes. You can change this value  
in **Edit Settings**:

[![](https://www.smcculloch.com/static/53af6aa37f3077580351bfca1eef9190/fcda8/edit-settings.png)](https://www.smcculloch.com/static/53af6aa37f3077580351bfca1eef9190/fcda8/edit-settings.png)

Window Services tracking - Edit Settings  

Navigate to **Windows Services** tab and change the collection frequency to a smaller number (e.g. 2 minutes):  

[![](https://www.smcculloch.com/static/b770252c9057008b8d0ff49a28fc5334/fcda8/win-services-collection.png)](https://www.smcculloch.com/static/b770252c9057008b8d0ff49a28fc5334/fcda8/win-services-collection.png)

Window Services tracking - Collection Settings  

## Step 2: Configure Alert

Now that services are showing, we can setup an alert in **Log Analytics** to monitor the **Print Spooler** service.

[![](https://www.smcculloch.com/static/1c9b21cde33c9c667dd13c632b0c7738/fcda8/log-analytics-1.png)](https://www.smcculloch.com/static/1c9b21cde33c9c667dd13c632b0c7738/fcda8/log-analytics-1.png)
>Log Analytics

Modify the query to look for **Print Spooler** and a corresponding **Stopped** event.

```Plain
ConfigurationData | where ConfigDataType == "WindowsServices" and SvcDisplayName == "Print Spooler" and SvcState == "Stopped"
| order by TimeGenerated desc
```

Select **+ New alert rule** to use this query as the alert:  

[![](https://www.smcculloch.com/static/5a33cfda35105a777a7ce44891322abd/fcda8/new-alert-rule.png)](https://www.smcculloch.com/static/5a33cfda35105a777a7ce44891322abd/fcda8/new-alert-rule.png)
> New Alert Rule - Log Analytics  

The rule engine will use this query as the signal and you can specify  
how often it checks:  

Set a **threshold value** to **0**

> Azure will evaluate this query every 5 minutes and will trigger on 1 or more change events.  

[![](https://www.smcculloch.com/static/9b9fbc019ac4c6ae62d1cf27fb112d1d/fcda8/alert-rule.png)](https://www.smcculloch.com/static/9b9fbc019ac4c6ae62d1cf27fb112d1d/fcda8/alert-rule.png)

Alert Rule

- Navigate to **Actions**
- Specify an existing **Action Group** or create a new one. My action group sends an email to myself. 

> This is a list of people/services to notify when the alert triggers.  

[![](https://www.smcculloch.com/static/f40a3e765e060313048e3cc5d1f665d3/fcda8/alert-rule-action.png)](https://www.smcculloch.com/static/f40a3e765e060313048e3cc5d1f665d3/fcda8/alert-rule-action.png)

Alert Rule Action

- Navigate to **Details**.
- Give your alert an **Alert Rule** **Name** and **Severity**.

[![](https://www.smcculloch.com/static/f66bdbc5ab6efafabe517533d0cdfb5d/fcda8/alert-rule-details.png)](https://www.smcculloch.com/static/f66bdbc5ab6efafabe517533d0cdfb5d/fcda8/alert-rule-details.png)

> Alert Rule Details

- **Review + Create** to complete the alert setup.

## Step 3: Testing the Alert

RDP into your server and stop the **Print Spooler** service.

[![](https://www.smcculloch.com/static/cf2072d30832c0d971ff66765faa6695/fcda8/stop-service.png)](https://www.smcculloch.com/static/cf2072d30832c0d971ff66765faa6695/fcda8/stop-service.png)
> Stop Service

Once the service has stopped, you should receive a notification within the next 5 minutes stating the service has stopped.  

[![](https://www.smcculloch.com/static/0fe760d1420c46e1705dda489d9ffe55/fcda8/alert-detail.png)](https://www.smcculloch.com/static/0fe760d1420c46e1705dda489d9ffe55/fcda8/alert-detail.png)
> Alert Detail