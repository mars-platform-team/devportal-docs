# Role-Based Access Control (RBAC)

Understanding permissions and access control in Mars Rover.

## Overview

Mars Rover uses a 4-tier role system with team-based access control to ensure secure and appropriate access to applications and platforms.

## Role Hierarchy

```
Admin > Lead > Developer > Viewer
```

Each higher role inherits all permissions of lower roles.

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

**Description**: Can deploy and manage applications

**Can** (in addition to Viewer):
- ✅ Create applications
- ✅ Update configuration
- ✅ Restart applications
- ✅ Scale applications
- ✅ Stop/start applications

**Cannot**:
- ❌ Delete applications
- ❌ Manage platform services

**Typical users**: Application developers, DevOps engineers

### Lead

**Description**: Full team application management including deletion

**Can** (in addition to Developer):
- ✅ Delete applications
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

Access is controlled by **two factors**:

1. **Your Role**: Determines what you can do
2. **Your Team Membership**: Determines what you can access

Example:
- User is a **Developer** on the **Falcon** team
- Can manage Falcon team apps in dev/qa/prod
- Cannot access Phoenix team apps
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
