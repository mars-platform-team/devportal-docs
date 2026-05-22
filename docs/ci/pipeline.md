# TechDocs Publishing Pipeline

This page describes the CI/CD workflow for building and publishing the Developer Portal documentation to AWS S3 so it is served by Backstage TechDocs.

---

## Overview

Every time documentation changes are merged to the `main` branch, a pipeline should:

1. **Check out** the repository
2. **Install** Node.js (for the TechDocs CLI)
3. **Generate** the static site from the MkDocs source
4. **Authenticate** to AWS (tools account)
5. **Publish** the generated site to the S3 bucket

---

## Pipeline Steps

### 1. Checkout
Check out the `main` branch of this repository.

### 2. Set up Node.js
Install a recent LTS version of Node.js. The `@techdocs/cli` package is consumed via `npx` so no global install is needed.

### 3. Generate the site
```bash
npx @techdocs/cli generate --source-dir . --output-dir ./site
```

This reads `mkdocs.yml` and the `docs/` directory and produces a static HTML site in `./site`.

### 4. Authenticate to AWS
Configure AWS credentials with access to the `devportal-tools` account. The IAM principal needs `s3:PutObject`, `s3:DeleteObject`, and `s3:ListBucket` on the target bucket.

### 5. Publish to S3
```bash
npx @techdocs/cli publish \
  --publisher-type awsS3 \
  --storage-name devportal-tools-devportal-techdocs \
  --entity default/component/devportal-docs \
  --directory ./site
```

| Argument | Value |
|----------|-------|
| `--publisher-type` | `awsS3` |
| `--storage-name` | `devportal-tools-devportal-techdocs` |
| `--entity` | `default/component/devportal-docs` |
| `--directory` | `./site` (output of the generate step) |

---

## Trigger

The pipeline should run on every push to `main` that touches any file under `docs/` or `mkdocs.yml`. No other branches need to trigger a publish.

---

## Manual Publish

If you need to publish outside of CI (e.g. during initial setup or to fix a broken pipeline), run the generate and publish commands locally:

```bash
# Authenticate to the tools account first, then:
npx @techdocs/cli generate --source-dir . --output-dir ./site

npx @techdocs/cli publish \
  --publisher-type awsS3 \
  --storage-name devportal-tools-devportal-techdocs \
  --entity default/component/devportal-docs \
  --directory ./site
```

See the [README](https://github.com/mars-platform-team/devportal-docs/blob/main/README.md) for full manual instructions.

---

## Notes

- The `--entity` value must be lowercase and match the `metadata.name` in `catalog-info.yaml` exactly: `<namespace>/<kind>/<name>`.
- Backstage caches TechDocs pages. After a successful publish, wait a few minutes and hard-refresh the Docs tab in Backstage to see the latest content.
- The `./site` directory should be excluded from version control (add to `.gitignore`).
