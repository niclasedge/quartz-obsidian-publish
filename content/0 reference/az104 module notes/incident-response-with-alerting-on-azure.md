---
{}
---
# Azure Monitor Alerts Technical Documentation

## 1. Introduction
Azure Monitor provides robust alerting & monitoring capabilities for Azure resources. It enables:
- Real-time problem detection
- Proactive issue resolution
- Improved system reliability

Key benefits:
- Comprehensive monitoring across Azure services
- Customizable alert conditions
- Automated actions & notifications
- Integration with other Azure services

## 2. Alert Types

### 2.1 Metric Alerts
- Based on numerical time-series data
- Ideal for threshold monitoring
- Stateful: Notifies only on state changes

Use cases:
- CPU utilization > 90%
- Low storage capacity
- High network latency

Components:
- Target resource
- Metric
- Time aggregation
- Condition type (static/dynamic)
- Threshold
- Frequency
- Look-back period

### 2.2 Log Alerts
- Based on log file data
- Suitable for complex queries & historical analysis
- Stateless: Generates new alerts each time criteria are met

Use cases:
- Error frequency in application logs
- Security event detection
- Performance trend analysis

Components:
- Log query
- Time period
- Frequency
- Threshold
- Alert types:
  1. Number of records
  2. Metric measurement (aggregation function, group field, interval)

### 2.3 Activity Log Alerts
- Based on Azure resource operations
- Monitors subscription-level events
- Two types: Specific operations & Service health events

Use cases:
- Resource creation/deletion
- Role assignments
- Azure service incidents

Components:
- Category (e.g., Administrative, Service health)
- Scope (resource/group/subscription level)
- Operation name
- Level (Verbose, Info, Warning, Error, Critical)
- Status (Started, Failed, Succeeded)
- Initiator (email/Azure AD identifier)

## 3. Alert Rule Configuration

### 3.1 Common Components
- Resource: Target for monitoring
- Condition: Signal type & alert logic
- Actions: Notifications or automated tasks
- Alert details: Name, description, severity

### 3.2 Severity Levels
0: Critical
1: Error
2: Warning
3: Informational
4: Verbose

## 4. Action Groups
Collections of notification preferences & actions executed when an alert fires.

Supported actions:
- Email
- SMS
- Azure app push notification
- Voice call
- Azure function
- Logic app
- Webhook
- ITSM ticket
- Runbook (e.g., VM restart/scale)

Configuration:
1. Create action group
2. Add to alert rule
3. Reuse across multiple alerts

## 5. Alert Processing Rules
Override normal alert behavior by adding/suppressing action groups.

Use cases:
- Suppress notifications during maintenance
- Implement management at scale
- Add action groups to all alert types

Configuration:
1. Define scope (resource/group/subscription)
2. Set filters
3. Specify schedule (always active, one-time, recurring)

## 6. Best Practices

### 6.1 Metric Alerts
- Use dynamic thresholds for varying workloads
- Set appropriate time aggregation & frequency
- Leverage multi-resource monitoring

### 6.2 Log Alerts
- Optimize queries for performance
- Use metric measurement for reduced alert volume
- Implement alert suppression for known issues

### 6.3 Activity Log Alerts
- Focus on critical operations
- Utilize service health alerts for Azure-wide issues
- Implement proper RBAC for alert management

### 6.4 General
- Use action groups for consistent notifications
- Implement alert processing rules for maintenance windows
- Regularly review & optimize alert configurations

## 7. Implementation Guide

### 7.1 Creating a Metric Alert (Azure CLI)
```bash
az monitor metrics alert create \
  --name "High CPU Alert" \
  --resource-group myResourceGroup \
  --scopes "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM" \
  --condition "max percentage CPU > 90" \
  --window-size 5m \
  --evaluation-frequency 1m \
  --action /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Insights/actionGroups/myActionGroup
```

### 7.2 Creating a Log Alert (Azure PowerShell)
```powershell
$condition = New-AzScheduledQueryRuleLogMetricTrigger `
  -ThresholdOperator GreaterThan `
  -Threshold 10 `
  -MetricTriggerType Consecutive `
  -MetricColumn "_Count"

$source = New-AzScheduledQueryRuleSource `
  -Query "requests | where resultCode == '500'" `
  -DataSourceId /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.OperationalInsights/workspaces/myWorkspace

$schedule = New-AzScheduledQueryRuleSchedule -FrequencyInMinutes 15 -TimeWindowInMinutes 30

New-AzScheduledQueryRule `
  -ResourceGroupName myResourceGroup `
  -Location eastus `
  -Action $action `
  -Enabled $true `
  -Source $source `
  -Schedule $schedule `
  -Name "High Error Rate Alert"
```

### 7.3 Creating an Activity Log Alert (Azure portal)
1. Navigate to Monitor > Alerts > New alert rule
2. Select subscription/resource group as scope
3. Choose "Activity Log" as signal type
4. Configure alert logic (e.g., "Delete Virtual Machine")
5. Add action group
6. Set alert details (name, description, severity)

### 7.4 Creating an Action Group (Azure CLI)
```bash
az monitor action-group create \
  --name myActionGroup \
  --resource-group myResourceGroup \
  --action email myemail@contoso.com \
  --action sms 1 4255655665 \
  --action webhook mywebhook https://www.contoso.com/alert
```

### 7.5 Creating an Alert Processing Rule (Azure PowerShell)
```powershell
New-AzActionRule `
  -ResourceGroupName myResourceGroup `
  -Name "Maintenance Window" `
  -Scope "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup" `
  -ActionGroupId /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Insights/actionGroups/myActionGroup `
  -RecurrenceType Weekly `
  -RecurrenceValue "Saturday, Sunday" `
  -StartTime "2023-01-01T22:00:00Z" `
  -EndTime "2023-01-02T06:00:00Z"
```

## 8. Monitoring & Maintenance
- Regularly review alert efficacy
- Adjust thresholds based on performance data
- Implement proper logging for troubleshooting
- Use Azure Monitor Workbooks for visualization
- Leverage Azure Advisor for optimization recommendations

## 9. Limitations & Considerations
- Metric alert evaluation interval: 1 min (min)
- Log alert query time range: 48 hours (max)
- Activity log alert retention: 90 days
- Max actions per action group: 10
- Alert rule limit per subscription: 5000

## 10. Integration with Other Azure Services
- Azure Automation for complex remediation
- Azure Logic Apps for custom workflows
- Azure Functions for serverless actions
- Power BI for advanced visualizations

## 11. Cost Optimization
- Use appropriate alert frequencies
- Leverage Azure Monitor pricing tiers
- Implement log data retention policies
- Use Azure Reservations for consistent workloads

## 12. Security Considerations
- Implement least privilege access for alert management
- Use Azure Private Link for secure network access
- Enable Azure Monitor Private Link Scope (AMPLS)
- Encrypt sensitive data in action groups

## 13. Troubleshooting
- Check signal configuration for no-data scenarios
- Verify action group connectivity
- Review alert processing rules for suppressed notifications
- Use diagnostic settings for alert rule audit logs

## 14. Additional Resources
- [Azure Monitor documentation](https://docs.microsoft.com/en-us/azure/azure-monitor/)
- [Azure Monitor pricing](https://azure.microsoft.com/en-us/pricing/details/monitor/)
- [Azure Monitor GitHub repo](https://github.com/MicrosoftDocs/azure-docs/tree/main/articles/azure-monitor)
- [Azure Monitor Community](https://techcommunity.microsoft.com/t5/azure-monitor/bd-p/AzureMonitor)