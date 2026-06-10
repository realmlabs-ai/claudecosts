<div align="center">

# 😱 ClaudeCosts

**Self-hosted gateway for Claude Code**

[![Start Free](https://img.shields.io/badge/Start_Free-000000?style=for-the-badge&logo=anthropic&logoColor=white)](https://www.claudecosts.com/)
[![Self-Hosted](https://img.shields.io/badge/Self--Hosted-2ea44f?style=for-the-badge)](https://www.claudecosts.com/)
[![License: Realm Labs License 1.0](https://img.shields.io/badge/License-Realm_Labs_License_1.0-blue?style=for-the-badge)](LICENSE)

[**Start Free →**](https://www.claudecosts.com/) · [Website](https://www.claudecosts.com/) · [Built by Realm Labs](https://realmlabs.ai)

</div>

---

## Understand and Optimize Claude Costs

Observability, cost breakdown, and saving opportunities for Claude Code.

---

## Claude bills are climbing and nobody knows why.

From unexpected spikes to opaque billing, teams are flying blind on their Claude costs — and the invoice at the end of the month is the first time they see the damage.

> “I'm back to the drawing board, because the budget I thought I would need is blown away already.”
> — **Uber**, *The Information*

> “Microsoft is canceling most internal Claude Code licenses — engineers were using it too much to justify the cost.”
> — **Microsoft**, *The Next Web*

> “The leaderboard was built with good intentions, but the compute costs it generated were too high — so we deleted it.”
> — **Amazon**, *InfoWorld*

---

## See every token. Control every dollar.

ClaudeCosts gateway meters every call, gives you the controls to route, cap, and govern spend before the invoice lands.

### 01 / 03 · Full observability
Trace every session down to request, response, tool call, and line of code in one live dashboard.

### 02 / 03 · Cost breakdown
See dollars spent by every user, project, intent, and model. Get alerts on spend and minimize waste.

### 03 / 03 · Risk Mitigation
Find every unauthorized mcp server, harmful skill, and secret leaked so you can protect your organization from a disaster.

---

## Run it yourself

Install and connect your enterprise Claude Code in minutes. ClaudeCosts runs as a set of Docker containers — a Postgres database, the backend, the metering **gateway**, and the **dashboard** UI. All you need is [Docker](https://docs.docker.com/get-docker/) with Compose.

### Recommended hardware

A single host with **8 CPUs** and **16–32 GB RAM** is the sweet spot. Run it on **any cloud provider** — ideally a **Linux** server — though **macOS** and **Windows** are supported as well.

### 1. Start the stack

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

> **⚠️ Without an `LLM_API_KEY`, functionality will be limited.** The stack will still come up and meter traffic, but features that rely on the model — such as intent classification and cost saving analysis — won't be available until you provide a key.

### 2. Open the dashboard

With the example ports above, the dashboard is available at:

```
http://localhost:3001
```

### 3. Point Claude Code at the gateway

Route your Claude Code traffic through the gateway so every call is metered:

```bash
export ANTHROPIC_BASE_URL=http://localhost:9090
```

📖 **See [Connecting Claude Code to the gateway](docs/connect-claude-code.md)** for full setup instructions — both for an **individual user** and **organization-wide (enterprise)** via Anthropic managed settings.

### Stop the stack

```bash
docker compose down
```

---

## Feedback & support

Run into a hiccup? There are two ways to reach us:

- **[Open a GitHub issue](../../issues)** — for bugs, unexpected behavior, or feature requests.
- **[feedback@realmlabs.ai](mailto:feedback@realmlabs.ai)** — if you'd rather drop us an email.

Also see **[LIMITATIONS.md](LIMITATIONS.md)** for known constraints around sub-agent visibility, data persistence, and production scale.

---

## Stop panicking. Start saving.

👉 **[Start Free](https://www.claudecosts.com/)**

---

<div align="center">

Built by **[Realm Labs](https://realmlabs.ai)**

</div>
