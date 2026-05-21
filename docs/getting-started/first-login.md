# First Login & Navigation

This guide walks you through your first login to the Developer Portal and explains the key interface elements.

## Accessing the Portal

1. Open your web browser and navigate to the DevPortal URL (provided by your platform team)
2. You'll see the Backstage homepage with a "Sign in" button
3. Click **"Sign in with Microsoft"**
4. Authenticate using your company Microsoft account

!!! tip "Bookmark It"
    Save the DevPortal URL to your bookmarks for quick access.

## Understanding the Interface

### Main Navigation

After logging in, you'll see the main Backstage interface:

- **Left Sidebar**: Main navigation menu
  - **Home**: Backstage homepage
  - **Catalog**: Component catalog
  - **APIs**: API registry
  - **Docs**: Technical documentation
  - **Applications**: Application management ← **This is what you'll use most**
  - **Create**: Software templates

- **Top Bar**: User menu and search
  - **Search**: Find components, docs, and APIs
  - **User Avatar**: Your profile and settings
  - **Role Badge**: Shows your current role

### Application Management

Click on **"Applications"** in the left sidebar. You'll see the catalog of registered applications. Click on your application to see details, then select the **"MARS Rover"** tab to access application management features.

#### Platform & Environment Selection

In the MARS Rover tab:

1. **Platform Dropdown**: Select which platform/cluster (e.g., `eks-prod-us-east-1`)
2. **Environment Dropdown**: Select which environment (e.g., `dev`, `qa`, `prod`)

!!! info "Single Portal"
    Unlike Epinio where you had separate portals per platform, the Developer Portal provides access to **all platforms and environments** from one place.

#### Application List

Once you select a platform and environment, you'll see:

- **Application Cards/Table**: Your deployed applications
- **Search Bar**: Filter applications by name
- **Sort Options**: Sort by name, status, age, etc.
- **Pagination**: Navigate through pages if you have many apps

#### Application Detail View

Click on any application to see:

**Tabs**:

- **Overview**: Application status, routes, instance count
- **Instances**: Detailed instance status and health
- **Logs**: Real-time log viewer
- **Configuration**: View and edit manifest/configuration
- **Operations**: Track ongoing and recent operations

**Actions Menu**:

- Restart
- Scale
- Stop/Start
- Delete (Lead/Admin only)

## Understanding Your Role

Your role determines what actions you can perform. Check the top-right corner to see your assigned role.

### Role Hierarchy

```
Admin > Lead > Developer > Viewer
```

Each higher role can perform all actions of lower roles, plus additional ones.

| Role | Description | Typical Responsibilities |
|------|-------------|-------------------------|
| **Admin** | Full access to all features | Platform team, operations |
| **Lead** | Can delete applications and manage team apps | Tech leads, senior developers |
| **Developer** | Can deploy, update, restart, scale apps | Application developers |
| **Viewer** | Read-only access | Stakeholders, support teams |

### Team-Based Access

Access is controlled by two factors:

1. **Your Role**: Determines what actions you can perform
2. **Your Team**: Determines which platforms/environments you can access

!!! question "Need Access?"
    If you don't see the platforms or environments you need, or need a different role, contact the MARS Platform Team.

## My Access Panel

The "My Access" panel shows:

- **Your Teams**: Which teams you belong to
- **Your Roles**: Your role assignments per team/platform
- **Available Platforms**: Platforms you have access to
- **Available Environments**: Environments you can manage

## Navigation Tips

### Quick Access

- **Recent Apps**: Your recently viewed applications appear at the top
- **Favorites**: Star applications for quick access (feature may vary)
- **Search**: Use the global search to find applications across all environments

### Multi-Tab Workflow

You can open multiple applications in separate browser tabs for parallel management:

1. Right-click on an application → "Open in new tab"
2. Work on multiple apps simultaneously
3. Each tab maintains its own operation tracking

### Breadcrumbs

Use the breadcrumb navigation to quickly return to previous views:

```
Mars Rover > Platform: eks-prod > Environment: prod > App: my-service
                ↑               ↑                 ↑
            Click to go back to any level
```

## Common First-Time Tasks

### 1. Find Your Team's Applications

1. Click **Mars Rover** in the sidebar
2. Select your team's platform
3. Select your environment (usually start with `dev`)
4. Browse your team's applications

### 2. Check Application Health

1. Click on an application
2. Go to **Instances** tab
3. Verify all instances are "Running"
4. Check for any restart counts or errors

### 3. View Application Logs

1. Click on an application
2. Go to **Logs** tab
3. Watch the real-time log stream
4. Use for quick debugging (remember: Grafana/Loki for deep analysis)

### 4. Explore the Configuration

1. Click on an application
2. Go to **Configuration** tab
3. Review environment variables and settings
4. Don't edit yet - just familiarize yourself

## Setting Up Your Workflow

### Recommended Browser Setup

1. **Primary Tab**: MARS Rover tab for application management
2. **Secondary Tab**: Grafana for log analysis and dashboards
3. **Third Tab**: Your CI/CD pipeline (Jenkins)

### Notifications (if available)

Configure browser notifications to get alerts for:

- Operation completions
- Application health changes
- Failed deployments

## Next Steps

Now that you're familiar with the interface:

1. **[Quick Start Guide](quick-start.md)** - Learn common operations
2. **[Application Management](../user-guides/application-management.md)** - Detailed management guide
3. **[Migration from Epinio](migration-guide.md)** - If you're transitioning from Epinio

## Getting Help

- **In-Portal Help**: Look for help icons (?) throughout the interface
- **Documentation**: Access via the "Docs" link in the main navigation
- **Support**: Contact the MARS Platform Team via email at mars-platformteam@maximus.com

---

!!! success "You're All Set!"
    You should now be comfortable navigating the portal. Try exploring your applications and viewing their status to get familiar with the interface.
