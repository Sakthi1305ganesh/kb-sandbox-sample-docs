# Your Docs Repo

This repository was created from the [kb-sandbox-docs-template](https://github.com/trimble-oss/kb-sandbox-docs-template) — a starter for teams who want to validate their documentation against the Trimble Knowledge Service and experience it through the AAIP virtual MCP server before formal onboarding.

---

## Quick Start

### 1. Configure your service

Edit `.platform-kb/kb-manifest.yaml`:

```yaml
service_id: REPLACE_WITH_YOUR_SERVICE_ID   # lowercase, hyphen-separated
fix_version: "1.0.0"
description: "Short description of your service"
```

### 2. Add your content

| Directory | What goes here |
|-----------|---------------|
| `docs/` | Your MkDocs documentation source (same structure as services in `platform-services-kb`) |
| `boundary/` | Boundary classification markdown — manually authored, describes when to use this service |
| `openapi/` | OpenAPI specs (`.yaml` / `.json`) — optional, leave empty to skip the contracts library |

### 3. Trigger the sandbox

Go to **Actions → Sandbox KB → Run workflow** (select branch `main`).

The workflow will:
- Crawl `docs/` using the platform content crawler (runs on a self-hosted runner with Bedrock access)
- Publish a sandbox knowledge library to the Trimble Knowledge Service
- Publish `boundary/` directly as a boundary library
- Provision a per-repo AAIP virtual server combining all staging libraries + your new library
- Output the sandbox MCP URL in the job summary

### 4. Connect Cursor

Copy the **Sandbox MCP URL** from the job summary and add it to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "platform-kb-sandbox": {
      "url": "<sandbox_mcp_url from job summary>"
    }
  }
}
```

Your sandbox MCP server now includes all staging libraries **plus** your docs — ready to query via Cursor AI, skills, and agents.

### 5. Iterate

Update `docs/`, re-run the workflow. Each run replaces the previous sandbox library — no manual cleanup needed.

---

## Prerequisites

- Your GitHub account must be a member of `trimble-oss`.
- No credentials needed in this repo — all Trimble secrets stay in `platform-services-kb`.

## Template version

This repo calls `platform-services-kb` reusable workflow at tag `@v1`.
See [releases](https://github.com/trimble-oss/platform-services-kb/releases) for the latest tag and update `.github/workflows/sandbox.yml` if needed.

## Reference

- [Sandbox Pipeline Design](https://github.com/trimble-oss/platform-services-kb/blob/main/docs/architecture/designs/kb-sandbox-pipeline/design.md)
- [platform-services-kb](https://github.com/trimble-oss/platform-services-kb)
