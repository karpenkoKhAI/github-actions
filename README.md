# GitHub Actions CI/CD Pipeline

This repository demonstrates a comprehensive GitHub Actions workflow with build, test, and push artifacts stages.

## Workflow Overview

The CI/CD pipeline (`.github/workflows/ci-cd.yml`) includes:

### 🔨 Build Stage
- Sets up Node.js environment
- Installs dependencies
- Builds the application
- Uploads build artifacts for use in subsequent stages

### 🧪 Test Stage
- Runs in parallel with matrix strategy (unit & integration tests)
- Downloads build artifacts
- Executes test suites
- Uploads test results and coverage reports

### 🚀 Push Artifacts Stage
- Only runs on main branch pushes
- Downloads all artifacts
- Creates release packages
- Supports multiple deployment targets:
  - GitHub Packages (Docker)
  - NPM Registry
  - GitHub Releases
  - AWS S3
  - Custom deployment environments

### 📢 Notification Stage
- Runs after all stages complete
- Provides success/failure notifications

## Key Features

- **Multi-stage pipeline** with proper dependency management
- **Artifact management** between stages
- **Matrix builds** for comprehensive testing
- **Conditional deployments** based on branch and events
- **Error handling** and notifications
- **Flexible configuration** for different project types

## Triggering the Workflow

The workflow triggers on:
- Push to `main` or `develop` branches
- Pull requests to `main` branch
- Manual dispatch via GitHub UI

## Configuration

### Environment Variables
- `NODE_VERSION`: Node.js version (default: 18)
- `ARTIFACT_NAME`: Name for build artifacts

### Secrets Required (for optional features)
- `GITHUB_TOKEN`: Automatically provided by GitHub
- `NPM_TOKEN`: For NPM package publishing
- `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`: For S3 uploads

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # Main workflow file
├── src/
│   └── index.js               # Sample application
├── package.json               # Project configuration
└── README.md                  # This file
```

## Usage

1. Fork or use this repository as a template
2. Customize the workflow for your project type
3. Enable/disable specific deployment targets
4. Configure required secrets in repository settings
5. Push to main branch or create a pull request

## Customization

The workflow is designed to be flexible and can be adapted for:
- Different programming languages (Python, Java, etc.)
- Various deployment targets
- Custom build processes
- Different testing frameworks

Simply modify the relevant steps in the workflow file to match your project requirements.
