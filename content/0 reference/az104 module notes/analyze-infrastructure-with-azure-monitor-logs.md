---
{}
---
# Introduction

Logging and monitoring the health of your services is a vital component of
production applications. You need to be able to determine the causes of
failures. You also need to identify any problems before they occur.

Azure Monitor is an important tool to help you in this process. It allows you
to gather monitoring and diagnostic information about the health of your
services. You can use this information to visualize and analyze the causes of
problems that might occur in your app.

Suppose that you work for a large organization's operations team. The
organization is running large-scale production apps in the cloud. The team
wants to consolidate its log data in a single service to improve visibility
across services and simplify its logging strategy.

The team began implementing Azure Monitor logs. It wants to fully understand
how the logs work. It also wants to know the service's capabilities to query
and evaluate the log data that's fed into it.

## Learning objectives

In this module, you'll:

  * Identify the features and capabilities of Azure Monitor logs.
  * Create basic Azure Monitor log queries to extract information from log data.



---
# Features of Azure Monitor logs

Azure Monitor is a service for collecting and analyzing telemetry. It helps
you get maximum performance and availability for your cloud applications and
for your on-premises resources and applications. It shows how your
applications are performing and identifies any issues with them.

## Data collection in Azure Monitor

Azure Monitor collects two fundamental types of data: metrics and logs.
Metrics tell you how a resource is performing and the other resources that
it's consuming. Logs contain records that show when resources are created or
modified.

The following diagram gives a high-level view of Azure Monitor. On the left
are the data-monitoring sources: Azure, operating systems, and custom sources.
At the center of the diagram are the data stores for metrics and logs. On the
right are the functions that Azure Monitor performs with this collected data,
such as analysis, alerting, and streaming to external systems.

![Diagram of Azure Monitor's architecture, displaying the sources of
monitoring data, the data stores, and functions performed on the
data.](media/2-azure-monitor.svg)

Azure Monitor collects data automatically from a range of components. For
example:

  * **Application data** : Data that relates to your custom application code.
  * **Operating-system data** : Data from the Windows or Linux virtual machines that host your application.
  * **Azure resource data** : Data that relates to the operations of an Azure resource, such as a web app or a load balancer.
  * **Azure subscription data** : Data that relates to your subscription. It includes data about Azure health and availability.
  * **Azure tenant data** : Data about your Azure organization-level services, such as Microsoft Entra ID.

Because Azure Monitor is an automatic system, it begins to collect data from
these sources as soon as you create Azure resources like virtual machines and
web apps. You can extend the data that Azure Monitor collects by:

  * **Enabling diagnostics** : For some resources, such as Azure SQL Databases, you'll receive full information about a resource only after you've enabled diagnostic logging for it. You can use the Azure portal, the Azure CLI, or PowerShell to enable diagnostics.
  * **Adding an agent** : For virtual machines, you can install the Log Analytics agent and configure it to send data to a Log Analytics workspace. This agent increases the amount of information that's sent to Azure Monitor.

Your developers might also want to send data to Azure Monitor from custom
code, such as a web app, an Azure function, or a mobile app. They send data by
calling the Data Collector API. You can communicate with this REST interface
through HTTP. This interface is compatible with various development
frameworks, such as .NET Framework, Node.js, and Python. Developers can choose
their favorite language and framework to log data in Azure Monitor.

### Logs

Logs contain time-stamped information about resource changes. The type of
information recorded varies by log source. The log data is organized into
records, with different sets of properties for each type of record. The logs
can include numeric values like Azure Monitor metrics, but most include text
data rather than numeric values.

The most common type of log entry records an event. Events can occur
sporadically rather than at fixed intervals or according to a schedule. Events
are created by applications and services, which provide the context for the
events. You can store metric data in logs to combine them with other
monitoring data for analysis.

You can log data from Azure Monitor in a Log Analytics workspace. Azure
provides an analysis engine and a rich query language. The logs show the
context of any problems, and are useful for identifying root causes.

![Screenshot of an example query against Azure logs with the query text on top
and a graph displaying the results below.](media/2-azure-logs-query-
example.png)

### Metrics

Metrics are numerical values that describe some aspect of a system at a point
in time. Azure Monitor can capture metrics in near-real time. The metrics are
collected at regular intervals, and are useful for alerting because of their
frequent sampling. You can use various algorithms to compare a metric to other
metrics and observe trends over time.

Metrics are stored in a time-series database. This data store is most
effective for analyzing time-stamped data. Metrics are suited for alerting and
fast detection of issues. They can tell you about system performance. If
needed, you can combine them with logs to identify the root cause of issues.

![Screenshot of an example chart in Azure Metrics displaying average CPU
percentage.](media/2-azure-monitor-metrics.png)

## Analyzing logs by using Kusto

To retrieve, consolidate, and analyze data, you can specify a query to run in
Azure Monitor logs. You can write a log query with the Kusto query language,
which Azure Data Explorer also uses.

You can test log queries in the Azure portal so you can work with them
interactively. You'll typically start with basic queries, then progress to
more advanced functions as your requirements become more complex.

In the Azure portal, you can create custom dashboards, which are targeted
displays of resources and data. You can build each dashboard from a set of
tiles. Each tile might show a set of resources, a chart, a data table, or some
custom text. Azure Monitor provides tiles that you can add to dashboards; for
example, you might use a tile to display the results of a Kusto query in a
dashboard.

In the example scenario, the operations team can consolidate its monitoring
data by visualizing it in charts and tables. These tools are effective for
summarizing data and presenting it to different audiences.

By using Azure dashboards, you can combine various kinds of data, including
both logs and metrics, into a single pane in the Azure portal. For example,
you might want to create a dashboard that combines tiles that show a graph of
metrics, a table of activity logs, charts from Azure Monitor, and the output
of a log query.

## Check your knowledge

1.

What data does Azure Monitor collect?

Data from a variety of sources, such as the application event log, the
operating system (Windows and Linux), Azure resources, and custom data sources

Azure billing details

Backups of database transaction logs

2.

What two fundamental types of data does Azure Monitor collect?

Metrics and logs

Username and password

Email notifications and errors

Check your answers

You must answer all questions before checking your work.



---# Create basic Azure Monitor log queries to extract information from log data

You can use Azure Monitor log queries to extract information from log data.
Querying is an important part of examining the log data that Azure Monitor
captures.

In the example scenario, the operations team will use Azure Monitor log
queries to examine the health of its system.

## Write Azure Monitor log queries by using Log Analytics

You can find the Log Analytics tool in the Azure portal and use it to run
sample queries or to create your own queries:

  1. In the Azure portal, in the left menu pane, select **Monitor**.

The Azure Monitor page appears along with more options, including **Activity
Log** , **Alerts** , **Metrics** , and **Logs**.

  2. Select **Logs**.

Here, you can enter your query and see the output.

![Screenshot of Azure Monitor with a new query tab opened.](media/3-azure-
monitor-portal-query-pane.png)

## Write queries by using the Kusto language

You can use the Kusto Query Language to query log information for your
services running in Azure. A Kusto query is a read-only request to process
data and return results. You'll state the query in plain text by using a data-
flow model that's designed to make the syntax easy to read, write, and
automate. The query uses schema entities that are organized in a hierarchy
similar to that of Azure SQL Database: databases, tables, and columns.

A Kusto query consists of a sequence of query statements, delimited by a
semicolon (`;`). At least one statement is a tabular expression statement. A
tabular expression statement formats the data arranged as a table of columns
and rows.

A tabular expression statement's syntax has a tabular data flow from one
tabular query operator to another, starting with a data source. A data source
might be a table in a database or an operator that produces data. The data
then flows through a set of data-transformation operators that are bound
together with the pipe (`|`) delimiter.

For example, the following Kusto query has a single tabular expression
statement. The statement starts with a reference to a table called `Events`.
The database that hosts this table is implicit here, and is part of the
connection information. The data for that table, stored in rows, is filtered
by the value of the `StartTime` column. The data is filtered further by the
value of the `State` column. The query then returns the count of the resulting
rows.

    
    
    Events
    | where StartTime >= datetime(2018-11-01) and StartTime < datetime(2018-12-01)
    | where State == "FLORIDA"  
    | count
    

Note

The Kusto query language that Azure Monitor uses is case-sensitive. Language
keywords are typically written in lowercase. When you're using names of tables
or columns in a query, make sure to use the correct case.

Events captured from the event logs of monitored computers are just one type
of data source. Azure Monitor provides many other types of data sources. For
example, the `Heartbeat` data source reports the health of all computers that
report to your Log Analytics workspace. You can also capture data from
performance counters and update management records.

The following example retrieves the most recent heartbeat record for each
computer. The computer is identified by its IP address. In this example, the
`summarize` aggregation with the `arg_max` function returns the record with
the most recent value for each IP address.

    
    
    Heartbeat
    | summarize arg_max(TimeGenerated, *) by ComputerIP
    



---# Exercise - Create basic Azure Monitor log queries to extract information
from log data

The operations team doesn't currently have enough information about its system
behavior to diagnose and resolve problems effectively. To address this issue,
the team has configured an Azure Monitor workspace with the company's Azure
services. It runs Kusto queries to get the status of the system and attempts
to identify the causes of any problems that might occur.

In particular, the team is interested in monitoring security events to check
for possible attempts to break into the system. An attacker might try to
manipulate the applications running on the system, so the team also wants to
gather application data for further analysis. An attacker might also try to
halt the computers that compose the system, so the team wants to examine how
and when machines are stopped and restarted.

In this exercise, you'll practice performing Azure log queries against a demo
project that contains sample data in tables, logs, and queries.

## Create basic Azure Monitor log queries to extract information from log data

Let's use the **Azure Demo Logs pane** to practice writing queries. The demo
project workspace is prepopulated with sample data. Azure offers an optimized
SQL-like query with visualization options of its data in a language called KQL
(Kusto Query Language.)

  1. Open the [Logs demo environment](https://portal.azure.com/learn.docs.microsoft.com/#blade/Microsoft_Azure_Monitoring_Logs/DemoLogsBlade?azure-portal=true). In the top-left corner, under **New Query 1** , you'll find **Demo** , which identifies the workspace, or the scope of the query. The left side of this pane contains several tabs: **Tables** , **Queries** , and **Functions**. The right side has a scratchpad for creating or editing queries.

  2. On the **New Query 1** tab, enter a basic query on the first line of the scratchpad. This query retrieves the details of the 10 most recent security events.
    
        SecurityEvent
        | take 10
    

  3. In the command bar, select **Run** to execute the query and view the results. You can expand each row in the results pane for more information.

  4. Sort the data by time by adding a filter to your query:
    
        SecurityEvent
        | top 10 by TimeGenerated
    

  5. Add a filter clause and a time range. Run this query to fetch records that are more than 30 minutes old, and that have a level of 10 or more:
    
        SecurityEvent
        | where TimeGenerated < ago(30m)
        | where toint(Level) >= 10
    

  6. Run the following query to search the `AppEvents` table for records of the `Clicked Schedule Button` event being invoked in the last 24 hours:
    
        AppEvents 
        | where TimeGenerated > ago(24h)
        | where Name == "Clicked Schedule Button"
    

  7. Run the following query to display the number of different computers that generated heartbeat events each week for the last three weeks. The results appear as a bar chart:
    
        Heartbeat
        | where TimeGenerated >= startofweek(ago(21d))
        | summarize dcount(Computer) by endofweek(TimeGenerated) | render barchart kind=default
    

## Use predefined Azure log queries to extract information from log data

In addition to writing queries from scratch, the operations team can also take
advantage of predefined queries in Azure Logs that answer common questions
related to their resources' health, availability, usage, and performance.

  1. Use the **Time Range** parameter in the command bar to set a custom range. Select the month, year, and day to a range from January to today. You can set and apply a custom time to any query.

  2. On the toolbar, select **Queries**. The **Queries** pane appears. Here, in the drop-down list in the left menu, you can view a list of the sample queries grouped by _Category_ , _Query type_ , _Resource type_ , _Solution_ , or _Topic_.

  3. Select **Category** in the drop-down list, and then select **IT & Management Tools**.

  4. In the search box, enter _Distinct missing updates cross computers_. Select the query in the left pane, then select **Run**. The **Logs** pane reappears, with the query returning a list of Windows updates missing from virtual machines that are sending logs to the workspace.

Note

You can also run this same query from the **Logs** pane. In the left pane,
select the **Queries** tab, then select **Category** in the **Group by**
dropdown list. Now scroll down the list, expand **IT & Management Tools**, and
double-click **Distinct missing updates cross computers**. Select **Run** to
run the query. When you select a predefined query in the left pane, the query
code is appended to whatever query exists in the scratchpad. Remember to clear
the scratchpad before opening or adding a new query to run.

  5. In the left pane, clear the search box. Select **Queries** , then select **Category** in the **Group by** dropdown list. Expand **Azure Monitor** , and double-click **Computers availability today**. Select **Run**. This query creates a time series chart with the number of unique IP addresses sending logs into the workspace each hour for the last day.

  6. Select **Topic** in the **Group by** dropdown list, scroll down to expand **Function App** , and then double-click **Show application logs from Function Apps**. Select **Run**. This query returns a list of application logs, sorted by time with the latest logs shown first.

You'll notice that from the Kusto queries you used here, it's easy to target a
query to a specific time window, event level, or event log type. The security
team can easily examine heartbeats to identify when servers are unavailable,
which might indicate a denial-of-service attack. If the team spots the time
when a server was unavailable, it can query for events in the security log
around that time to diagnose whether an attack caused the interruption.
Additionally, predefined queries can also evaluate VM availability, identify
missing Windows updates, and review firewall logs to view denied network flows
intended for the VMs of interest.



---# Summary

In this module, you learned how to use Azure Monitor. You looked at Azure
Monitor logs to extract valuable information about your infrastructure from
log data by using queries, and you performed these queries by using the Kusto
query language.

You learned how to:

  * Explore the types of data that Azure Monitor collects.
  * Create Azure Monitor log queries to extract information from the log data.

You can now use Azure Monitor to analyze your environment and troubleshoot
issues.

## Learn more

For more information about Azure Monitor, check out the following articles:

  * [Azure Monitor overview](/en-us/azure/azure-monitor/overview)
  * [Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/log-query/get-started-queries)
  * [Optimize log queries in Azure Monitor](/en-us/azure/azure-monitor/log-query/log-query-performance)
  * [Create and share dashboards of Log Analytics data](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)
  * [Analyze and visualize monitoring data](/en-us/azure/azure-monitor/best-practices-analysis)



---