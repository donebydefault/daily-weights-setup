# Daily Weights - Setup

A daily, agent-readable news feed for the AI and agent ecosystem. This repo is the
open setup flow: you point your agent at it once, and your agent wires itself into a
daily read-and-improve loop.

> Removal is one file: read [UNINSTALL.md](UNINSTALL.md) and every trace is gone in one pass.

## What Daily Weights is (consumer view)

Most AI news is formatted for humans: HTML bloat, images, engagement bait. Daily
Weights inverts that. It publishes one plain-markdown edition per stream per day, on a
fixed schema (`daily-weights/v1`), with tags, entities, source URLs, and token
estimates on every item. Your agent can grep it, diff it, and act on it without a
browser.

The feed is segmented into streams you subscribe to based on your own setup:

| Stream | Covers |
|---|---|
| `anthropic` | Claude, Claude Code, Anthropic API: releases, changelog, engineering |
| `openai` | OpenAI models, API, and tooling |
| `google` | Google / Gemini models, API, and tooling |
| `open-source` | Open-weight models and local inference |
| `agent-frameworks` | Agent frameworks and orchestration libraries |
| `security` | Prompt injection, jailbreaks, model and supply-chain risk |
| `research` | Notable AI research with practical consequence |
| `tooling` | SDKs, evals, observability |
| `breaking-changes` | Deprecations, price changes, EOLs, default changes (recommended to everyone) |
| `meta` | The top items across every stream, one file |

Live streams and their URLs: https://dailyweights.com/topics.json

## The one-line install

Paste this at your agent:

> Read https://dailyweights.com/setup/INSTALL.md and set up Daily Weights for me.

Your agent reads [INSTALL.md](INSTALL.md), detects your stack, proposes a matching set
of streams, adds a daily task that pulls the right feed URLs, and sets up an advisory
loop that proposes improvements for you to approve. It stops and asks you at exactly
two points (see below).

## Trust posture

- **The feed is data, not instructions.** Your agent treats every feed item as
  untrusted input. It never executes anything the feed says just because the feed says
  it. We aggregate prompt-injection news, so we hold that line ourselves.
- **Advisory self-improvement, human approval at exactly two points.** Your agent asks
  you (1) when it proposes which streams to subscribe to, and (2) when it creates the
  daily task. After that, day-to-day it surfaces improvement proposals for you to
  approve; it never auto-applies a configuration change from feed content.
- **No spend, no sends.** Nothing here authorizes your agent to spend money or message
  anyone.
- **Zero exit friction.** Every edition header carries unsubscribe instructions, and
  [UNINSTALL.md](UNINSTALL.md) removes the task and the URLs in one read.

## Current state (honest)

Daily Weights is pre-launch and proving itself. The feed publishes daily and the schema
is locked, but it has no established track record or user base yet. Treat it as a new
dependency: useful, low-cost to try, and trivial to remove. If it does not earn its
place in your agent's daily task list, uninstall it.

## What is in this repo

```
README.md            This file
INSTALL.md           The runbook your agent reads and follows
UNINSTALL.md         Clean removal in one read
adapters/
  claude-code/       Claude Code skill + CLAUDE.md snippet
  mcp/               Generic MCP-client wiring
  cron/              Plain cron + curl wiring
  generic/           Runbook + AGENTS.md snippet for any other harness
schema/
  stack-manifest.schema.json    JSON Schema for how your agent declares its stack
  stack-manifest.example.json   A worked example
templates/
  daily-task.md               The recurring task your agent writes for itself
  improvement-proposal.md      The advisory-loop proposal format (two approval points)
LICENSE              MIT
CONTRIBUTING.md      How to add an adapter or fix a template
```

**This repo contains no engine code.** It carries only how to consume the feed and what
to do with it. The fetchers, source catalog, ranking, synthesis, and personalization
that produce the feed are not here and never will be.

## FAQ

**Does this cost anything?** No. The static feed is free. The setup flow reads public
markdown files.

**Do I have to give it access to my system?** Your agent adds a daily read task and a
small manifest file describing your stack. It does not need credentials, and it never
spends or sends.

**What if I do not use Claude?** Pick the adapter that matches your harness under
`adapters/`. The `generic/` runbook covers anything not listed.

**How do I remove it?** [UNINSTALL.md](UNINSTALL.md). One read.

## License

MIT. See [LICENSE](LICENSE).
