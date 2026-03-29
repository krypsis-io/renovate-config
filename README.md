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
| Minimum release age | 3 days | New package versions must exist for 3 days before Renovate opens a PR (supply chain defense) |
| Minor automerge | Enabled | Minor updates auto-merge after checks pass |
| Patch automerge | Enabled | Patch updates auto-merge after checks pass |
| GitHub Actions automerge | Minor and patch only | Minor and patch Actions updates auto-merge; major requires manual review |
| Vulnerability exemption | 0 seconds | Security remediation PRs bypass the 3-day quarantine |
