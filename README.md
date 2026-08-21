# Convertly Growth Operator

Convertly Growth Operator (`convertly-agent-stack`) is one universal advertising workflow for ChatGPT,
Codex, Claude, and other MCP-compatible agents:

| Layer | Responsibility |
| --- | --- |
| Convertly MCP | Salespage, TC, Untung, Daily, Doctor, Attribution, Growth OS memory, experiments, creative intelligence, and scale readiness |
| Agent image generation | Create ad images when the current agent supports native image generation |
| Cloudinary Asset Management MCP | Upload and manage approved media assets |
| Official Meta Ads MCP | Inspect and create campaign, ad set, creative, and ad objects |

The universal OpenAI plugin source is in `plugins/convertly-agent-stack`. It
packages the orchestration skill, Convertly OAuth MCP, official Meta Ads MCP,
and Cloudinary Asset Management MCP. The Claude Code compatibility manifest
shares the same orchestration skill.

## Install from ChatGPT Plugin Directory

After Convertly is approved in the public Plugin Directory:

1. Open ChatGPT Desktop, then open Plugins.
2. Search for `Convertly Growth Operator` and select Add.
3. Sign in to Convertly, choose the store, and approve access.
4. Authorize Meta Ads and Cloudinary when ChatGPT asks for them.
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

Restart Codex and approve the Convertly, Meta Ads, and Cloudinary OAuth
connections. Start a new task so the installed skill and MCP tools are loaded.

## Install in Claude Code

Paste this block into PowerShell. No Convertly key is needed:

```powershell
claude plugin marketplace add https://convertly.my/agent-stack.git --sparse .claude-plugin plugins/convertly-agent-stack
claude plugin install convertly-agent-stack@convertly
```

Restart Claude Code, run `/mcp`, and approve the Convertly, Meta Ads, and
Cloudinary OAuth connections. The orchestration skill is available as
`/convertly-agent-stack:convertly-ad-operator`.

Cursor and generic MCP clients do not share the Codex/Claude plugin format. Use
the manual three-server configuration shown in Convertly for those clients.

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
Convertly OAuth; they do not need an MCP key. The approved write scope only
stores or approves internal Growth OS artifacts and guardrails and cannot
publish or change Meta delivery. Meta Ads and Cloudinary use their own OAuth
approval flows after the plugin is enabled.

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
