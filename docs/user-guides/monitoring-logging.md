# Monitoring & Logging

Learn how to monitor your applications and access logs using Mars Rover and complementary tools.

## Overview

Mars Rover provides quick-access monitoring for development, while **Grafana & Loki remain your primary tools** for comprehensive log analysis and monitoring.

## Quick Start

### View Real-Time Logs

1. Navigate to your application
2. Click **Logs** tab
3. Watch logs stream in real-time
4. Scroll to view history

**Use for**:
- Quick troubleshooting during development
- Immediate error identification
- Deployment verification

### Check Instance Health

1. Navigate to your application
2. Click **Instances** tab
3. Review instance status
4. Check restart counts

## Mars Rover Logs

### Features

- **Real-time streaming**: Logs update automatically
- **Multi-container support**: All containers in one view
- **Recent history**: Scrollback buffer for recent logs
- **Auto-reconnect**: Resilient to network issues

### Use Cases

✅ **Good for**:
- Quick checks during deployment
- Real-time debugging
- Immediate issue identification
- Development troubleshooting

❌ **Not ideal for**:
- Historical analysis (>1 hour ago)
- Complex log queries
- Performance trending
- Long-term monitoring

## Grafana & Loki

> **Primary Tools for Log Analysis**

### When to Use Grafana/Loki

**Always use for**:

- Historical log analysis
- Complex queries and filters
- Cross-application analysis
- Performance metrics and trends
- Monitoring dashboards
- Alerting and notifications
- Compliance and audit reporting

### Accessing Grafana

[Add your organization's Grafana URL and access instructions]

### Common Log Queries

[Add examples of useful Loki queries for your applications]

## Instance Health Monitoring

### Understanding Instance Status

| Status | Meaning | Action |
|--------|---------|--------|
| Running | Healthy, ready to serve traffic | None needed |
| Pending | Starting up | Wait a moment |
| Failed | Crashed or failing health checks | Check logs, verify config |
| Stopped | Manually stopped | Start when ready |

### Health Checks

Applications should implement:

- **Liveness probe**: Is the app alive?
- **Readiness probe**: Can the app serve traffic?
- **Startup probe**: Has the app finished starting?

### Resource Metrics

View CPU and memory usage:

1. Navigate to application
2. Check Instances tab
3. Enable metrics (if available)
4. Monitor resource consumption

## Operation Tracking

### Monitoring Operations

Every operation provides:

- **Operation ID**: Track progress
- **Status**: Pending/In Progress/Completed/Failed
- **Progress messages**: Step-by-step updates
- **Error details**: If something fails

### Operation History

View recent operations:

1. Navigate to application
2. Check Operations section
3. See last 24hours of operations
4. Click operation ID for details

## Best Practices

### Log Levels

Use appropriate log levels:

- **DEBUG**: Detailed diagnostic info
- **INFO**: General informational messages
- **WARN**: Warning messages
- **ERROR**: Error events
- **FATAL**: Critical errors

### Structured Logging

Log in JSON format for better parsing:

```json
{
  "timestamp": "2026-05-21T10:15:30Z",
  "level": "ERROR",
  "message": "Database connection failed",
  "error": "connection timeout",
  "retries": 3
}
```

### Monitoring Strategy

1. **Real-time**: Use Mars Rover for immediate issues
2. **Historical**: Use Grafana/Loki for analysis
3. **Alerts**: Configure in Grafana
4. **Dashboards**: Create in Grafana for your team

## Troubleshooting

### Logs Not Appearing

**In Mars Rover**:
- Refresh the page
- Check application is running
- Verify instances are healthy
- Try reconnecting

**In Grafana/Loki**:
- Check time range
- Verify log shipping
- Contact platform team

### High Restart Counts

Indicates problems:
1. Check logs for crash reasons
2. Verify health checks
3. Review resource limits
4. Check for configuration issues

## Next Steps

- **[Configuration Management](configuration.md)** - Tune your app settings
- **[Application Management](application-management.md)** - Manage lifecycle
- **[Troubleshooting](../reference/troubleshooting.md)** - Solve common issues
