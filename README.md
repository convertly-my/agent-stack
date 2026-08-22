# Convertly Growth Operator

Convertly Growth Operator (`convertly-agent-stack`) is one universal advertising workflow for ChatGPT,
Codex, Claude, and other MCP-compatible agents:

| Layer | Responsibility |
| --- | --- |
| Convertly MCP | Salespage, TC, Untung, Daily, Doctor, Attribution, Growth OS, scale readiness, and secure hosting for approved images |
| Native generation or user upload | Supply the approved creative from ChatGPT, Claude, or the merchant |
| Convertly Media Bridge | Gives an approved image a stable public Convertly URL when Meta requires one |
| Official Meta Ads MCP | Inspect and create campaign, ad set, creative, and ad objects |
| Cloudinary | Optional fallback for video, oversized files, or unsupported formats |

The universal OpenAI plugin source is in `plugins/convertly-agent-stack`. It
packages the orchestration skill, Convertly OAuth MCP with Media Bridge, and
official Meta Ads MCP. The Claude Code compatibility manifest
shares the same orchestration skill.

## Install from ChatGPT Plugin Directory

After Convertly is approved in the public Plugin Directory:

1. Open ChatGPT Desktop, then open Plugins.
2. Search for `Convertly Growth Operator` and select Add.
3. Sign in to Convertly, choose the store, and approve access.
4. Authorize Meta Ads. Convertly Media Bridge is already included for approved images.
5. Start with: `Audit my funnel and build the highest-leverage ad test. Do not publish yet.`

No terminal or Convertly MCP key is required. Until the directory review is
complete, use the direct connector flow below; it reaches the same Convertly
data but does not automatically install the campaign skill or the two execution
connectors.

## Connect directly in ChatGPT Desktop or Claude Desktop

This is the default merchant flow. It requires no API key, plugin command, or
terminal:

1. Open Connectors in ChatGPT Desktop or Claude Desktop.
2. Add a custom connector named `Convertly`.
3. Use `https://convertly.my/api/mcp` as the connector URL.
4. Click Connect, sign in to Convertly, choose the store, and approve access.

Convertly implements OAuth discovery, Dynamic Client Registration, PKCE,
short-lived access tokens, rotating refresh tokens, exact redirect matching,
and resource binding. Active desktop connections can be revoked in Convertly
under Integrations → API/Webhook → MCP.

The command-line flows below are advanced alternatives for coding agents.

## Install in Codex

Paste this block into PowerShell. No Convertly key is needed:

```powershell
codex plugin marketplace add https://convertly.my/agent-stack.git --sparse .agents --sparse plugins/convertly-agent-stack
codex plugin add convertly-agent-stack@convertly
```

Restart Codex and approve the Convertly and Meta Ads OAuth connections. Start a
new task so the installed skill and MCP tools are loaded.

## Install in Claude Code

Paste this block into PowerShell. No Convertly key is needed:

```powershell
claude plugin marketplace add https://convertly.my/agent-stack.git --sparse .claude-plugin plugins/convertly-agent-stack
claude plugin install convertly-agent-stack@convertly
```

Restart Claude Code, run `/mcp`, and approve Convertly and Meta Ads. The
orchestration skill is available as
`/convertly-agent-stack:convertly-ad-operator`.

Cursor and generic MCP clients do not share the Codex/Claude plugin format. Use
the Convertly and Meta configuration shown in Convertly. Convertly itself
provides the approved-image bridge.

## First prompts

After setup, paste one of these into the agent chat:

- Review my Convertly data for the last 7 days and explain the biggest problem
  in simple language.
- Create three ad angles based on my best Convertly sales page. Do not publish
  anything yet.
- Prepare a paused Meta campaign from the best angle. Ask me before activating
  or spending.

## Authentication

ChatGPT Desktop, Codex, Claude Desktop, and Claude Code authenticate through
Convertly OAuth; they do not need an MCP key. The approved write scope stores
or approves internal Growth OS artifacts and guardrails, and creates
short-lived Media Bridge upload sessions. It cannot publish or change Meta
delivery. Meta Ads uses its own OAuth approval flow.

## Images from ChatGPT or Claude

- ChatGPT may generate the creative natively. If the official Meta MCP accepts
  that file directly, Media Bridge is skipped.
- In Claude, the merchant can attach an existing image in chat. The agent uses
  that approved attachment directly when Meta supports it.
- When Meta requires a public image URL, the agent asks Convertly for a
  short-lived, single-use Media Bridge link. A capable coding agent uploads the
  attachment directly; a desktop-only user opens the link and chooses the
  approved image once. Convertly validates and converts it to WebP, then the
  agent passes the returned Convertly URL to Meta.
- Cloudinary is optional fallback infrastructure for video, files above 10MB,
  or formats not yet supported by Convertly Media Bridge.

Image generation is not represented as a fake remote MCP. Codex uses its native
image-generation capability when available. An agent without image generation
must return a production-ready prompt and stop before the asset-upload step.

Merchants without TrueConvert can still use the stack for salespage context,
copy, images, and paused Meta campaign planning. TC-dependent tool responses
return `trueconvert.state: not_configured`; the agent must disclose the missing
analytics and must not interpret empty metrics as zero performance.

## Default execution policy

- Read and planning work may run without a publishing approval.
- New Meta objects should be created paused or non-delivering where supported.
- Uploading an approved asset is a write and must match the user's requested
  workflow.
- Starting spend, raising budget, changing delivery, or activating ads requires
  explicit confirmation immediately before the action.
- Every completed external action must be backed by returned asset or Meta IDs.

## Growth OS prompts

- List the available Convertly growth playbooks and recommend one from my current evidence. Do not publish.
- Build a controlled CTA test, record the hypothesis and experiment, then prepare paused Meta objects.
- Evaluate campaign `CAMPAIGN_ID` for scaling using delivered TrueProfit, customer outcome, stock, creative depth, cooldown, and my budget constitution.
- Show me the exact approval packet for a safe scale step. Do not change Meta until I confirm.
