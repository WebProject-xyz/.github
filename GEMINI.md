# Gemini CLI Context: WebProject-xyz/.github

This repository serves as the centralized hub for the **WebProject-xyz** GitHub organization's health files and shared configurations. It is primarily used to manage organization-wide Renovate bot settings and the organization's public profile documentation.

## Directory Overview

This is a **Non-Code Project** focused on configuration and documentation. It defines how dependencies are managed across all repositories within the organization and provides the content for the organization's GitHub profile page.

## Key Files

- **`renovate-config.json`**: The master Renovate configuration for the entire organization.
- **`renovate.json`**: Local Renovate configuration that extends `renovate-config.json`.
- **`renovate.md`**: User documentation for integrating the shared Renovate config.
- **`profile/README.md`**: Source for the WebProject-xyz GitHub organization profile.

## Renovate Configuration Details

The organization-wide configuration (`renovate-config.json`) is optimized for PHP/Symfony environments with the following key policies:

### 1. Automerge Strategy
- **PR-Based Automerge**: All automerges are performed via Pull Requests (`automergeType: "pr"`) to comply with branch protection rules on the default branch.
- **Rebase Policy**: PRs are automatically rebased when they are behind the base branch (`rebaseWhen: "behind-base-branch"`), ensuring they are always up-to-date before merging.
- **Stability Delay**: A `minimumReleaseAge` of 3 days is enforced to avoid immediate updates of potentially buggy new releases.
- **Manual Review**: Automerge is explicitly **disabled** for core dependencies (Symfony, PHP) to ensure manual verification.

### 2. Grouping & Noise Reduction
- **GitHub Actions**: All GitHub Action updates are grouped into a single PR.
- **PHP Dev Tools**: Development dependencies (including PHPUnit, PHPStan, and Codeception) are grouped together to reduce PR volume.
- **Minor/Patch Automerge**: General minor and patch updates for non-core packages are automatically merged once status checks pass.

### 3. PHP Environment Constraints
- **Strict Platform Requirements**: `composerIgnorePlatformReqs` is set to `false` to ensure lock files are generated for the correct environment.
- **Version Constraints**: PHP constraints are explicitly set to `~8.3.0 || ~8.4.0` to align with the organization's allowed version range.

## Usage & Integration

To use this configuration in a new repository, create a `renovate.json` file:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "local>WebProject-xyz/.github:renovate-config"
  ]
}
```

## Development Conventions

- **Semantic Commits**: Use `chore` prefix for dependency updates.
- **Profile Updates**: Changes to `profile/README.md` update the organization's main landing page.
