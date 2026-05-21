# Developer Portal Documentation

Welcome to the Developer Portal documentation! This portal provides a unified interface for managing applications across all your platforms and environments.

## 🚀 What is the Developer Portal?

The Developer Portal is a Backstage-based platform that replaces Epinio for application deployment and management. It provides:

- **Unified Access**: One portal for all platforms and environments
- **Application Management**: Deploy, configure, scale, and monitor your applications
- **Role-Based Access**: Fine-grained permissions based on your team and role
- **CI/CD Integration**: Seamless integration with Jenkins pipelines
- **Real-Time Monitoring**: View logs, check health, and track operations

## 📖 Quick Navigation

### New to the Portal?
Start here to get up and running quickly:

- **[Quick Start Guide](getting-started/quick-start.md)** - Get started in 5 minutes
- **[First Login](getting-started/first-login.md)** - Initial setup and navigation
- **[Migration from Epinio](getting-started/migration-guide.md)** - Transitioning from Epinio

### Coming from Epinio?
Everything you need to know about the migration:

- **[Feature Comparison](migration/feature-comparison.md)** - What's changed, what's better
- **[Migration Process](migration/migration-process.md)** - Step-by-step migration guide
- **[Migration FAQ](migration/faq.md)** - Common questions answered

### Daily Operations
Guides for common tasks:

- **[Application Management](user-guides/application-management.md)** - Deploy, restart, scale, delete apps
- **[Monitoring & Logging](user-guides/monitoring-logging.md)** - View logs and monitor health
- **[Configuration Management](user-guides/configuration.md)** - Update app settings
- **[Role-Based Access](user-guides/rbac.md)** - Understanding permissions

### Beta Testing
Help us improve before launch:

- **[Beta Testing Guide](beta-testing/testing-guide.md)** - Comprehensive testing checklist

### Need Help?
- **[Troubleshooting](reference/troubleshooting.md)** - Common issues and solutions
- **[Glossary](reference/glossary.md)** - Terms and definitions
- **[Support](reference/support.md)** - How to get help

## 🔑 Key Features

### Single Portal, All Environments
No more juggling multiple Epinio instances. Access all your platforms and environments from one place with a single login.

### Automated Manifest Conversion
Your CD pipeline automatically converts Epinio manifests to DevPortal format - no manual changes needed.

### Enhanced Monitoring
DevPortal provides quick log access for development, while Grafana & Loki remain your primary tools for deep analysis and monitoring.

### Fine-Grained RBAC
Four-tier role system (Admin, Lead, Developer, Viewer) with team-based access control via Azure AD.

## 🎯 Migration Status

!!! success "Ready for Beta Testing"
    The platform is ready for beta testing. Contact the MARS Platform Team to request access.

### Migration Timeline
- **Week 1**: Read-only testing (view apps, logs, monitoring)
- **Week 2-3**: Full testing (deploy, update, manage applications)
- **Week 4**: Production-like workloads and feedback collection
- **Go-Live**: After beta feedback incorporation and sign-off

## 📋 Before You Start

### Request Access
Contact the MARS Platform Team with:
- Your team name
- Required platforms (clusters)
- Environments you need (dev, qa, prod)

### What to Know
1. **Manifest conversion is automatic** - CD pipeline handles it
2. **Routes don't change** - Application URLs remain the same
3. **CI/CD process stays the same** - Only deployment target changes
4. **Keep using Grafana/Loki** - For deep log analysis and monitoring

## 🤝 Getting Support

**Platform Team Contact**:
- Email: mars-platformteam@maximus.com

**For Urgent Issues**:
- Contact on-call engineer via PagerDuty
- Include: timestamp, operation ID, application name, environment

## 📚 Additional Resources

- [DevPortal Rover Service](https://github.com/mars-platform-team/devportal-rover-service) - Backend API service
- [MARS Platform Documentation](https://github.com/mars-platform-team) - Additional platform resources
- [Software Templates](https://github.com/mars-platform-team/idp-software-templates) - Create new apps from templates

---

!!! tip "Quick Start"
    Ready to dive in? Head to the [Quick Start Guide](getting-started/quick-start.md) to begin!
