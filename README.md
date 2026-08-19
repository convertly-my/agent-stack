# Convertly Agent Stack

Convertly Agent Stack packages one governed advertising workflow for Codex and
Claude Code:

| Layer | Responsibility |
| --- | --- |
| Convertly MCP | Salespage, TC, Untung, Daily, Doctor, and Attribution intelligence |
| Agent image generation | Create ad images when the current agent supports native image generation |
| Cloudinary Asset Management MCP | Upload and manage approved media assets |
| Official Meta Ads MCP | Inspect and create campaign, ad set, creative, and ad objects |

The plugin source is in `plugins/convertly-agent-stack`. It has client-specific
MCP files because Codex and Claude Code use different environment-header
configuration shapes, while sharing the same orchestration skill.

## Install in Codex

Set `CONVERTLY_MCP_KEY` in the user's environment, then run:

```bash
codex plugin marketplace add https://convertly.my/agent-stack.git --sparse .agents --sparse plugins/convertly-agent-stack
codex plugin add convertly-agent-stack@convertly
```

Restart Codex and approve the Meta Ads and Cloudinary OAuth connections. Start
a new task so the installed skill and MCP tools are loaded.

## Install in Claude Code

Set `CONVERTLY_MCP_KEY` in the user's environment, then run:

```bash
claude plugin marketplace add https://convertly.my/agent-stack.git --sparse .claude-plugin plugins/convertly-agent-stack
claude plugin install convertly-agent-stack@convertly
```

Restart Claude Code, run `/mcp`, and approve the Meta Ads and Cloudinary OAuth
connections. The orchestration skill is available as
`/convertly-agent-stack:convertly-ad-operator`.

Cursor and generic MCP clients do not share the Codex/Claude plugin format. Use
the manual three-server configuration shown in Convertly for those clients.

## Authentication

Set `CONVERTLY_MCP_KEY` to the plaintext `mcp:read` key generated in Convertly.
Never place the key in a committed file. Meta Ads and Cloudinary use their own
OAuth approval flows after the plugin is enabled.

Image generation is not represented as a fake remote MCP. Codex uses its native
image-generation capability when available. An agent without image generation
must return a production-ready prompt and stop before the asset-upload step.

## Default execution policy

- Read and planning work may run without a publishing approval.
- New Meta objects should be created paused or non-delivering where supported.
- Uploading an approved asset is a write and must match the user's requested
  workflow.
- Starting spend, raising budget, changing delivery, or activating ads requires
  explicit confirmation immediately before the action.
- Every completed external action must be backed by returned asset or Meta IDs.
