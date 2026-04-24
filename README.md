# Renovate Runner

Centralized Renovate Bot runner for the `haproxy-haptic` GitLab group.

## Overview

This project runs [Renovate](https://docs.renovatebot.com/) on a schedule to automatically create merge requests for dependency updates across all repositories in the group.

## Configuration

The runner uses the official [renovate-bot/renovate-runner](https://gitlab.com/renovate-bot/renovate-runner) templates with autodiscover enabled for the `haproxy-haptic/*` group.

### CI/CD Variables

| Variable | Description |
|----------|-------------|
| `RENOVATE_TOKEN` | GitLab Group Access Token with Developer role and `api` scope |
| `RENOVATE_GITHUB_COM_TOKEN` | GitHub PAT for fetching changelogs from public repos |

### Schedules

- **Renovate dependency updates**: Runs hourly to check for updates
- **Rotate Renovate token**: Runs monthly to rotate the GitLab token before expiry

## Adding Renovate to a Repository

Repositories in the `haproxy-haptic` group are automatically discovered. To inherit the group-wide Renovate policy (auto-merge for non-major updates, dependency dashboard, semantic commits, etc.), extend the shared preset shipped from this repo:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["gitlab>haproxy-haptic/renovate-runner"]
}
```

Repo-specific `packageRules`, `customManagers`, and overrides can be added alongside the `extends` line. The preset itself is `default.json` at the root of this repo.

## License

Apache License 2.0
