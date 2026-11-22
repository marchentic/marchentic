<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/assets/mark-white.svg">
    <img src="docs/assets/mark-black.svg" alt="marchentic" width="96" height="96">
  </picture>
</p>

<h1 align="center">marchentic</h1>

<p align="center">
  Agent plugins that stick with you — across Claude, Cursor, Copilot, and Codex.
</p>

## Built so agents behave the way you already decided

Agent plugins for [Claude Code](https://docs.anthropic.com/en/docs/claude-code),
[Cursor](https://cursor.com),
[GitHub Copilot](https://github.com/features/copilot), and
[OpenAI Codex](https://openai.com/codex).

Each plugin is a bundle of rules, skills, agents, and slash commands that change
how the agent behaves—not just a list of files to open. Add this repo as a
marketplace, then install what you actually need.

## Install

Plugin ids are `marchentic-<short>`. The marketplace name in install
selectors is `marchentic-marketplace`. Substitute `<plugin>` with any id
from the tables below.

### Claude Code

In a Claude Code session (slash commands):

```text
/plugin marketplace add marchentic/marchentic
/plugin install <plugin>@marchentic-marketplace
```

`/plugin install` opens the plugin panel so you can pick a scope. Closing the
panel applies pending changes.

From your shell (no session required):

```shell
claude plugin marketplace add marchentic/marchentic
claude plugin install <plugin>@marchentic-marketplace
```

If a session is already running when you install from the shell, apply the
change with `/reload-plugins`. Use `/reload-plugins --force` if Claude warns
that the reload would invalidate the prompt cache.

### Cursor

1. Open **Dashboard → Settings → Plugins**
2. Import `https://github.com/marchentic/marchentic`
3. Install plugins from the catalog

### OpenAI Codex

From your shell:

```shell
codex plugin marketplace add marchentic/marchentic
codex plugin add <plugin>@marchentic-marketplace
```

Or open `/plugins` in Codex CLI, add the marketplace, and install from there.
Start a new Codex session after install so skills and tools load.

### GitHub Copilot

From your shell:

```shell
copilot plugin marketplace add marchentic/marchentic
copilot plugin install <plugin>@marchentic-marketplace
```

In an interactive Copilot CLI session the same steps are
`/plugin marketplace add …` and `/plugin install …`.

## Plugins

Marketplace ids are `marchentic-<short>`. On disk that is `plugins/<short>/`.

### Core

| Install id | Description |
| --- | --- |
| `marchentic-global` | Default posture, MCP-first workflow, writing |
| `marchentic-code` | Language standards, refactor/deslop, coding agents |
| `marchentic-business-analyst` | Briefs, plans, external research |
| `marchentic-security` | Secrets, auth, injection, crypto, supply chain |
| `marchentic-git` | Worktrees, merge conflicts, Conventional Commits |
| `marchentic-github` | PRs, review checks, Actions workflows |

### Collaboration

| Install id | Description |
| --- | --- |
| `marchentic-atlassian` | Jira and Confluence |
| `marchentic-freshservice` | Freshservice ITSM |
| `marchentic-google-workspace` | Gmail, Drive, Calendar, Docs, Sheets |

### Diagrams

| Install id | Description |
| --- | --- |
| `marchentic-drawio` | Author and repair `.drawio` diagrams |
| `marchentic-lucidchart` | Lucidchart Standard Import |

### Cloud & CI

| Install id | Description |
| --- | --- |
| `marchentic-google-cloud` | GCP projects, Compute, GKE, GCS |
| `marchentic-jenkins` | Jenkins builds and pipeline craft |
| `marchentic-runpod` | RunPod GPU cloud inventory and gated mutate |

### Infrastructure

| Install id | Description |
| --- | --- |
| `marchentic-compose` | Docker Compose |
| `marchentic-kubernetes` | Manifest craft, pods, events, logs |
| `marchentic-argocd` | Argo CD apps and gated sync |
| `marchentic-portainer` | Portainer endpoints, stacks, containers |
| `marchentic-proxmox` | Proxmox VE inventory and gated VM ops |

### Observability

| Install id | Description |
| --- | --- |
| `marchentic-grafana` | Dashboards, Explore, incidents, alerting |
| `marchentic-prometheus` | PromQL discover and query |
| `marchentic-victoriametrics` | MetricsQL / PromQL via VictoriaMetrics |
| `marchentic-graylog` | Log search |
| `marchentic-uptime-kuma` | Monitors, status pages, notifications |

### Networking & edge

| Install id | Description |
| --- | --- |
| `marchentic-cloudflare` | DNS records |
| `marchentic-fortigate` | FortiGate inventory and gated policies |
| `marchentic-nginx-proxy-manager` | Proxy hosts, SSL, access lists |
| `marchentic-traefik` | Routers, middlewares, IngressRoute |
| `marchentic-tailscale` | Devices and ACLs |

### Secrets & identity

| Install id | Description |
| --- | --- |
| `marchentic-vault` | Vault secrets and PKI |
| `marchentic-vaultwarden` | Vaultwarden admin / ops posture |
| `marchentic-authentik` | Authentik IdP apps, providers, flows |

### Storage, backup & registries

| Install id | Description |
| --- | --- |
| `marchentic-minio` | MinIO / S3 buckets and objects |
| `marchentic-velero` | Backup and restore |
| `marchentic-kopia` | Repository and snapshot inventory |
| `marchentic-zot` | Zot OCI registry inventory |
| `marchentic-harbor` | Harbor projects and artifacts |

### Media & home

| Install id | Description |
| --- | --- |
| `marchentic-yarr` | *arr, Plex, qBittorrent, Seerr |
| `marchentic-home-assistant` | Home Assistant entities and service calls |
| `marchentic-immich` | Immich library, albums, assets |

Many plugins also expose slash commands named after the short key
(`/global`, `/vault`, `/kubernetes`, …). See each plugin’s `README.md` for
details.
