# Role-Based Access Control (RBAC)

Understanding permissions and access control in Mars Rover.

## Overview

Mars Rover uses a 4-tier role system with team-based access control to ensure secure and appropriate access to applications and platforms.

## Role Hierarchy

```
Admin > Lead > Developer > Viewer
```

Each higher role inherits all permissions of lower roles.

> **Team-scoped roles**: Your role may differ per platform. For example, you could be a Lead on the `cp` platform but a Developer on `fhk`. The portal resolves your effective permissions for each platform you switch to.

## Role Definitions

### Viewer

**Description**: Read-only access to applications and logs

**Can**:
- ✅ View all applications in accessible environments
- ✅ View application details and status
- ✅ View logs
- ✅ View configuration (read-only)
- ✅ View operation history

**Cannot**:
- ❌ Create applications
- ❌ Update configuration
- ❌ Restart or scale applications
- ❌ Delete applications

**Typical users**: Stakeholders, support staff, auditors

### Developer

**Description**: Can deploy and manage applications in non-production; read-only on production

**Can** (in addition to Viewer):
- ✅ Update configuration (non-production and production)
- ✅ Restart applications
- ✅ Scale applications
- ✅ Stop/start applications
- ✅ Exec into pods (non-production only)

**Read-only on production** (cannot modify):
- ❌ Update/write configuration on production
- ❌ Restart, scale, or stop production apps
- ❌ Exec into production pods

**Cannot** (any tier):
- ❌ Delete applications
- ❌ Manage platform services

**Typical users**: Application developers, DevOps engineers

### Lead

**Description**: Full team application management including deletion, with full read/write access on all tiers

**Can** (in addition to Developer):
- ✅ Delete applications
- ✅ Modify and restart production applications
- ✅ Exec into pods on all tiers (including production)
- ✅ Manage team applications fully

**Cannot**:
- ❌ Manage platform services
- ❌ Access other teams' restricted resources

**Typical users**: Tech leads, senior developers, team managers

### Admin

**Description**: Full platform access including platform service management

**Can** (in addition to Lead):
- ✅ Manage platform services
- ✅ Access all applications across all teams
- ✅ Manage access controls
- ✅ View audit logs

**Typical users**: Platform team, operations team

## Team-Based Access

### How It Works

Access is controlled by **three factors**:

1. **Your Role**: Determines what you can do
2. **Your Team Membership**: Determines which platforms you can access
3. **Environment Tier**: Determines what your role permits (non-production vs production)

### Team-Scoped Roles

You can hold **different roles on different platforms**. The portal resolves your highest effective role when you switch between platforms.

**Examples:**
- `cp_leads` — Lead on the `cp` platform (and all environments under it, e.g. `cp-prod`, `cp-dev`)
- `fhk_developers` — Developer on the `fhk` platform only
- `admins` — Global Admin across all platforms

If you have both `cp_leads` and `fhk_developers`, you'll have Lead permissions on `cp` environments and Developer permissions on `fhk` environments.

### Production vs Non-Production Tiers

| Tier | Developer | Lead | Admin |
|------|-----------|------|-------|
| Non-production (dev, qa, uat) | Full read/write | Full read/write | Full read/write |
| Production | **Read-only** | Full read/write | Full read/write |

Developers cannot modify applications or exec into pods in production environments. They will see production apps and logs, but action buttons are disabled.

Example:
- User is a **Developer** on the **Falcon** team
- Can create/update/restart Falcon apps in dev and qa environments
- Can **view** Falcon apps in production, but **cannot** change them
- Cannot access Phoenix team apps in any environment
- Cannot delete any applications (requires Lead role)

### Azure AD Integration

Access control leverages:

- **Azure AD Security Groups**: Control platform/environment access
- **App Roles**: Define your role (Admin/Lead/Developer/Viewer)
- **Team Assignments**: Link you to specific teams

## Checking Your Access

### My Access Panel

View your permissions:

1. Navigate to Mars Rover
2. Check "My Access" panel
3. See your:
   - Teams
   - Roles
   - Accessible platforms
   - Accessible environments

### Testing Permissions

Buttons and actions are hidden/disabled based on your role:

- Grayed out = No permission
- Visible and enabled = You can perform this action

## Requesting Access Changes

### Need More Access?

Contact MARS Platform Team via:
- Email: mars-platformteam@maximus.com

**Provide**:
- Your name and team
- Current role
- Desired role or additional access
- Business justification

### Need to Remove Access?

When team members leave or change roles:
- Notify platform team
- They'll update Azure AD groups
- Access is revoked automatically

## Audit Logging

All actions are logged for compliance:

- Who performed the action
- What action was performed
- When it occurred
- Which resource was affected
- Outcome (success/failure)

**Access audit logs**: Admin role required

## Best Practices

### Principle of Least Privilege

- Request only access you need
- Use lowest role that allows your work
- Escalate temporarily when needed

### Access Reviews

Teams should regularly review:
- Who has access
- Which roles are assigned
- Remove unnecessary access

### Security

- Don't share credentials
- Report suspicious activity
- Follow company security policies

## Troubleshooting

### "Permission Denied" Errors

**Check**:
1. Your current role
2. Required role for the action
3. Team membership
4. Platform/environment access

**Solutions**:
- Request role upgrade
- Request additional team access
- Contact platform team

### Can't See Expected Applications

**Possible reasons**:
- Wrong platform/environment selected
- Not a member of the owning team
- Application doesn't exist in this environment
- Access hasn't been granted yet

**Solutions**:
- Verify platform/environment selection
- Request team access
- Contact application owner
- Contact platform team

## Next Steps

- **[Quick Start Guide](../getting-started/quick-start.md)** - Learn the basics
- **[Application Management](application-management.md)** - Manage apps based on your role
- **[Support](../reference/support.md)** - Get help with access issues
