# Migration Process: Step-by-Step Guide

This comprehensive guide walks you through migrating your applications from Epinio to the Developer Portal.

## Before You Begin

### Prerequisites

- [ ] Access to the Developer Portal (if not, [request access](#requesting-access))
- [ ] Familiarity with your application's current Epinio deployment
- [ ] Access to your team's CD pipeline
- [ ] Contact information for MARS Platform Team

### What You Need to Know

1. **Manifest conversion is automatic** - No manual editing required
2. **Routes remain unchanged** - Application URLs stay the same
3. **CI/CD pipeline minimal changes** - Only deployment target changes
4. **Teams migrate incrementally** - Do one app at a time or in parallel
5. **Rollback is possible** - Can redeploy to Epinio if needed during transition

## Step-by-Step Migration

### Phase 1: Requesting Access

#### 1.1 Contact Platform Team

Send a request to the MARS Platform Team with:

```
Subject: Mars Rover Access Request - [Your Team Name]

Team Name: [e.g., "Falcon Team"]
Team Lead: [Name and email]
Required Platforms: [e.g., "eks-prod-us-east-1, eks-dev-us-west-2"]
Required Environments: [e.g., "dev, qa, prod"]
Number of team members: [e.g., "5"]
Desired roles: 
  - [Name]: [Admin/Lead/Developer/Viewer]  
  - [Name]: [Admin/Lead/Developer/Viewer]
```

**Contact Methods**:
- Email: mars-platformteam@maximus.com

#### 1.2 Wait for Confirmation

You'll receive confirmation when:
- Your Azure AD Security Groups are configured
- Role assignments are complete
- You have access to the portal

**Typical turnaround**: 1-2 business days

#### 1.3 Verify Access

1. Log into Mars Rover portal
2. Check that you see your assigned platforms
3. Verify you can access required environments
4. Confirm your role is displayed correctly

### Phase 2: Prepare for Migration

#### 2.1 Review Your Applications

For each application:

- Document current configuration
- Note any special requirements  
- Identify dependencies on other services
- Check current Epinio manifest

#### 2.2 Plan Migration Order

**Recommended approach**:

1. Start with **dev environment** applications
2. Choose a **simple, stateless application** first
3. Migrate **critical applications last**
4. Do **one environment at a time** (dev → qa → prod)

#### 2.3 Communicate with Your Team

- Notify team members of migration schedule
- Coordinate who will handle which applications
- Plan for potential downtime windows
- Set up communication channel for migration day

### Phase 3: Migrate an Application

#### 3.1 Pre-Migration Checklist

- [ ] Application is stable in Epinio
- [ ] Recent backup/snapshot exists (if applicable)
- [ ] Dependencies are documented
- [ ] Routes/URLs are documented
- [ ] Team members are informed
- [ ] Test plan is ready

#### 3.2 Delete from Epinio

1. Log into Epinio UI
2. Navigate to your application
3. Click **Delete** button
4. Confirm deletion
5. Verify application is removed

!!! warning "Point of No Return"
    Once deleted from Epinio, the application will be offline until redeployed to Mars Rover.

#### 3.3 Trigger CD Pipeline

1. Navigate to your CI/CD system (Jenkins)
2. Locate your application's CD job
3. Trigger deployment with appropriate parameters
4. Monitor pipeline execution

**What happens automatically**:
- Pipeline fetches your Epinio manifest
- Parser converts manifest to Mars Rover format
- Application deploys to Mars Rover
- Routes are configured automatically

#### 3.4 Monitor Deployment

1. Watch CD pipeline logs for any errors
2. Check for "Deployment Successful" message
3. Note the operation ID if provided

#### 3.5 Verify in Mars Rover

1. Log into Mars Rover portal
2. Select platform and environment
3. Find your application in the list
4. Click on application name
5. Verify:
   - Status is "Running"
   - Instances are healthy
   - Routes are displayed correctly
   - Configuration matches expectations

#### 3.6 Test Application

1. Access application via its route (URL)
2. Perform functional testing
3. Check logs in Mars Rover (Logs tab)
4. Verify logs in Grafana/Loki
5. Test any integrations with other services

#### 3.7 Post-Migration Validation

- [ ] Application is accessible at correct URL
- [ ] All instances are running and healthy
- [ ] Logs appear in both Mars Rover and Grafana/Loki
- [ ] Application functions correctly
- [ ] Dependencies/integrations work
- [ ] No errors in monitoring dashboards

### Phase 4: Iterate for Remaining Applications

Repeat Phase 3 for each application.

**Tips for efficiency**:
- Migrate similar applications in batches
- Use parallel team member workflows
- Document any issues for future reference
- Refine process based on learnings

### Phase 5: Post-Migration

#### 5.1 Update Documentation

- Update runbooks with Mars Rover procedures
- Document any configuration changes
- Update team wiki/knowledge base
- Share lessons learned with team

#### 5.2 Update Monitoring

- Verify Grafana dashboards still work
- Update any hardcoded Epinio references
- Test alerting rules
- Update incident response procedures

#### 5.3 Team Training

- Conduct walkthroughs of Mars Rover interface
- Share common operations guide
- Answer questions from team members
- Collect feedback on experience

#### 5.4 Provide Feedback

Send your feedback to mars-platformteam@maximus.com with details about your testing experience.

## Migration Timelines

### By Application Type

| Application Type | Estimated Time | Notes |
|-----------------|----------------|-------|
| Simple stateless app | 15-30 minutes | Single instance, no dependencies |
| Stateless with dependencies | 30-45 minutes | Database connections, external APIs |
| Stateful application | 45-60 minutes | Persistent data, careful validation |
| Complex multi-tier app | 1-2 hours | Multiple components, integration testing |

### By Team Size

| Applications | 1 Person | 2 People | 3+ People |
|--------------|----------|----------|-----------|
| 1-5 apps | 1-3 hours | 1-2 hours | 1 hour |
| 6-15 apps | 3-8 hours | 2-5 hours | 2-3 hours |
| 16+ apps | 1-2 days | 1 day | Half day |

*Assuming parallel migration where possible*

## Troubleshooting Migration Issues

### Application Won't Deploy

**Symptoms**: CD pipeline fails, application doesn't appear in Mars Rover

**Solutions**:
1. Check CD pipeline logs for errors
2. Verify manifest syntax
3. Confirm platform/environment are correct
4. Contact platform team with pipeline logs

### Application Deploys But Won't Start

**Symptoms**: Application appears in Mars Rover but instances are "Failed" or "Pending"

**Solutions**:
1. Check logs in Mars Rover Logs tab
2. Verify configuration (env vars, ports, resources)
3. Check for missing dependencies
4. Review instance events for error messages

### Routes Not Working

**Symptoms**: Application runs but URL doesn't work

**Solutions**:
1. Verify ingress/route configuration in manifest
2. Check DNS resolution
3. Confirm TLS certificates are valid
4. Verify network policies allow traffic

### Different Behavior Than Epinio

**Symptoms**: Application works differently than in Epinio

**Solutions**:
1. Compare Epinio vs Mars Rover manifests
2. Check for environment-specific configurations
3. Verify resource limits haven't changed
4. Review application logs for clues

## Rollback Procedure

If you need to rollback to Epinio:

1. Trigger redeployment to Epinio via old CD job
2. Verify application in Epinio
3. Optionally delete from Mars Rover (not required)
4. Report issue to platform team

## Getting Help During Migration

### Self-Service Resources
- [Quick Start Guide](../getting-started/quick-start.md)
- [FAQ](faq.md)
- [Troubleshooting Guide](../reference/troubleshooting.md)

### Platform Team Support

**Email**: mars-platformteam@maximus.com
- Response time: < 2 hours during business hours
- For questions, guidance, and technical support
- Include operation IDs, logs, and error messages when reporting issues

**Pair Programming Sessions**
- Available for complex applications
- Schedule via Slack or email
- Platform engineer walks through migration with you

**Emergency Support**
- PagerDuty on-call engineer
- For production-impacting issues only
- Include: timestamp, application name, environment, error details

## Migration Checklist Summary

Use this checklist to track your migration progress:

### Pre-Migration
- [ ] Access requested and confirmed
- [ ] Team notified of migration plan
- [ ] Applications prioritized
- [ ] Documentation reviewed

### Per Application
- [ ] Current state documented
- [ ] Application deleted from Epinio
- [ ] CD pipeline triggered
- [ ] Deployment monitored
- [ ] Application verified in Mars Rover
- [ ] Functionality tested
- [ ] Logs confirmed in Grafana/Loki
- [ ] Team notified of completion

### Post-Migration
- [ ] All applications migrated
- [ ] Documentation updated
- [ ] Monitoring verified
- [ ] Team trained
- [ ] Feedback submitted

## Next Steps

- **[Feature Comparison](feature-comparison.md)** - Understand what's changed
- **[FAQ](faq.md)** - Common questions answered
- **[Quick Start Guide](../getting-started/quick-start.md)** - Learn the interface
- **[Support](../reference/support.md)** - How to get help

---

!!! success "You're Ready!"
    With this guide, you have everything you need for a successful migration. Take it one application at a time, and don't hesitate to reach out to the platform team for help!
