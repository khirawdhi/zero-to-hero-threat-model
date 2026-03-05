# Architecture

A simplified CI/CD pipeline architecture affected by the incident:

Developer
   ↓
Source Code Repository
   ↓
CI/CD Pipeline
   ↓
Codecov Bash Uploader Script
   ↓
Environment Variables
   ↓
Attacker Server

## Components

| Component | Description |
|---|---|
| Developer | Engineers committing code |
| Source Code Repository | Version control hosting application code |
| CI/CD Pipeline | Automated build system |
| Codecov Script | Script uploading code coverage reports |
| Environment Variables | Credentials and secrets used during builds |
| Attacker Server | External server receiving stolen secrets |

## Trust Boundaries

| Boundary | Description |
|---|---|
| Developer Environment | Developer systems committing code |
| CI/CD Infrastructure | Pipeline execution environment |
| Third-Party Integration | External script provided by Codecov |
| External Network | Attacker-controlled infrastructure |
