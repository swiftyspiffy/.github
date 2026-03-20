# .github

Shared GitHub Actions workflows and configurations.

## Reusable Workflows

### `notify-commit.yml`

Sends push notifications via ntfy when commits are made.

**Usage:**

Add this to your repo's `.github/workflows/notify.yml`:

```yaml
name: Notify Commit

on:
  push:
    branches: [main]

jobs:
  notify:
    uses: swiftyspiffy/.github/.github/workflows/notify-commit.yml@main
    secrets:
      TS_AUTHKEY: ${{ secrets.TS_AUTHKEY }}
      NTFY_SERVER_URL: ${{ secrets.NTFY_SERVER_URL }}
```

**With custom topic:**

```yaml
jobs:
  notify:
    uses: swiftyspiffy/.github/.github/workflows/notify-commit.yml@main
    with:
      topic: my-custom-topic
    secrets:
      TS_AUTHKEY: ${{ secrets.TS_AUTHKEY }}
      NTFY_SERVER_URL: ${{ secrets.NTFY_SERVER_URL }}
```

**Inputs:**

| Input | Default | Description |
|-------|---------|-------------|
| `topic` | `deploys` | ntfy topic to publish to |

**Secrets required:**

- `TS_AUTHKEY` - Tailscale auth key (ephemeral recommended)
- `NTFY_SERVER_URL` - ntfy server URL

**Notification format:**

- **Title:** Repository name
- **Body:** `{actor} pushed to {branch}: {commit message}`
- **Click action:** Opens commit on GitHub
- **Tags:** `git,package`
