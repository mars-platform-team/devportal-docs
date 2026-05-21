# Frequently Asked Questions (FAQ)

Common questions about the Developer Portal and the Epinio migration.

## General Questions

### What is the Developer Portal?

The Developer Portal is a Backstage-based platform that provides a unified interface for managing applications across all platforms and environments. It replaces Epinio for application deployment and management.

### Why are we moving from Epinio?

The migration provides several benefits:

- **Unified Portal**: One interface for all platforms vs. separate Epinio instances per platform
- **Enhanced RBAC**: Fine-grained role-based access control (4 tiers)
- **Better Visibility**: Operation tracking, audit logging, detailed monitoring
- **Enterprise Integration**: Microsoft OAuth, Azure AD groups, Jenkins integration
- **Improved UX**: Modern interface with real-time updates and advanced features

### Is the portal production-ready?

Yes! The platform is currently in beta testing and will be production-ready after incorporating beta feedback. The platform team is available to support migration.

---

## Access & Permissions

### How do I get access to the portal?

Contact the MARS Platform Team via email at mars-platformteam@maximus.com with:

- Your team name
- Required platforms (clusters)
- Environments you need (dev, qa, prod)

They'll assign you the appropriate role based on your responsibilities.

### What are the different roles?

| Role | Description | Typical Users |
|------|-------------|---------------|
| **Admin** | Full access to all features including platform service management | Platform team, operations |
| **Lead** | Can manage applications including deletion | Tech leads, senior developers |
| **Developer** | Can deploy, update, restart, and scale applications | Application developers |
| **Viewer** | Read-only access to view applications and logs | Stakeholders, support teams |

### Can I have different roles for different platforms?

Yes! Role assignments are per-team and per-platform. You might be a Lead for your team's applications but a Viewer for platform services.

### I don't see the platform/environment I need. What do I do?

Contact the MARS Platform Team to request access to additional platforms or environments.

---

## Migration Questions

### Do I need to change my application manifests?

**No!** The CD pipeline includes an automatic parser that converts Epinio manifests to Mars Rover format. Your existing manifests work without manual changes.

### Will my application routes (URLs) change?

**No.** Routes are defined in your configuration and remain the same. Your applications will be accessible at the same URLs after migration.

### Do I need to rebuild my applications?

**No.** If your images are already in Artifactory, the CD pipeline deploys them directly to Mars Rover.

### Do my CI/CD pipelines need major changes?

**Minimal changes required.** Only the deployment target changes from Epinio to Mars Rover. Your build process and pipeline structure remain the same.

### Can I migrate one application at a time?

**Yes!** You can migrate applications incrementally at your own pace. We recommend starting with development environment applications.

### What if something goes wrong during migration?

You can rollback to Epinio by redeploying via your old CD job. Contact the platform team for assistance if needed.

### How long does migration take per application?

- Simple stateless app: 15-30 minutes
- App with dependencies: 30-60 minutes
- Complex applications: 1-2 hours

### Can I test before fully migrating?

Yes! Start with development environment applications. Beta testers can also use test environments provided by the platform team.

---

## Using Mars Rover

### How do I access multiple platforms?

Use the platform dropdown at the top of the application management interface to switch between platforms. No need for separate URLs - it's all in one portal.

### Where are my application logs?

**Quick troubleshooting**: Use the Logs tab in the Developer Portal for real-time viewing  
**Deep analysis**: Continue using Grafana & Loki for historical logs, complex queries, and dashboards

### What happened to Grafana and Loki?

**They're still your primary tools!** The Developer Portal complements (doesn't replace) Grafana & Loki. Use the portal for quick log checks during development, and Grafana/Loki for:

- Historical log analysis
- Complex queries and filtering
- Monitoring dashboards
- Performance metrics
- Alerting

### How do I track operations?

Every operation (restart, scale, update, etc.) returns an operation ID. Use it to:

- Monitor progress in real-time
- Check status later
- View error messages if something fails

### Do I need direct cluster access?

No! The platform handles all deployment operations for you. You don't need kubectl or direct cluster access - everything is managed through the Developer Portal interface.

### How do I update my application configuration?

1. Click on your application
2. Go to Configuration tab
3. Click Edit
4. Update YAML/JSON manifest
5. Save changes
6. Track the update operation

### Can I delete applications?

Only users with **Lead** or **Admin** roles can delete applications. Deletion is permanent and cannot be undone.

---

## Troubleshooting

### My application won't start

1. Check logs in Mars Rover Logs tab
2. Verify configuration (env vars, ports, resources)
3. Check instance health status in Instances tab
4. Review error messages in operations history
5. Contact platform team if issue persists

### I can't perform an action (getting "Permission denied")

Check your role. Some actions require higher privileges:

- **Delete apps**: Requires Lead or Admin role
- **Manage platform services**: Requires Admin role

Contact platform team if you need a role change.

### Operation is taking too long

- Most operations complete in 30-60 seconds
- Scaling many instances: up to 90 seconds
- If > 2 minutes: Note the operation ID and contact platform team

### Configuration change didn't take effect

1. Check operation status - did it complete successfully?
2. View current configuration - verify your changes are there
3. Check logs for errors after restart
4. Verify YAML/JSON syntax was valid

---

## Technical Questions

### What happens to my application during a restart?

The platform performs a **rolling restart**:

- New instances start before old ones stop
- Zero downtime for multi-instance apps
- Single-instance apps have brief downtime (~30 seconds)

### How is RBAC implemented?

Access control uses:

### What CI/CD systems are supported?

Currently integrated with **Jenkins**. The platform executes deployments via Jenkins CD jobs. Support for other CI/CD systems may be added based on demand.

### How does the manifest conversion work?

The CD pipeline includes automation that:

1. Reads your Epinio manifest
2. Translates to the new platform format
3. Deploys to the target environment
4. No manual conversion needed

### Can I see the converted manifest?

Yes! After deployment, view the Configuration tab in the application management interface to see the actual deployed manifest.

---

## Getting Help

### Who do I contact for support?

**Platform Team**:
- Email: mars-platformteam@maximus.com

**Emergency** (production issues only):
- PagerDuty on-call engineer

### Where can I find more documentation?

- **[Quick Start Guide](../getting-started/quick-start.md)** - Get started quickly
- **[Migration Process](migration-process.md)** - Step-by-step migration
- **[Feature Comparison](feature-comparison.md)** - Detailed feature analysis
- **[Troubleshooting](../reference/troubleshooting.md)** - Common issues and solutions

### How do I report a bug or request a feature?

Contact the platform team via email at mars-platformteam@maximus.com with a detailed description.

### Is there training available?

Yes! The platform team provides:

- Written documentation (this site)
- Video walkthroughs (check internal wiki)
- Office hours during beta period
- Pair programming for complex migrations

---

## Beta Testing

### How do I participate in beta testing?

Contact the MARS Platform Team expressing interest. They'll provide access and testing guidance.

### What should I test?

See the comprehensive [Beta Testing Guide](../beta-testing/testing-guide.md) for a detailed checklist of test scenarios.

### How do I submit feedback?

Send your feedback to mars-platformteam@maximus.com with details about your experience, issues encountered, or improvement suggestions.

---

## Other Questions?

If your question isn't answered here:

1. Check the [Troubleshooting Guide](../reference/troubleshooting.md)
2. Search the documentation using the search bar
3. Contact the platform team via email at mars-platformteam@maximus.com

---

*Last updated: May 21, 2026*
