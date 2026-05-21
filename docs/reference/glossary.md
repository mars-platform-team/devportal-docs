# Glossary

Terms and definitions for the Developer Portal.

## A

**Admin**  
The highest role level with full access to all features including platform service management. Typically assigned to platform team members.

**Application**  
A deployed software service managed through the Developer Portal. Consists of one or more instances running your container image.

**Artifactory**  
JFrog Artifactory - the artifact repository where container images and build artifacts are stored.

**Azure AD App Roles**  
Role assignments in Azure Active Directory that define user permissions within Mars Rover.

## B

**Backstage**  
The open-source platform that powers the Developer Portal. Provides the UI framework and plugin system.

**Beta Testing**  
Testing phase before general availability where select users test the platform and provide feedback.

## C

**CI/CD**  
Continuous Integration/Continuous Deployment - automated build and deployment pipelines, typically using Jenkins.

**Platform**  
A cloud infrastructure environment where applications run (e.g., eks-prod-us-east-1). The Developer Portal can manage multiple platforms from one interface.

**Configuration**  
Application settings defined in your deployment manifest, including environment variables, resources, and other runtime parameters.

**Container**  
A lightweight, standalone package containing your application and its dependencies.

## D

**Developer**  
A role that can deploy, update, restart, and scale applications but cannot delete them.

**DevPortal**  
Short for Developer Portal - refers to the Mars Rover interface and supporting backend services.

## E

**Environment**  
A deployment environment (e.g., dev, qa, prod) where applications are deployed. Organizes applications by lifecycle stage.

**Epinio**  
The previous platform for application deployment being replaced by the Developer Portal.

## G

**Grafana**  
Visualization and monitoring tool used for creating dashboards and viewing metrics. Primary tool for log analysis with Loki.

## H

**High Availability**  
Running multiple instances of an application to ensure continuous operation even if one instance fails.

## I

**Instance**  
A single running copy of your application. Applications can have multiple instances for high availability.

**Route**  
A URL path that directs external traffic to your application (e.g., `myapp.example.com`).

## J

**Jenkins**  
CI/CD automation server used for building, testing, and deploying applications.

**JWT**  
JSON Web Token - used for authentication between your browser and the backend services.

## L

**Lead**  
A role that has all Developer permissions plus the ability to delete applications.

**Loki**  
Log aggregation system that stores and queries logs. Primary tool for historical log analysis.

**Logs**  
Output from your application, useful for debugging and monitoring. Available in the Developer Portal for quick access and Grafana/Loki for deep analysis.

## M

**Manifest**  
The complete configuration for an application deployment, stored as YAML or JSON. Includes all deployment parameters and settings.

**MARS Rover**  
The application management interface within the Developer Portal. Provides capabilities for deploying and managing applications.

**Microsoft OAuth**  
Authentication system using Microsoft accounts (Azure AD) for single sign-on.

## O

**Operation**  
An action performed on an application (restart, scale, update, etc.). Each operation has a unique ID for tracking.

**Operation ID**  
Unique identifier for tracking the progress and status of an operation.

## P

**Platform**  
A cloud infrastructure environment where applications run (e.g., eks-prod-us-east-1). The Developer Portal can manage multiple platforms.

**Platform Team**  
The MARS team responsible for managing the Developer Portal infrastructure and supporting users.

## R

**RBAC**  
Role-Based Access Control - system for managing user permissions based on assigned roles.

**Replica**  
A copy of your application instance. Scaling increases replica count.

**Route**  
The URL/hostname where your application is accessible externally.

**Rover Service**  
The backend API service that handles application management operations. The platform automation layer.

## S

**Scaling**  
Adjusting the number of application instances (replicas) up or down based on load.

**Secret**  
Secure storage for sensitive data like passwords, tokens, or keys. Referenced by applications but never hardcoded in configuration.

## T

**TechDocs**  
Backstage documentation system that serves this documentation site.

## V

**Viewer**  
The most basic role with read-only access to applications and logs.

## W

**WebSocket**  
Protocol used for real-time log streaming and terminal access in the application management interface.

## Y

**YAML**  
Human-readable data serialization format used for configuration files and manifests.

---

*Don't see a term you're looking for? Contact the platform team to suggest additions.*
