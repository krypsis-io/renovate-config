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
| Vulnerability alerts | GitHub Dependabot alerts + OSV | Security fix PRs are labeled `security` and skip the 7-day minimum release age and every schedule (Renovate's built-in `vulnerabilityAlerts` defaults). GitHub alerts need Dependabot alerts enabled on the repo; OSV covers direct dependencies only |
| Lock file maintenance | Monday 00:00–11:59 (America/New_York), automerged | Refreshes the lock file weekly, which is what updates transitive dependencies. Twelve hours, because the hosted app runs a quiet repo only every few hours and can miss the default four-hour window |
| Go module tidy | `gomodTidy` | Renovate runs `go mod tidy` after Go module updates so stale `go.sum` entries are pruned instead of accumulating |
