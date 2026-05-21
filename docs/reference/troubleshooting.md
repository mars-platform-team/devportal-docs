# Troubleshooting

Common issues and solutions for the Developer Portal.

## Quick Troubleshooting

### Can't Login

**Symptoms**: Login fails or redirects to error page

**Solutions**:
1. Clear browser cache and cookies
2. Try incognito/private browsing mode
3. Verify you're using company Microsoft account
4. Check with platform team if account needs provisioning

### Can't See My Applications

**Symptoms**: Application list is empty

**Check**:
- Correct platform selected?
- Correct environment selected?
- Do you have access to this environment?
- Are applications actually deployed here?

**Solutions**:
1. Switch to different platform/environment
2. Request access from platform team
3. Verify applications exist in this environment
4. Check "My Access" panel for permissions

### Application Won't Start

**Symptoms**: Application stuck in "Pending" or shows "Failed"

**Diagnose**:
1. Check Logs tab for error messages
2. Review Instances tab for specific failures
3. Check operation history for errors

**Common causes**:
- Invalid configuration
- Missing secrets/config maps
- Insufficient resources
- Image pull errors
- Health check failures

**Solutions**:
1. Fix configuration errors
2. Verify secrets exist
3. Check resource quotas
4. Verify image exists in Artifactory
5. Adjust health check timing

### Logs Not Showing

**Symptoms**: Logs tab is blank or not updating

**Solutions**:
1. Refresh the page
2. Check that application is running
3. Verify instances are healthy
4. Close and reopen Logs tab
5. Try in different browser

### Configuration Change Didn't Work

**Symptoms**: Updated configuration but app behavior unchanged

**Check**:
1. Did operation complete successfully?
2. Did application restart?
3. Is the configuration actually updated in Configuration tab?

**Solutions**:
1. Check operation status
2. Manually restart application
3. Verify YAML syntax was valid
4. Review logs for configuration errors

### Can't Perform an Action

**Symptoms**: Button is grayed out or action returns "Permission Denied"

**Check your role**:
- Viewer: Read-only
- Developer: Can't delete apps
- Lead: Full app management
- Admin: Full platform access

**Solution**: Request appropriate role from platform team

### Operation Taking Too Long

**Expected times**:
- Restart: 20-60 seconds
- Scale: 15-45 seconds
- Update config: 20-60 seconds
- Deploy: 1-3 minutes

**If exceeded**:
1. Note operation ID
2. Check operation status
3. Contact platform team if > 5 minutes

## Error Messages

### "Conflict: Another operation in progress"

**Meaning**: An operation is already running on this application

**Solution**: Wait for current operation to complete, then retry

### "Not Found: Application does not exist"

**Meaning**: Application not deployed or was deleted

**Solution**: Verify application name and environment, redeploy if needed

### "Forbidden: Insufficient permissions"

**Meaning**: Your role doesn't allow this action

**Solution**: Request role upgrade from platform team

### "Bad Request: Invalid configuration"

**Meaning**: Configuration has syntax or validation errors

**Solution**: Check YAML syntax, fix errors, retry

### "Service Unavailable"

**Meaning**: Backend service or platform issue

**Solution**: Contact platform team immediately

## Performance Issues

### Slow Page Load

**Solutions**:
1. Check internet connection
2. Clear browser cache
3. Try different browser
4. Contact platform team if persistent

### Logs Lag Behind

**Expected**: < 2 seconds delay

**If longer**:
1. Refresh connection
2. Close and reopen Logs tab
3. Use Grafana/Loki for historical analysis
4. Report to platform team

## Migration Issues

### Application Different After Migration

**Check**:
- Configuration differences
- Environment variables
- Resource limits
- Health check settings

**Solution**: Compare Epinio and Mars Rover configurations

### Routes Not Working After Migration

**Check**:
- DNS resolution
- TLS certificates
- Ingress configuration
- Network policies

**Solution**: Verify route configuration in manifest

## Getting Help

### Self-Service

1. Check this troubleshooting guide
2. Search documentation
3. Review [FAQ](../migration/faq.md)
4. Check operation history for error details

### Platform Team Support

**Email**: mars-platformteam@maximus.com
- For questions and detailed technical issues
- < 2 hour response during business hours
- Include: logs, operation IDs, screenshots

**PagerDuty** (Emergency Only)
- Production-down situations only
- Include: timestamp, application, environment, impact

### What to Include in Support Requests

Always provide:
- **Timestamp**: When issue occurred
- **Application**: Name and environment
- **Operation ID**: If applicable
- **Error messages**: Exact text
- **What you tried**: Steps already taken
- **Expected vs Actual**: What should happen vs what did happen

## Status Page

[Add link to internal status page if available]

Check for:
- Platform outages
- Scheduled maintenance
- Known issues

## Next Steps

- **[FAQ](../migration/faq.md)** - Common questions
- **[Support](support.md)** - Contact information
- **[Application Management](../user-guides/application-management.md)** - Learn proper workflows
