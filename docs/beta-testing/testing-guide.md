# Beta Testing Guide: Epinio to Backstage Migration

## Overview

This guide helps you test the new Backstage-based Developer Portal as a replacement for Epinio. Focus on the key workflows you use daily to deploy and manage applications.

**Out of Scope for Initial Testing:**
- Jenkins deployment triggers (handled by platform team)
- First-time deployments via CI/CD
- Creating new applications (handled by CI/CD pipeline)
- Deep log analysis and troubleshooting (use Grafana & Loki)

---

## Before You Start Testing

### Key Things to Know

1. **Manifest Conversion is Automatic**: Your Epinio manifests are automatically converted by the CD pipeline - no manual changes needed

2. **Request Access First**: Contact MARS Platform Team to get access to the platforms and environments you need. They manage role assignments.

3. **One Portal, All Environments**: Instead of separate Epinio portals per platform, DevPortal gives you access to all platforms and environments from one URL.

4. **Your Routes Don't Change**: Application URLs remain the same after migration.

5. **CI/CD Process Stays the Same**: Your build process doesn't change - only the deployment target changes from Epinio to DevPortal.

6. **Use Grafana & Loki for Deep Analysis**: DevPortal logs are for quick checks. Continue using Grafana & Loki for historical analysis, complex queries, and monitoring dashboards.

### Migration Process (For Context)

When your team migrates:
1. Delete app from Epinio UI
2. Trigger your CD pipeline (unchanged)
3. App deploys to DevPortal automatically
4. Routes remain the same

For beta testing, apps may already be deployed to DevPortal for you.

---

## What Changed?

### Epinio UI → Backstage Applications

| What You Used in Epinio UI | New Backstage Equivalent |
|--------------------------|--------------------------|  
| Browse applications list | Browse applications in environment |
| View application details | View application details page |
| Delete application button | Delete application button |
| View application logs | Real-time log viewer |
| Edit app configuration/chart values | Update application configuration |
| Restart/scale application | Application management actions |
| Environment variables configuration | Configuration manifest editor |

---

## Getting Started

### Verify Your Access & Role

**Before you start**: Ensure you've requested and received access from the MARS Platform Team. If you don't have access yet, contact them with your team name and required platforms/environments.

- [ ] Check which role you have (Admin, Lead, Developer, or Viewer)
- [ ] Browse available platforms (cloud environments)
- [ ] Select a platform and see available environments
- [ ] Confirm you can see the "My Access" panel showing your permissions

**Note your role - it determines what actions you can perform:**
- **Viewer**: Read-only access to all applications on your assigned platforms
- **Developer**: Can update configuration, restart, scale, stop/start apps. **On production environments, Developers have read-only access** — only Leads and Admins can modify production apps.
- **Lead**: Everything Developer can do plus delete apps; full read/write on all tiers including production
- **Admin**: Full access including platform services across all environments

**Team-scoped roles**: You may have different roles on different platforms. For example, you could be a Lead on the `cp` platform but a Developer on `cpfhk`. Your effective permissions are resolved per platform when you switch environments.

**If you need additional access**: Contact MARS Platform Team to request access to additional platforms or role changes.

---

## Testing Checklist

### Discovering Applications

#### Browse Your Applications
- [ ] Select an environment from the dropdown
- [ ] See list of deployed applications
- [ ] Try sorting by name, status, or age
- [ ] Use search box to filter applications by name
- [ ] Navigate through pages if you have many apps
- [ ] Click on an application name to view details

#### View Application Info
- [ ] See application name, status, and version
- [ ] View external URLs (routes) for accessing your app
- [ ] Check how many instances are running
- [ ] See when the app was last updated
- [ ] Identify the container image being used

---

### Monitoring Application Health

#### Check Instance Status
- [ ] View how many instances are running/stopped/failed
- [ ] See restart counts for each instance
- [ ] Check if instances are healthy (ready)
- [ ] View when each instance was created
- [ ] Identify which instances need attention

#### View Application Logs
- [ ] Open the log viewer for your application
- [ ] See real-time log output
- [ ] Scroll through recent logs
- [ ] Test log streaming (new logs appear automatically)
- [ ] Verify logs stop streaming when you close the viewer
- [ ] For multi-container apps, confirm all container logs appear

**What to verify:**
- Logs appear without long delays (< 2 seconds)
- Log format is readable
- You can identify errors in your application
- Streaming stays connected for several minutes

**Important**: DevPortal logs are for quick troubleshooting during development. **Continue using Grafana & Loki** for:
- Historical log analysis (beyond recent logs)
- Complex log queries and filtering
- Monitoring dashboards
- Long-term trends and patterns

---

### Managing Application Configuration

#### View Current Configuration
- [ ] Open "Configuration" or "Manifest" tab
- [ ] View configuration in easy-to-read format
- [ ] See environment variables
- [ ] Check instance count (replicas)
- [ ] View resource limits (CPU, memory)
- [ ] See exposed routes and ports
- [ ] Download configuration as YAML or JSON

#### Update Configuration
- [ ] Click "Edit Configuration" or "Update Manifest"
- [ ] Change an environment variable value
- [ ] Save changes
- [ ] Wait for operation to complete (watch the status indicator)
- [ ] Verify the change appears in application details
- [ ] Check that your app restarted with new config

**Test scenarios:**
- Add a new environment variable
- Update an existing environment variable value
- Change instance count (scale up/down)
- Modify resource limits
- Add or update route configuration

---

### Application Lifecycle Actions

#### Restart Application
- [ ] Click "Restart" button or menu item
- [ ] Confirm restart action
- [ ] Wait for restart to complete (watch status indicator)
- [ ] Verify instances are recreated
- [ ] Confirm application is accessible after restart
- [ ] Check that restart involved zero downtime (if multiple instances)

#### Stop Application
- [ ] Click "Stop" button
- [ ] Confirm stop action
- [ ] Wait for operation to complete (watch status indicator)
- [ ] Verify all instances shut down
- [ ] Confirm application still appears in list (not deleted)
- [ ] Check that routes return an error (app is stopped)

#### Start Application
- [ ] Click "Start" button (on a stopped app)
- [ ] Wait for operation to complete (watch status indicator)
- [ ] Verify instances start running
- [ ] Confirm application becomes accessible

#### Scale Application
- [ ] Find the scaling control (slider, input, or menu)
- [ ] Increase instance count (e.g., 1 → 3)
- [ ] Wait for scaling to complete (watch status indicator)
- [ ] Verify the correct number of instances are running
- [ ] Decrease instance count (e.g., 3 → 1)
- [ ] Confirm instances scale down correctly
- [ ] Try scaling to 0 (should stop the app)

**What to verify:**
- Operations complete successfully within a reasonable time (duration depends on instance count and environment)
- Application behaves as expected after each action
- Clear error messages if something fails

---

### Deleting Applications

#### Delete Application (Lead/Admin Only)
- [ ] Select an application you can delete
- [ ] Click "Delete" button
- [ ] Read deletion warning carefully
- [ ] Confirm deletion
- [ ] Wait for deletion to complete (watch status indicator)
- [ ] Verify app is removed from list
- [ ] Confirm routes are no longer accessible

**Important:**
- Deletion is permanent - cannot be undone
- All data in the application is lost
- External resources (databases, storage) may need separate cleanup

---

### Operation Tracking

#### Monitor Operation Status
- [ ] After triggering any action, view the operation status panel
- [ ] See operation progress messages
- [ ] Watch status change from "pending" → "in progress" → "completed"
- [ ] For failures, see an error message explaining what went wrong
- [ ] Verify completed operations disappear after some time (cleanup)

#### View Operation History
- [ ] Open operation history for an application
- [ ] See list of recent operations (last 24 hours)
- [ ] Check details for each operation (type, status, time)
- [ ] Identify which user performed each operation
- [ ] View error messages for failed operations

**What to verify:**
- Status updates appear without manual refresh
- Error messages are helpful and actionable
- Can track multiple operations on different apps simultaneously

---

## Testing Scenarios

### Scenario 1: Update Environment Variable
1. View your application's current configuration
2. Note an existing environment variable value
3. Edit the configuration and change that value
4. Save and watch the operation status
5. Wait for operation to complete
6. Verify the change in configuration view
7. Check your application's behavior reflects the new value

### Scenario 2: Scale for Load Testing
1. Check current instance count (e.g., 1)
2. Scale up to 3 instances
3. Verify all 3 instances are running and healthy
4. Test your application (should handle more traffic)
5. Scale back down to 1 instance
6. Verify only 1 instance remains

### Scenario 3: Troubleshoot a Failed Instance
1. Find an application with a failed or restarting instance
2. Check the restart count (is it restarting repeatedly?)
3. View logs to identify error messages
4. Based on logs, determine if it's a configuration issue
5. Update configuration to fix the issue
6. Restart the application
7. Verify instances are now healthy

### Scenario 4: Emergency Stop
1. Identify an application that needs to be stopped immediately
2. Click "Stop" button
3. Confirm stop action
4. Verify all instances shut down (time depends on instance count)
5. Confirm application is inaccessible
6. Leave stopped for testing, or start it back up

### Scenario 5: Multi-App Management
1. Open 3 different applications in separate browser tabs
2. Make a different change to each app (restart, scale, config update)
3. Track all 3 operations simultaneously
4. Verify each completes independently without conflicts
5. Confirm no operation affected the wrong application

---

## Error Conditions to Test

### Permission Errors
- [ ] Try to delete an app as a Developer (should fail with clear message)
- [ ] As a Developer, try to modify an app in a **production** environment (should be denied — Developers are read-only on prod)
- [ ] Try to access another team's environment (should be denied)
- [ ] Attempt an action you're not authorized for
- [ ] Verify error messages explain what permission you need

### Invalid Input
- [ ] Try to scale to negative instances (should reject)
- [ ] Enter invalid YAML/JSON in configuration editor (should validate)
- [ ] Use a duplicate application name (should reject)
- [ ] Provide invalid environment variable names (special characters)
- [ ] Submit empty required fields

### Conflict Handling
- [ ] Start an operation (e.g., restart)
- [ ] Immediately try another operation on the same app (should detect conflict)
- [ ] See clear message about existing operation
- [ ] Wait for first operation to complete
- [ ] Retry second operation (should now succeed)

### Resource Not Found
- [ ] Manually change URL to non-existent application name (should get 404)
- [ ] Try to view an application that was just deleted (clear "not found" message)
- [ ] Reference an invalid environment or platform

---

## Performance Expectations

| Action | Expected Response Time | What to Report |
|--------|------------------------|----------------|
| Browse application list | < 2 seconds | Slow loading, timeouts |
| View application details | < 1 second | Delays, missing data |
| Open log viewer | < 3 seconds | Connection failures, lag |
| Start/Stop application | Varies by instance count | Excessive delays, failures |
| Scale application | Varies by instance count | Slow scaling, stuck operations |
| Update configuration | Varies by instance count | Timeouts, failed updates |
| Restart application | Varies by instance count | Excessive downtime, no recovery |

**Operation duration depends on the number of instances** — a single-instance app will complete significantly faster than one with 5+ instances. If you're experiencing unusually long operations, note:
- Number of running instances
- Time of day (peak hours vs off-peak)
- Complexity of configuration changes
- Any error messages or warnings

---

## Getting Help

**During testing, if you encounter issues:**

1. **Note the details:**
   - Timestamp when issue occurred
   - Application name and environment
   - Your role/permissions
   - What you were trying to do

2. **Check operation status:**
   - Failed operations have error messages
   - Note the exact error text

3. **Try basic troubleshooting:**
   - Refresh the page
   - Log out and back in
   - Try the operation again

4. **Report the issue:**
   - Include all details from step 1
   - Copy any error messages exactly
   - Attach screenshots if helpful

---

## Quick Reference

### Common Actions

| To Do This | Look For |
|------------|----------|
| See all my apps | Select environment from dropdown |
| Check app health | Click app name → view instances summary |
| View logs | Click app name → Logs tab |
| Restart app | Click app name → Actions → Restart |
| Scale instances | Click app name → Actions → Scale |
| Update config | Click app name → Configuration → Edit |
| Stop app temporarily | Click app name → Actions → Stop |
| Delete app permanently | Click app name → Actions → Delete (Lead/Admin only) |

### Status Indicators

| Status | Meaning | What to Do |
|--------|---------|------------|
| Running | Healthy and serving traffic | No action needed |
| Pending | Starting up | Wait a moment, refresh |
| Failed | Instance crashed | Check logs, verify configuration |
| Stopped | Manually stopped (scale 0) | Start it when ready |
| Unknown | Status unavailable | Refresh or check platform health |

---

## Success Criteria

At the end of your testing, you should be able to:

- ✅ Find and view all your applications easily
- ✅ Monitor application health and identify issues
- ✅ View logs to troubleshoot problems
- ✅ Update application configuration confidently
- ✅ Perform lifecycle operations (restart, scale, stop/start)
- ✅ Understand what's happening through clear status messages
- ✅ Feel confident managing your applications without Epinio

**If any of these feel uncertain or difficult, note it down — we will be meeting with you at the end of the two-week period to collect your feedback before go-live.**

---

**Thank you for participating in the beta test!**

Your feedback will be gathered in person and is critical to ensuring a smooth migration for all teams.
