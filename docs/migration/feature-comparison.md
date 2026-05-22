# Epinio to Developer Portal Migration: Feature Comparison

## Executive Summary

The Developer Portal (Backstage-based) replaces Epinio as the application deployment and management platform. This document outlines feature parity, enhancements, and known differences.

**Note**: This comparison is based on Epinio web UI usage (not CLI), which is how developers currently interact with Epinio.

**Migration Status**: ✅ Ready for Beta Testing

---

## Migration Expectations

### What Changes During Migration

#### 1. **Application Manifests (Automated Conversion)**
- **What's Changing**: Manifest format is different between Epinio and DevPortal
- **What We're Doing**: CI/CD pipelines include an automated parser that converts Epinio manifests to DevPortal format
- **Developer Action**: None required - conversion happens automatically in your CD pipeline
- **Result**: Your existing Epinio manifests continue to work without manual changes

#### 2. **Application Deployment Process**
- **What's Required**: Applications must be deleted from Epinio and redeployed via CD pipeline to DevPortal
- **Why**: Clean migration ensures proper DevPortal configuration and tracking
- **Process**:
  1. Delete application from Epinio UI
  2. Trigger your CD pipeline (targeting DevPortal)
  3. Application deploys to DevPortal with converted manifest
- **Routes**: Your application routes (URLs) remain unchanged

#### 3. **CI/CD Pipelines (Minimal Change)**
- **What's Changing**: CD job target changes from Epinio to DevPortal
- **What's Staying Same**: Build process, pipeline structure, triggers, and workflow
- **Impact**: Your CI builds images the same way; only the deployment target changes
- **Benefit**: No need to reconfigure Jenkins jobs or build processes

#### 4. **Access & Role Management**
- **Initial Setup**: MARS Platform Team manages role assignments during migration
- **How to Get Access**: Contact the MARS Platform Team at mars-platformteam@maximus.com with:
  - Your team name
  - Required platforms/environments
- **Role Assignment**: Based on your team responsibilities and Azure AD Security Groups
- **Future**: Self-service role management planned for post-migration

#### 5. **Single Portal for All Environments**
- **What's Changing**: Instead of separate Epinio instances per platform, one unified DevPortal
- **Access Model**: 
  - Single login (Microsoft OAuth)
  - Select platform (cluster) from dropdown
  - Select environment from dropdown
  - Access controlled via Azure AD Security Groups + App Roles
- **Benefit**: No need to remember multiple URLs; centralized application management

#### 6. **Monitoring & Log Analysis**
- **Primary Tools**: **Grafana & Loki remain your primary tools** for log analysis and monitoring
- **DevPortal Logs**: Available for quick troubleshooting and real-time viewing
- **Use DevPortal For**: 
  - Quick log checks during deployments
  - Real-time debugging during development
  - Immediate issue identification
- **Use Grafana/Loki For**:
  - Historical log analysis
  - Complex queries and filters
  - Dashboards and alerting
  - Performance metrics and trends
- **Important**: DevPortal log viewer is a convenience feature, not a replacement for Grafana/Loki

---

## Feature Parity Matrix

| Feature Category | Epinio UI | Backstage + Rover | Status | Notes |
|------------------|--------|-------------------|--------|-------|
| **Application Discovery** |
| List applications | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Pagination, sorting, search |
| View application details | ✅ Web UI | ✅ Web UI | ✅ Enhanced | More detailed status |
| Filter/search apps | ✅ Basic | ✅ Full-text | ✅ Better | Advanced search and filtering |
| **Application Management** |
| Create/deploy application | ✅ Web UI | ✅ Web UI | ✅ Equivalent | Helm-based deployment |
| Update configuration | ✅ Web UI | ✅ Manifest editor | ✅ Enhanced | Full YAML/JSON editing |
| Delete application | ✅ Web UI | ✅ Web UI | ✅ Equivalent | With confirmation dialog |
| Restart application | ✅ Web UI | ✅ Web UI | ✅ Equivalent | Rolling restart |
| Scale instances | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Visual controls with tracking |
| Stop/start application | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Explicit actions with tracking |
| **Monitoring & Logs** |
| View logs | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Real-time streaming |
| Stream logs | ✅ Web UI | ✅ WebSocket | ✅ Better | Low latency |
| Historical logs | ✅ Web UI | ✅ Web UI | ✅ Equivalent | Scrollback buffer |
| Multi-container logs | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Automatic aggregation |
| Terminal access | ✅ Web UI | ✅ WebSocket | ✅ Equivalent | Interactive web terminal |
| Resource metrics | Limited | ✅ CPU/Memory | ✅ Better | Via Metrics Server |
| Instance health | Basic | ✅ Detailed | ✅ Better | Per-container status |
| **Configuration** |
| Environment variables | ✅ Web UI | ✅ Web UI | ✅ Enhanced | Full manifest editor |
| Chart values | ✅ Web UI | ✅ YAML/JSON | ✅ Enhanced | Full manifest access |
| Secrets management | ✅ Manual | ✅ Manual | ✅ Equivalent | Via platform-managed secrets |
| ConfigMaps | ✅ Manual | ✅ Manual | ✅ Equivalent | Via configuration values |
| **Services & Bindings** |
| Service connections | ✅ Manual config | ✅ Manual config | ✅ Equivalent | Configure in manifest |
| Database connections | ✅ Manual config | ✅ Manual config | ✅ Equivalent | Set connection strings in env vars |
| **Build & Deploy** |
| Build from source | ✅ Paketo | ❌ N/A | ⚠️ Different | Use CI pipeline |
| Dockerfile support | ✅ Built-in | ❌ N/A | ⚠️ Different | Build via Jenkins |
| Pre-built image deploy | ✅ Web UI | ✅ Web UI | ✅ Equivalent | Primary workflow |
| Version selection | ✅ Manual entry | ✅ Browser | ✅ Better | Browse available versions |
| CI/CD integration | External | ✅ Jenkins | ✅ Better | Built-in pipeline trigger |
| **Access Control** |
| Multi-tenant | ✅ Environments | ✅ Environments | ✅ Equivalent | Isolated environments |
| Basic auth | ✅ Simple | ✅ Microsoft OAuth | ✅ Better | Enterprise SSO |
| RBAC | Basic | ✅ 4-tier roles | ✅ Better | Admin/Lead/Developer/Viewer |
| Team-based access | Limited | ✅ Team scoping | ✅ Better | Azure AD App Roles |
| Audit logging | ❌ None | ✅ Full | ✅ New | Compliance ready |
| **Operations** |
| Async operations | ❌ Blocking | ✅ Background | ✅ Better | Track via operation ID |
| Operation tracking | ❌ N/A | ✅ Status API | ✅ New | Progress monitoring |
| Operation history | ❌ N/A | ✅ Per-app | ✅ New | Last 24 hours |
| Conflict detection | ❌ N/A | ✅ Automatic | ✅ New | Prevents concurrent ops |

---

## Legend

- ✅ **Equivalent or Better** - Feature parity achieved or improved
- ⚠️ **Different Approach** - Similar outcome, different method
- ❌ **Not Supported** - Feature not available in new platform
- 🔄 **Planned** - On roadmap for future release

---

## What's Better in Backstage + Rover

### 1. **Enhanced Visual Dashboard**
- **Epinio UI**: Basic web interface
- **Rover**: Rich web UI with real-time updates, advanced filtering, operation tracking

### 2. **Fine-Grained Access Control**
- **Epinio**: Basic environment isolation
- **Rover**: 4-tier RBAC (Admin/Lead/Developer/Viewer) with team scoping

### 3. **Operation Visibility**
- **Epinio**: Synchronous operations, basic status
- **Rover**: Async operations with progress tracking, operation history, detailed status

### 4. **Enhanced Monitoring**
- **Epinio**: Basic log viewing
- **Rover**: Real-time log streaming, detailed instance health, resource metrics
- **Note**: Grafana & Loki remain the primary tools for log analysis and monitoring; DevPortal provides quick-access logs for development and troubleshooting

### 5. **Configuration Management**
- **Epinio**: Basic form-based configuration
- **Rover**: Full manifest editor with validation, JSON/YAML support, syntax highlighting

### 6. **Audit & Compliance**
- **Epinio**: No audit trail
- **Rover**: Full audit logging (who did what, when)

### 7. **CI/CD Integration**
- **Epinio**: External tooling
- **Rover**: Built-in Jenkins integration, artifact browsing

### 8. **Unified Multi-Platform Access**
- **Epinio**: Separate portal per platform/cluster
- **Rover**: Single portal for all platforms and environments
- **Benefit**: One login, one URL - access all your applications across all clusters

---

## What Works Differently

### 1. **Configuration Updates**

**Epinio UI Approach:**
- Edit configuration via web forms
- Update individual values one at a time
- Limited to common configuration options

**Rover Approach:**
- Full manifest editor (YAML/JSON)
- Edit all values in one view
- Access to all deployment configuration values
- Syntax validation and highlighting

**Why**: More powerful for complex configurations, single-operation updates

---

### 2. **Service Connections**

**Both Platforms:**
Manually configure service connections in application configuration. Neither platform uses automatic service bindings.

**Best Practice** (same for both):
```yaml
env:
  - name: DB_HOST
    valueFrom:
      secretKeyRef:
        name: mydb-secret
        key: host
```

**Why**: Explicit configuration provides better control and auditability

---

### 3. **Builds**

**Epinio Approach:**
- Auto-builds from source code (Paketo buildpacks)
- Detects language and creates container image
- Immediate deployment after build

**Rover Approach:**
- CI pipeline builds image → Artifactory
- Browse available versions in UI
- Deploy selected version

**Why**: Separation of build and deploy, better for enterprise CI/CD workflows

---

## What's Not Supported (and Workarounds)

### ❌ Automatic Builds from Source

**Workaround**: 
- Use Jenkins CI pipeline to build container images
- Push to Artifactory
- Deploy pre-built images via Rover

**Impact**: Extra setup step, but more control over build process and better separation of concerns

---

### ❌ Auto-scaling

**Workaround**:
- Manually scale via UI based on load
- Future: Auto-scaling support planned

**Impact**: Requires manual monitoring and scaling

---

## Migration Path for Developers

### Actual Migration Process

#### Step 1: Request Access
1. Contact MARS Platform Team for access
2. Provide: team name, platforms needed, environments required
3. Wait for role assignment confirmation via Azure AD Security Groups

#### Step 2: Migrate Your Application
1. **Delete** your application from Epinio UI
2. **Trigger** your existing CD pipeline (no changes needed to the pipeline itself)
3. **Automatic conversion**: CD pipeline parser converts your Epinio manifest to DevPortal format
4. **Deploy**: Application deploys to DevPortal with same routes/configuration
5. **Verify**: Check application in DevPortal UI

#### Step 3: Validate
- Confirm application is running
- Verify routes work (URLs unchanged)
- Check logs and monitoring in DevPortal and Grafana
- Test any application-specific functionality

### Migration Timing

**Simple apps (stateless)**: 15-30 minutes per app  
**Apps with dependencies**: 30-60 minutes per app  
**Multiple apps**: Can be done in parallel by different team members

---

## Common Migration Questions

### Q: Do I need to change my application manifest?
**A**: No! The CD pipeline includes an automatic parser that converts Epinio manifests to DevPortal format. Your existing manifests work without changes.

### Q: Do I need to rebuild my application?
**A**: No. If your image is in Artifactory, the CD pipeline deploys it directly to DevPortal.

### Q: Will my routes (URLs) change?
**A**: No. Routes remain the same. Your application will be accessible at the same URLs after migration.

### Q: Do I need to change my CI/CD pipelines?
**A**: Minimal changes. The CD job target changes from Epinio to DevPortal, but your build process and pipeline structure remain the same.

### Q: Can I migrate one app at a time?
**A**: Yes! You can migrate applications incrementally. Delete from Epinio, redeploy to DevPortal via CD pipeline.

### Q: What if I need access to additional platforms or environments?
**A**: Contact the MARS Platform Team. They manage role assignments during the migration period.

### Q: How do I access my applications after migration?
**A**: Single DevPortal URL → Login with Microsoft account → Select platform → Select environment → View your apps.

### Q: Will I lose my logs and monitoring during migration?
**A**: Historical logs remain in Loki/Grafana. New logs will be in both DevPortal and Grafana/Loki after redeployment.

### Q: How do secrets work?
**A**: Same as Epinio - use platform-managed secrets and reference them in your manifest. Both platforms require manual secret configuration.

### Q: Do I need direct access to the platform infrastructure?
**A**: No! Platform automation handles all deployment operations. You manage applications through the Developer Portal interface - no direct access needed.

---

## Beta Testing Focus Areas

Given the differences above, please focus beta testing on:

1. ✅ **Core workflows**: Deploy, configure, restart, scale
2. ✅ **Monitoring**: Logs, instance health, metrics
3. ✅ **Access control**: Verify role-based permissions work correctly
4. ✅ **Configuration management**: Test apps with many env vars or complex configs
5. ✅ **Multi-instance apps**: Ensure scaling and load distribution work
6. ⚠️ **Build pipeline integration**: Verify artifact browsing and version selection

**Out of Scope for Beta:**
- Build pipeline setup (handled separately)
- Auto-scaling configuration

---

## Timeline & Support

**Beta Testing Phase**: You have **two weeks** to explore and test the portal at your own pace. At the end of the two-week period, we'll collect your feedback before making a go-live decision.

**Migration Support**:
- Platform team available for questions
- Migration guides for common app types
- Pair programming sessions for complex apps

**Go-Live**: After beta feedback incorporated and sign-off

---

## Feedback Channels

| Issue Type | Where to Report |
|------------|-----------------|
| Feature not working | Operation ID + details to platform team |
| Feature request | Email the platform team |
| Documentation gap | Comment on specific guide |
| Security concern | Direct escalation to security team |

---

**Last Updated**: May 21, 2026  
**Document Owner**: Platform Engineering Team
