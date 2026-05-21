# Developer Portal Documentation

This repository contains the user-facing documentation for the Developer Portal, published via Backstage TechDocs.

## 📚 Documentation Structure

```
devportal-docs/
├── docs/                          # Documentation source files
│   ├── index.md                  # Documentation home page
│   ├── getting-started/          # Getting started guides
│   ├── user-guides/              # Detailed user guides
│   ├── beta-testing/             # Beta testing materials
│   ├── migration/                # Epinio migration docs
│   └── reference/                # Reference materials
├── mkdocs.yml                    # MkDocs configuration for TechDocs
├── catalog-info.yaml             # Backstage catalog registration
└── README.md                     # This file
```

## 🚀 Viewing Documentation

### In Backstage
1. Navigate to Backstage
2. Search for "devportal-docs" or "Developer Portal Documentation"
3. Click on the Docs tab

### Locally
```bash
# Install dependencies
pip install mkdocs-techdocs-core

# Serve documentation locally
mkdocs serve

# View at http://localhost:8000
```

## ✏️ Contributing

### Making Changes

1. Edit files in the `docs/` directory
2. Test locally using `mkdocs serve`
3. Commit and push to `main` branch
4. TechDocs will automatically rebuild in Backstage

### Adding New Pages

1. Create a new `.md` file in the appropriate directory under `docs/`
2. Add the page to `nav:` section in `mkdocs.yml`
3. Update any necessary cross-references

## 📖 Documentation Categories

### Getting Started
- Quick Start Guide - 5-minute introduction
- First Login - Initial setup and access
- Migration from Epinio - For existing Epinio users

### User Guides
- Application Management - Deploy, scale, restart apps
- Monitoring & Logging - View logs and monitor health
- Configuration Management - Update app configurations
- Role-Based Access - Understanding permissions

### Beta Testing
- Testing Guide - Comprehensive testing checklist
- Feedback Template - Structured feedback format

### Migration  
- Feature Comparison - Epinio vs Backstage + Rover
- Migration Process - Step-by-step migration guide
- FAQ - Common migration questions

### Reference
- Troubleshooting - Common issues and solutions
- Glossary - Terms and definitions
- Support - How to get help

## 🏗️ TechDocs Integration

This documentation is integrated with Backstage TechDocs, which provides:

- **Automatic Publishing**: Docs update automatically on commit
- **Search Integration**: Full-text search across all documentation
- **Version Control**: All changes tracked in Git
- **Access Control**: Integrated with Backstage authentication

## 🔧 Technical Details

- **Static Site Generator**: MkDocs with Material theme
- **Format**: Markdown with extensions
- **CI/CD**: Automatic builds via Backstage TechDocs
- **Hosting**: Served through Backstage

## 📝 Writing Guidelines

- Use clear, concise language
- Include code examples where applicable
- Add screenshots for UI-heavy sections
- Use admonitions for important notes
- Keep paragraphs short and scannable
- Test all commands and examples

## 👥 Ownership

- **Owner**: MARS Platform Team
- **Maintainers**: Platform Engineering
- **Reviewers**: DevOps Team

## 📞 Support

For questions or issues with the documentation:
- Open an issue in this repository
- Contact the MARS Platform Team
- Use the #platform-support Slack channel

---

**Last Updated**: May 21, 2026  
**Version**: 1.0.0
