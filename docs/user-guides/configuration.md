# Configuration Management

Learn how to view and update application configurations in Mars Rover.

## Overview

Mars Rover provides a full YAML/JSON manifest editor for updating application configuration. This replaces Epinio's form-based configuration with more powerful editing capabilities.

## Viewing Configuration

### Current Configuration

1. Navigate to your application
2. Click **Configuration** tab
3. View current manifest

**Available formats**:
- JSON (structured view)
- YAML (deployment format)

### Downloading Configuration

Click **Download** to save:
- As backup before changes
- For version control
- To copy to another app

## Editing Configuration

**Requirements**: Developer, Lead, or Admin role

### Basic Editing Flow

1. Navigate to application
2. Click Configuration → **Edit**
3. Modify values
4. **Validate** syntax (automatic)
5. **Save** changes
6. Track operation via operation ID
7. Wait for application restart

### Common Configuration Changes

#### Environment Variables

```yaml
env:
  - name: LOG_LEVEL
    value: "debug"
  - name: DATABASE_URL
    valueFrom:
      secretKeyRef:
        name: db-credentials
        key: url
```

#### Instance Count (Replicas)

```yaml
replicaCount: 3
```

#### Resource Limits

```yaml
resources:
  limits:
    cpu: "1000m"
    memory: "512Mi"
  requests:
    cpu: "100m"
    memory: "128Mi"
```

#### Routes (Ingress)

```yaml
ingress:
  enabled: true
  hosts:
    - host: myapp.example.com
      paths:
        - path: /
          pathType: Prefix
```

## Best Practices

### Before Editing

- Review current configuration
- Know what you want to change
- Have rollback plan
- Test in dev first

### While Editing

- Change one thing at a time
- Use valid YAML syntax
- Reference secrets, don't hardcode
- Comment your changes

### After Editing

- Verify operation completes
- Check logs for errors
- Test application functionality
- Monitor for issues

## Advanced Configuration

### Using Secrets

**Never hardcode sensitive values!**

```yaml
env:
  - name: API_KEY
    valueFrom:
      secretKeyRef:
        name: app-secrets
        key: api-key
```

### ConfigMaps

Reference external configuration:

```yaml
env:
  - name: APP_CONFIG
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: config.json
```

### Health Probes

Configure liveness, readiness, and startup probes:

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

## Troubleshooting

### Validation Errors

- Check YAML syntax
- Verify indentation
- Ensure quotes match
- Review error messages

### Changes Don't Apply

- Check operation status
- Verify operation completed
- Review update logs
- Try manual restart

### Application Won't Start After Update

- Check logs for errors
- Verify configuration changes
- Consider rollback
- Contact platform team

## Next Steps

- **[Application Management](application-management.md)** - Manage lifecycle
- **[Monitoring & Logging](monitoring-logging.md)** - Monitor your apps
- **[Troubleshooting](../reference/troubleshooting.md)** - Solve issues
