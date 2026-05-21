# Migration from Epinio

Welcome! This guide helps you transition from Epinio to the Developer Portal.

## TL;DR - What You Need to Know

!!! success "Good News"
    1. **Your manifests convert automatically** - CD pipeline handles the conversion
    2. **Your routes stay the same** - Application URLs don't change
    3. **CI/CD mostly unchanged** - Only deployment target changes
    4. **One portal for all** - No more separate Epinio instances per platform
    5. **Keep using Grafana/Loki** - Primary tools for log analysis remain the same

## What's Changing?

### Before: Epinio
- Separate Epinio portal per platform
- Basic UI with limited features
- Synchronous operations
- Basic RBAC

### After: Mars Rover
- **Single portal** for all platforms and environments
- **Enhanced UI** with real-time updates and operation tracking
- **Async operations** with progress monitoring
- **Fine-grained RBAC** (4 roles: Admin, Lead, Developer, Viewer)

## Quick Comparison

| Action | Epinio UI | Mars Rover |
|---------|-----------|------------|
| Browse apps | Click platform link, view list | Select platform dropdown, select environment, view list |
| View app details | Click app name | Click app name (more detailed status) |
| View logs | Logs tab | Logs tab (enhanced streaming, but use Grafana for deep analysis) |
| Restart app | Restart button | Actions → Restart (with operation tracking) |
| Scale app | Scale control | Actions → Scale (with operation tracking) |
| Edit config | Edit form | Configuration → Edit (full YAML/JSON editor) |
| Delete app | Delete button | Actions → Delete (with confirmation) |

## Migration Process

### Step 1: Request Access

Before you can migrate, you need access to Mars Rover.

**Contact the MARS Platform Team** with:
- Your team name
- Required platforms (clusters)
- Environments you need access to (dev, qa, prod)

They'll assign you the appropriate role based on your responsibilities.

### Step 2: Migrate Your Application

For each application:

1. **Delete** the application from Epinio UI
2. **Trigger** your existing CD pipeline (no pipeline changes needed!)
3. **Automatic conversion**: Your Epinio manifest is converted automatically
4. **Deploy**: Application deploys to Mars Rover with same routes
5. **Verify**: Check application in the Developer Portal

!!! info "No Manual Changes"
    Your CI/CD pipeline includes a parser that automatically converts Epinio manifests to Mars Rover format. You don't need to edit your manifests manually.

### Step 3: Verify

After migration:

- ✅ Confirm application is running
- ✅ Verify routes work (URLs should be unchanged)
- ✅ Check logs in Mars Rover (quick checks)
- ✅ Verify logs in Grafana/Loki (historical analysis)
- ✅ Test application functionality

### Migration Timing

- **Simple stateless app**: 15-30 minutes
- **App with dependencies**: 30-60 minutes
- **Multiple apps**: Can migrate in parallel

## Key Differences to Know

### 1. Single Portal Access

**Epinio**: Separate portal per platform  
**Developer Portal**: One portal, select platform from dropdown

**Benefit**: One URL to remember, one login for everything

### 2. Operation Tracking

**Epinio**: Operations happen synchronously, limited feedback  
**Mars Rover**: Every operation returns an operation ID you can track

When you restart, scale, or update an app, you get an operation ID. Use it to:
- Monitor progress
- Check status
- View error messages if something fails

### 3. Enhanced Configuration Editor

**Epinio**: Basic form-based configuration  
**Mars Rover**: Full YAML/JSON manifest editor

You can now:
- Edit all configuration values in one view
- Get syntax validation
- See highlighting and auto-complete
- Access advanced chart options

### 4. Role-Based Access

**Epinio**: Basic access control  
**Mars Rover**: 4-tier role system

| Role | Can Do |
|------|--------|
| **Viewer** | View apps and logs only |
| **Developer** | + Create, update, restart, scale apps |
| **Lead** | + Delete applications |
| **Admin** | + Manage platform services |

### 5. Grafana & Loki Remain Primary

!!! warning "Important"
    Mars Rover provides quick log access during development, but **Grafana & Loki remain your primary tools** for:
    
    - Historical log analysis
    - Complex queries and filtering
    - Monitoring dashboards
    - Performance metrics
    - Alerting

Don't change your monitoring workflow - Mars Rover complements, doesn't replace, your existing tools.

## What's Better?

### ✅ Visual Dashboard
- Real-time status updates
- Advanced filtering and search
- Multiple sorting options
- Pagination for large app lists

### ✅ Operation Visibility
- Track every operation with an ID
- See progress in real-time
- View operation history
- Clear error messages

### ✅ Fine-Grained Permissions
- Team-based access control
- Role hierarchy
- Audit logging (who did what, when)

### ✅ Multi-Platform from One Place
- No more multiple bookmarks
- Single authentication
- Consistent interface across all platforms

## What's Different (Not Better or Worse)

### Configuration Management
- **Epinio**: Simple form fields
- **Mars Rover**: Full manifest editor

**Why the change**: More powerful for complex configurations, but requires knowing YAML syntax. You can copy/paste between apps easily.

### Service Connections
- **Both**: Manual configuration required
- **No change**: Neither platform auto-binds services

### Builds
- **Epinio**: Auto-builds from source
- **Mars Rover**: Pre-built images from Artifactory

**Your workflow**: CI builds image → Artifactory → Deploy via CD → Mars Rover. The build step moved to your CI pipeline (better separation of concerns).

## Common Questions

??? question "Do I need to change my application manifest?"
    **No!** The CD pipeline automatically converts Epinio manifests to Mars Rover format.

??? question "Will my routes (URLs) change?"
    **No.** Routes remain the same. Your applications will be accessible at the same URLs.

??? question "Do I need to rebuild my application?"
    **No.** If your image is already in Artifactory, the CD pipeline deploys it directly.

??? question "Do my CI/CD pipelines need major changes?"
    **Minimal changes.** Only the deployment target changes from Epinio to Mars Rover. Your build process stays the same.

??? question "Can I migrate one app at a time?"
    **Yes!** Migrate apps incrementally at your own pace.

??? question "What if I need different access or roles?"
    **Contact the MARS Platform Team.** They manage role assignments during migration.

??? question "How do I get help during migration?"
    Contact the MARS Platform Team via:
    
    - Email: mars-platformteam@maximus.com
    - For urgent issues: PagerDuty on-call engineer

## What to Test

After migrating your first app, verify:

- [ ] Application deploys successfully
- [ ] Routes work and application is accessible
- [ ] Logs appear in Mars Rover
- [ ] Can restart application
- [ ] Can scale application
- [ ] Can update configuration
- [ ] Historical logs still available in Grafana/Loki
- [ ] Monitoring dashboards still work

## Next Steps

1. **[Request Access](#step-1-request-access)** - Contact the platform team
2. **[Read the Quick Start](quick-start.md)** - Familiarize yourself with the interface
3. **[Review Beta Testing Guide](../beta-testing/testing-guide.md)** - If participating in beta
4. **[Detailed Migration Guide](../migration/migration-process.md)** - Step-by-step migration instructions
5. **[Feature Comparison](../migration/feature-comparison.md)** - Complete feature parity analysis

## Support During Migration

The Platform Team is here to help:

- **Email**: mars-platformteam@maximus.com for questions
- **Pair Programming**: Available for complex application migrations
- **Office Hours**: Weekly drop-in sessions during beta period
- **Documentation**: This guide and detailed references

---

!!! tip "Start Simple"
    Migrate a simple development application first to get comfortable with the process before moving production workloads.
