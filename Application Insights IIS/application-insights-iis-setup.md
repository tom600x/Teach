# Application Insights – IIS Codeless Monitoring Setup

## Prerequisites
- Windows Server with IIS running
- .NET Framework 4.5+ or .NET Core application
- PowerShell running as **Administrator**
- Outbound HTTPS (port 443) to Azure
- An Azure subscription

---

## Step 1: Create an Application Insights Resource

1. Go to the [Azure Portal](https://portal.azure.com)
2. Search for **Application Insights** → click **Create**
3. Fill in: Subscription, Resource Group, Name, Region
4. Set Resource Mode to **Workspace-based** (recommended)
5. Click **Review + Create** → **Create**
6. Once deployed, open the resource and copy the **Connection String**

---

## Step 2: Update PowerShellGet (Required First)

```powershell
Install-Module -Name PowerShellGet -Force
```

> Close and reopen PowerShell as Administrator before continuing.

---

## Step 3: Install the Application Insights Agent Module

```powershell
Install-Module -Name Az.ApplicationMonitor -AllowPrerelease -AcceptLicense
```

---

## Step 4: Enable Monitoring

### Monitor all IIS sites (recommended)

Use `-InstrumentationKeyMap` with a catch-all regex to cover every site on the server:

```powershell
Enable-ApplicationInsightsMonitoring -InstrumentationKeyMap @(
    @{MachineFilter='.*'; AppFilter='.*'; InstrumentationSettings=@{InstrumentationKey='YOUR-KEY-HERE'}}
)
```

> `AppFilter='.*'` is a C# regex matched against the **IIS Site Name**. `.*` matches every site.

### Monitor specific sites with different keys

```powershell
Enable-ApplicationInsightsMonitoring -InstrumentationKeyMap @(
    @{MachineFilter='.*'; AppFilter='SiteA'; InstrumentationSettings=@{InstrumentationKey='KEY-FOR-SITE-A'}},
    @{MachineFilter='.*'; AppFilter='SiteB'; InstrumentationSettings=@{InstrumentationKey='KEY-FOR-SITE-B'}}
)
```

### Monitor a single site (simple)

```powershell
Enable-ApplicationInsightsMonitoring -ConnectionString 'InstrumentationKey=00000000-0000-0000-0000-000000000000;IngestionEndpoint=https://xxxx.applicationinsights.azure.com/'
```

> Get the full Connection String from: Azure Portal → Application Insights resource → Overview  
> Replace `YOUR-KEY-HERE` with the **Instrumentation Key** (GUID only) from the Connection String.

---

## Step 5: Restart IIS

```powershell
iisreset
```

---

## Verify the Connection

### Option 1: Live Metrics (instant)
1. Browse your website to generate traffic
2. Azure Portal → Application Insights resource → **Live Metrics**
3. You should see active requests within seconds

### Option 2: Transaction Search
1. Azure Portal → Application Insights → **Transaction Search**
2. Wait 2–5 minutes after browsing the site
3. Filter by **Request** to see incoming traffic

### Option 3: Check Monitoring Status via PowerShell
```powershell
Get-ApplicationInsightsMonitoringStatus
```
Expected output confirms: which sites are instrumented and the connection string in use.

### Option 4: Check IIS Worker Process
The agent injects into the IIS worker process (`w3wp.exe`). Confirm it loaded:
```powershell
Get-Process w3wp | Select-Object Id, CPU, WorkingSet
```
Then check Application Event Log for Application Insights entries:
```powershell
Get-EventLog -LogName Application -Source "*ApplicationInsights*" -Newest 20
```

---

## Management Commands

| Command | Purpose |
|---|---|
| `Get-ApplicationInsightsMonitoringStatus` | Check if monitoring is active and which sites are instrumented |
| `Get-ApplicationInsightsMonitoringConfig` | View the current configuration |
| `Disable-ApplicationInsightsMonitoring` | Turn off monitoring for all sites |
| `Enable-ApplicationInsightsMonitoring` | Turn on monitoring |

---

## Troubleshooting

- **No data in portal**: Wait 5 minutes, then check Live Metrics after browsing the site
- **Module install fails**: Ensure PowerShellGet is up to date (Step 2)
- **`AllowPrerelease` parameter error**: Re-run Step 2 and reopen PowerShell
- **Connection string vs Instrumentation Key**: Always use the full Connection String — the standalone Instrumentation Key is being deprecated
- **Firewall**: Ensure port 443 outbound is open to `*.applicationinsights.azure.com`

---

## Dependency Tracking

### What is tracked automatically (no setup needed)

Once the agent is running, these dependency types are captured out of the box:

| Dependency type | What is captured |
|---|---|
| **SQL Server / Azure SQL** | Server name, database name, stored proc / query name, duration, success/fail |
| HTTP / HTTPS calls | URL, method, status code, duration |
| Azure Cosmos DB | Operation, collection, duration |
| Azure Blob / Queue / Table Storage | Operation, container/queue name, duration |
| Azure Service Bus / Event Hubs | Operation, entity name, duration |

View these in: Azure Portal → Application Insights → **Performance** → **Dependencies** tab.

---

### Enable full SQL query text (optional)

The actual SQL statement is **not** captured by default. To enable it:

```powershell
# Step 1 – Enable the Instrumentation Engine (run as Administrator)
Enable-InstrumentationEngine

# Step 2 – Re-enable monitoring with SQL text capture ON
Enable-ApplicationInsightsMonitoring -InstrumentationKeyMap @(
    @{MachineFilter='.*'; AppFilter='.*'; InstrumentationSettings=@{InstrumentationKey='YOUR-KEY-HERE'}}
) -EnableSqlCommandTextInstrumentation

# Step 3 – Restart IIS
iisreset
```

> **Security warning:** Full SQL text may contain sensitive data or PII. Only enable this if you are confident queries do not expose sensitive values.

---

### Oracle databases

**Oracle is NOT automatically tracked** by the Application Insights IIS agent. The codeless agent only intercepts `System.Data.SqlClient` and `Microsoft.Data.SqlClient` (SQL Server). Oracle's `ODP.NET` driver (`Oracle.DataAccess` / `Oracle.ManagedDataAccess`) is not hooked automatically.

#### Workaround options

**Option A – Use `TrackDependency` in code (requires app change)**

If code changes are allowed, wrap Oracle calls manually:

```csharp
var telemetry = new TelemetryClient();
var startTime = DateTimeOffset.UtcNow;
var timer = Stopwatch.StartNew();
bool success = false;
try
{
    // ... execute Oracle command ...
    success = true;
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("Oracle", "MyDatabase", "SELECT ...", startTime, timer.Elapsed, success);
}
```

**Option B – Route Oracle through a SQL Server linked server**  
Oracle calls proxied through SQL Server linked servers will appear as SQL dependencies automatically.

**Option C – Use OpenTelemetry with Oracle instrumentation**  
The `OpenTelemetry.Instrumentation.Oracle` community package can instrument ODP.NET when used with the Azure Monitor OpenTelemetry exporter. This requires adding the package to the application.

#### Query to see what dependencies ARE flowing

```kusto
dependencies
| where timestamp > ago(1h)
| summarize count() by type, target
| order by count_ desc
```

If Oracle calls are not in the results, they are not being captured.

