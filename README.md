# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) configuration preset for `krypsis-io` repos.

## Usage

Add this to your repository's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>krypsis-io/renovate-config"]
}
```

## What this config does

| Setting | Value | Effect |
|---------|-------|--------|
| Base preset | `config:recommended` | Renovate's recommended defaults (pinning, scheduling, grouping) |
| Labels | `dependencies` | All Renovate PRs are labeled `dependencies` |
| Commit prefix | `chore(deps):` | Conventional commit format, avoids triggering version bumps |
| Minimum release age | 7 days | New package versions must exist for 7 days before Renovate opens a PR (supply chain defense) |
| Minor automerge | Enabled | Minor updates auto-merge after checks pass |
| Patch automerge | Enabled | Patch updates auto-merge after checks pass |
| GitHub Actions automerge | Minor and patch only | Minor and patch Actions updates auto-merge; major requires manual review |
| Vulnerability alerts | GitHub Dependabot alerts + OSV | Security fix PRs are labeled `security` and skip the 7-day minimum release age and every schedule (Renovate's built-in `vulnerabilityAlerts` defaults). GitHub alert-driven PRs need all three on the consuming repo: the dependency graph, Dependabot alerts, and read access to "Dependabot alerts" for the Renovate app; with any one missing, Renovate opens no fix PRs from GitHub alerts. OSV is a backstop for direct dependencies only, and only for the datasources Renovate queries OSV for (not `docker`, for example; see [the supported list](https://docs.renovatebot.com/configuration-options/#osvvulnerabilityalerts)) |
| Lock file maintenance | Monday 00:00–11:59 (America/New_York), automerged | Refreshes the lock file weekly, which is what updates transitive dependencies. Twelve hours, because the hosted app runs a quiet repo only every few hours and can miss the default four-hour window |
| Go module tidy | `gomodTidy` | Renovate runs `go mod tidy` after Go module updates so stale `go.sum` entries are pruned instead of accumulating |
