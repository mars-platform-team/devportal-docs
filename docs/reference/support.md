# Getting Support

How to get help with the Developer Portal.
 
## Support Channels

### Slack (Recommended for Quick Questions)

**Channel**: Email mars-platformteam@maximus.com

**Response time**: < 2 hours during business hours (9 AM - 5 PM ET)

**Best for**:
- Quick questions
- General guidance
- Non-urgent issues
- Community discussion

**How to ask**:
```
Hey team! I'm trying to [action] for [app-name] in [environment]
but getting [error]. I've tried [what you tried]. Any ideas?

Operation ID (if applicable): [ID]
Timestamp: [when it occurred]
```

### Email

**Address**: mars-platformteam@maximus.com

**Response time**: Within 1 business day

**Best for**:
- Detailed technical questions
- Issues requiring investigation
- Feature requests
- Documentation feedback

**Template**:
```
Subject: [Issue Summary] - [App Name]

Details:
- Application: [name]
- Environment: [dev/qa/prod]
- Platform: [cluster name]
- Timestamp: [when it occurred]
- Operation ID: [if applicable]
- Your Role: [Viewer/Developer/Lead/Admin]

What happened:
[Describe the issue]

What I expected:
[Expected behavior]

What I tried:
[Steps already taken]

Error messages / logs:
[Exact error text or relevant log lines]

Screenshots:
[Attach if helpful]
```

### Emergency Support (Production Issues Only)

**PagerDuty**: [Company PagerDuty process]

**When to use**: **Production-downissues only**
- Complete service outage
- Data loss risk
- Security incidents

**Do NOT use for**:
- Development/QA issues
- Questions
- Feature requests
- Non-urgent problems

**Information to provide**:
- Application name and environment
- Impact description (how many users affected)
- Time issue started
- Error messages
- Operation ID if applicable
- What you've tried

## Self-Service Resources

Before reaching out, check these resources:

1. **[Quick Start Guide](../getting-started/quick-start.md)** - Basic operations
2. **[Troubleshooting Guide](troubleshooting.md)** - Common issues and solutions
3. **[FAQ](../migration/faq.md)** - Frequently asked questions
4. **Search** - Use the search bar in the documentation

## Office Hours

During beta testing, the platform team holds weekly office hours:

**When**: [Day and time]  
**Where**: [Meeting link or room]  
**Format**: Drop-in, no registration needed

**Good for**:
- Complex questions
- Migration planning
- Pair programming for tricky issues
- Learning best practices

## Reporting Bugs

### How to Report

Use email at mars-platformteam@maximus.com with:

**Required information**:
- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Operation ID (if applicable)
- Screenshots or screen recording
- Browser and version (for UI bugs)

**Example**:
```
Bug: Scale operation completes but instance count doesn't change

Steps to reproduce:
1. Navigate to app "my-service" in dev
2. Click Actions → Scale
3. Enter 3 replicas
4. Click Confirm
5. Operation shows "Completed"
6. Instance count still shows 1

Expected: Should show 3 running instances
Actual: Still shows 1 instance

Operation ID: abc123-def456-ghi789
Browser: Chrome 120.0
Screenshot: [attached]
```

## Feature Requests

We welcome feature requests!

**How to submit**:
- Email mars-platformteam@maximus.com for discussion
- Email for detailed proposals

**Include**:
- Use case / problem to solve
- Proposed solution
- Who would benefit
- Priority/importance
- Alternatives considered

## Training & Documentation

### Available Resources

- **This documentation site** - Comprehensive guides
- **Video walkthroughs** - [Link to internal video library]
- **Team training sessions** - Contact platform team to schedule
- **Pair programming** - For complex migrations

### Documentation Feedback

Found an error or unclear section?

**How to report**:
- Email mars-platformteam@maximus.com with:
  - Page URL
  - What's unclear or incorrect
  - Suggested improvement

## SLA & Response Times

| Channel | Response Time | Resolution Time |
|---------|--------------|-----------------|
| Email | < 2 hours (business hours) | Varies by issue |
| PagerDuty | Immediate | Based on severity |

**Business hours**: 9 AM - 5 PM ET, Monday-Friday (excluding holidays)

## Platform Team

The MARS Platform Team maintains Mars Rover and supports all users.

**Team members**: [List key contacts if appropriate]

**Responsibilities**:
- Platform operations and maintenance
- User support and troubleshooting
- Feature development
- Documentation
- Access management
- Migration support

## Escalation

If your issue isn't resolved satisfactorily:

1. **Follow up via email** - Reply to your support thread with additional details
2. **Email platform team lead** - For urgent escalation
3. **Via your manager** - For organizational issues

## Feedback

We continuously improve based on user feedback.

**Share feedback on**:
- Documentation quality
- Feature usability
- Performance issues
- Training effectiveness
- Overall experience

**Methods**:
- Email mars-platformteam@maximus.com
- [Beta Testing Guide](../beta-testing/testing-guide.md)
- During office hours

## Community

### Community Resources

Share your tips and learnings with the community:
- Contribute to documentation
- Present at team meetings
- Share best practices via email

---

## Quick Reference

**General Support**: mars-platformteam@maximus.com  
**Emergency**: PagerDuty (production issues only)  
**Documentation**: Search this site first  
**Office Hours**: [Time and location]

---

*The platform team is here to help! Don't hesitate to reach out with questions or issues.*
