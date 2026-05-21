# Application Management

This guide covers all aspects of managing applications in the Developer Portal.

## Overview

Mars Rover provides a comprehensive set of tools for managing your applications throughout their lifecycle.

## Viewing Applications

### Browsing Applications

1. Select platform from dropdown
2. Select environment from dropdown
3. View list of applications

**Features**:
- Search by name
- Sort by various fields
- Pagination for large lists
- Status indicators

### Application Details

Click on an application to view:

- Status and health
- Running instances
- Routes (URLs)
- Configuration
- Recent operations

## Creating Applications

> **Note**: Most applications are deployed via CI/CD pipelines. This section is for manual deployments.

**Requirements**: Developer, Lead, or Admin role

**Steps**:
1. Click "Create Application"
2. Enter application name
3. Provide deployment chart details
4. Configure initial settings
5. Track deployment via operation ID

## Managing Application Lifecycle

### Restarting Applications

Perform a rolling restart:

1. Navigate to application
2. Click Actions → Restart
3. Confirm action
4. Track using operation ID

**Expected duration**: 20-60 seconds

### Scaling Applications

Adjust the number of instances:

1. Navigate to application
2. Click Actions → Scale
3. Enter target instance count
4. Confirm
5. Track using operation ID

**Expected duration**: 15-45 seconds

### Stopping Applications

Temporarily stop an application:

1. Navigate to application
2. Click Actions → Stop
3. Confirm action
4. All instances will shut down

**Use cases**: Maintenance, cost savings, troubleshooting

### Starting Applications

Resume a stopped application:

1. Navigate to stopped application
2. Click Actions → Start
3. Wait for instances to start
4. Verify application is accessible

## Updating Configuration

See [Configuration Management](configuration.md) for detailed information on updating application settings.

## Deleting Applications

> **Warning**: Deletion is permanent and cannot be undone!

**Requirements**: Lead or Admin role

**Steps**:
1. Navigate to application
2. Click Actions → Delete
3. Read warning carefully
4. Confirm deletion
5. Track using operation ID

**What gets deleted**:
- Helm release
- Platform resources
- Running instances
- Configuration (manifest)

**What persists**:
- Historical logs in Grafana/Loki
- Audit trail
- Artifactory images

## Monitoring Applications

### Instance Health

View detailed instance status:

- Running/Stopped/Failed instances
- Restart counts
- Creation timestamps
- Container states

### Logs

Quick log access for development:

1. Navigate to application
2. Click Logs tab
3. View real-time streaming

**For deep analysis**: Use Grafana & Loki

### Operations History

Track recent operations:

- Operation type
- Status (pending/in-progress/completed/failed)
- Timestamps
- Error messages

## Best Practices

### Naming Conventions

- Use lowercase names
- Include environment prefix if needed
- Keep names short and descriptive
- Avoid special characters

### Scaling Strategy

- Start with minimum replicas
- Scale up based on load
- Consider resource limits
- Plan for peak traffic

### Configuration Changes

- Test in dev environment first
- Update one environment at a time
- Verify after each change
- Keep configuration in version control

### Security

- Never hardcode secrets
- Use platform-managed secrets
- Review access logs regularly
- Follow principle of least privilege

## Troubleshooting

### Common Issues

**Application won't start**:
- Check logs for errors
- Verify configuration
- Check resource limits
- Review instance events

**Scale operation fails**:
- Check resource quotas
- Verify instance limits
- Review cluster capacity
- Contact platform team

**Configuration update doesn't apply**:
- Verify operation completed
- Check manifest syntax
- Review restart logs
- Confirm no conflicts

## Next Steps

- **[Monitoring & Logging](monitoring-logging.md)** - Deep dive into monitoring
- **[Configuration Management](configuration.md)** - Advanced configuration
- **[Troubleshooting Guide](../reference/troubleshooting.md)** - Solve common issues
