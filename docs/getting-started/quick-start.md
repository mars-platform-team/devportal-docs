# Quick Start Guide

Get started with the Developer Portal in just 5 minutes!

!!! info "Important"
    This portal provides access to all your platforms and environments in one place. **Grafana & Loki remain your primary tools** for log analysis and monitoring. Use DevPortal for quick log checks and application management.

## 1. Login & Access (30 seconds)

1. Navigate to the DevPortal URL (provided by your platform team)
2. Click **Sign in with Microsoft**
3. Authenticate using your company Microsoft account
4. Click **"Applications"** in the left sidebar
5. Select your application to view details
6. Click the **"MARS Rover"** tab to access management features
7. Your role appears in the top right (Viewer, Developer, Lead, or Admin)

## 2. Find Your Application (30 seconds)

1. Select your **platform** (cloud environment) from the dropdown at the top
2. Choose your **environment** (e.g., dev, qa, prod) from the second dropdown
3. Your applications appear in the list
4. Use the search box to filter by application name

!!! tip "Platform Selection"
    If you don't see the platform you need, contact the MARS Platform Team to request access.

## 3. View Application Details (1 minute)

Click on an application name to see:

- **Status**: Is it running, pending, or failed?
- **Routes**: External URLs to access your app
- **Instances**: How many are running and their health status
- **Configuration**: Environment variables and settings
- **Logs**: Real-time application output

## 4. Common Tasks (3 minutes)

### See Real-Time Logs

1. Click your app name
2. Go to **Logs** tab
3. Watch logs stream in real-time
4. Close the tab when done (streaming stops automatically)

!!! note "Grafana & Loki for Deep Analysis"
    DevPortal logs are great for quick checks during development. For historical analysis, complex queries, and dashboards, continue using **Grafana & Loki**.

### Restart Your Application

1. Click your app name
2. Click **Actions** → **Restart**
3. Confirm the restart
4. An operation ID appears - use it to track progress
5. Instances will restart (usually 20-60 seconds)

### Scale Instances

1. Click your app name
2. Click **Actions** → **Scale**
3. Enter the number of instances you want
4. Track the operation to completion
5. Verify instance count updated

### Update Configuration

1. Click your app name
2. Go to **Configuration** tab
3. Click **Edit**
4. Update environment variables or settings
5. Save changes
6. Track the update operation
7. Your app restarts with new configuration

## What Can I Do Based on My Role?

| Action | Viewer | Developer | Lead | Admin |
|--------|:------:|:---------:|:----:|:-----:|
| View applications | ✅ | ✅ | ✅ | ✅ |
| View logs | ✅ | ✅ | ✅ | ✅ |
| Create applications | ❌ | ✅ | ✅ | ✅ |
| Update configuration | ❌ | ✅ | ✅ | ✅ |
| Restart/Scale apps | ❌ | ✅ | ✅ | ✅ |
| Stop applications | ❌ | ✅ | ✅ | ✅ |
| Delete applications | ❌ | ❌ | ✅ | ✅ |
| Manage platform services | ❌ | ❌ | ❌ | ✅ |

!!! question "Need Different Permissions?"
    Contact the MARS Platform Team to request a role change or access to additional platforms.

## From Epinio to Backstage

| I Used to Do in Epinio UI... | Now I Do in Backstage... |
|-----------------|-------------|
| Browse applications list | Select environment, browse app list |
| Click on app to view details | Click on app name |
| View app logs | Click app → Logs tab |
| Restart application | Click app → Actions → Restart |
| Edit app configuration/values | Click app → Configuration → Edit |
| Delete an application | Click app → Actions → Delete |
| Scale instances | Click app → Actions → Scale |
| Check app status | View instance summary on app details |

## Quick Reference: Common Actions

### ⚡ Quick Restart After Code Change
```
1. Navigate to your app
2. Actions → Restart
3. Wait ~30 seconds
4. Done!
```

### 🔧 Update Environment Variable
```
1. Navigate to your app
2. Configuration → Edit
3. Find the variable and update value
4. Save changes
5. App restarts automatically with new config
6. Verify in ~60 seconds
```

### 📈 Scale for More Traffic
```
1. Navigate to your app
2. Actions → Scale
3. Enter new instance count (e.g., 3)
4. Confirm
5. Wait ~45 seconds for instances to start
```

### 🔍 Debug Application Issues
```
1. Navigate to your app
2. Check instance summary - any failures?
3. Open Logs tab
4. Look for error messages
5. Fix configuration if needed
6. Restart app
```

### 🛑 Emergency Stop
```
1. Navigate to your app
2. Actions → Stop
3. Confirm
4. All instances shut down in ~30 seconds
5. To restart: Actions → Start
```

## Understanding Status

### Application Status
- **Running** ✅ - Healthy, serving traffic
- **Pending** 🔄 - Starting up (wait a moment)
- **Failed** ❌ - Check logs to diagnose
- **Stopped** 🛑 - Manually stopped, click Start to resume

### Operation Status
- **Pending** - Queued, waiting to start
- **In Progress** - Currently running
- **Completed** - Successfully finished
- **Failed** - Error occurred (see message for details)

## Troubleshooting Quick Tips

### My application won't start
1. Check logs for error messages
2. Verify configuration (env vars, ports)
3. Check instance health status
4. Ensure routes are correctly defined
5. Try restarting

### Configuration change didn't work
1. Check operation status - did it complete?
2. View current configuration - did it update?
3. Check logs for errors after restart
4. Verify syntax (JSON/YAML format)

### Can't perform an action
- ❌ **"Permission denied"** → Check your role (you may need Lead or Admin)
- ❌ **"Conflict detected"** → Another operation is running, wait for it to complete
- ❌ **"Not found"** → App may have been deleted or environment changed

### Operation taking too long
- Most operations: 30-60 seconds
- Scaling many instances: up to 90 seconds
- If > 2 minutes: Note operation ID and report to platform team

## Next Steps

- **[Application Management Guide](../user-guides/application-management.md)** - Detailed guide for managing applications
- **[Monitoring & Logging](../user-guides/monitoring-logging.md)** - Deep dive into logs and monitoring
- **[Configuration Management](../user-guides/configuration.md)** - Advanced configuration techniques
- **[Troubleshooting](../reference/troubleshooting.md)** - Solve common issues

## Remember

!!! success "Key Points"
    1. **Every action returns an operation ID** - use it to track progress
    2. **Most operations take 30-60 seconds** - be patient
    3. **Configuration changes restart your app** - expect brief downtime
    4. **Deletion is permanent** - double-check before confirming
    5. **Higher roles can do everything lower roles can** - Admin can do it all

---

**You're ready to go! Start with viewing your apps, then try a simple restart to get comfortable.**
