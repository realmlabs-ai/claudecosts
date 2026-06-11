<div align="center">

# 😱 ClaudeCosts

**Self-hosted gateway for Claude Code [Personal/Team/Enterprise]**

[![Self-Hosted](https://img.shields.io/badge/Self--Hosted-2ea44f?style=for-the-badge)](#run-it-yourself)
[![License: Realm Labs License 1.0](https://img.shields.io/badge/License-Realm_Labs_License_1.0-blue?style=for-the-badge)](LICENSE)

Observability, cost breakdown, and saving opportunities for Claude Code.

Built by **[Realm Labs](https://realmlabs.ai)**

</div>

---

## Run it yourself

Install and connect your **personal, team, or enterprise** Claude Code in minutes. ClaudeCosts runs as a set of Docker containers — a Postgres database, the backend, the metering **gateway**, and the **dashboard** UI. All you need is [Docker](https://docs.docker.com/get-docker/) with Compose.

### Recommended hardware

A single host with **8 CPUs** and **16–32 GB RAM** is the sweet spot (for example, Macbook Pro). Run it on **any cloud provider** — ideally a **Linux** server — though **macOS** and **Windows** are supported as well.

### 1. Clone the repo

The stack is defined in [docker-compose.yml](docker-compose.yml), so you need a local copy of this repo before you can bring it up.

```bash
git clone https://github.com/realmlabs-ai/claudecosts.git
cd claudecosts
```

Run all of the commands below from inside this `claudecosts` directory.

### 2. Start the stack

```bash
LLM_API_KEY=sk-ant-api... CLAUDE_GATEWAY_PORT=9090 UI_PORT=3001 docker compose up -d
```

This pulls the published images, runs the database migrations, and starts every service in the background.

| Variable | Default | Description |
| --- | --- | --- |
| `LLM_API_KEY` | _(empty)_ | Your Anthropic API key (`sk-ant-...`). See the note below. |
| `CLAUDE_GATEWAY_PORT` | `8080` | Port the Claude Code gateway listens on. |
| `UI_PORT` | `3000` | Port the dashboard UI is served on. |

**Default ports** — if you omit `CLAUDE_GATEWAY_PORT` and `UI_PORT`, the stack falls back to:

```
CLAUDE_GATEWAY_PORT=8080
UI_PORT=3000
```
> **⚠️ Without an `LLM_API_KEY`, functionality will be limited.** The stack will still come up and meter traffic, but features that rely on the model — such as intent classification and cost saving analysis — won't be available until you provide a key. The LLM_API_KEY is not used to make the actual Claude Code calls which will continue to be made through your pre-exising OAuth credentials (Claude Login) or ANTHROPIC_API_KEY.

Once `docker compose up -d` finishes, all services should report as running.

### 3. Open the dashboard

With the example ports above, the dashboard is available at:

```
http://localhost:3001
```

On a fresh install the dashboard is empty until traffic starts flowing through the gateway (next step).

### 4. Replace the Anthropic endpoint with the gateway

Claude Code normally talks to Anthropic directly. To meter every call, point it at the gateway instead by setting `ANTHROPIC_BASE_URL`:

**Quick start** (only applies to this terminal session):

```bash
export ANTHROPIC_BASE_URL=http://localhost:9090
```

> **⚠️ `export` only applies to the current terminal session.** It does **not** carry over to new terminals, and it does **not** affect Claude Code running in your IDE or Desktop app. For persistent setup — and to route the IDE/Desktop app — set `ANTHROPIC_BASE_URL` in your Claude Code settings or roll it out org-wide via Anthropic managed settings.

**Full integration:**

📖 **See [Connecting Claude Code to the gateway](docs/connect-claude-code.md)** for full setup instructions — covering an **individual user** (shell, IDE, and per-project settings) and **organization-wide (enterprise)** rollout via Anthropic managed settings.

### Stop the stack

```bash
docker compose down
```

If you only exported the base URL, restart your terminal to go to Anthropic directly. If you made a system or team/enterprise level change, please remove the `ANTHROPIC_BASE_URL` from local `settings.json` or `managed-settings.json` respectively.

---

## Feedback & support

**[Join our Discord →](https://discord.gg/6RPjGBEZW)** — the best place to share feedback, ask questions, and connect with the community. We're most active there.

Prefer another channel?

- **[Open a GitHub issue](../../issues)** — for bugs, unexpected behavior, or feature requests.
- **[feedback@realmlabs.ai](mailto:feedback@realmlabs.ai)** — if you'd rather drop us an email.

Also see **[LIMITATIONS.md](docs/LIMITATIONS.md)** for known constraints around sub-agent visibility, data persistence, and production scale.

---

<div align="center">

Built by **[Realm Labs](https://realmlabs.ai)**

</div>
