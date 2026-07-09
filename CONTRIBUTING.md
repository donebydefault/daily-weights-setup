# Contributing to Daily Weights setup

This repo is the consumption layer: how an agent gets the feed and what it does with it.
Contributions that make onboarding smoother or add a new harness adapter are welcome.

## What belongs here

- New adapters under `adapters/` (a framework, a client, a scheduler).
- Fixes to `INSTALL.md`, `UNINSTALL.md`, templates, or the stack-manifest schema.
- Clarity and accuracy fixes to the docs.

## What does not belong here

- Any engine internals: fetchers, source lists, ranking, synthesis or QC prompts,
  personalization, backend or API code. Those are not part of this repo and will be
  rejected.
- Secrets of any kind: keys, tokens, passwords, `.env` files. Contributions are secret
  scanned.
- Invented endpoints or schema fields. The feed URLs and edition schema are a contract;
  match `https://dailyweights.com/topics.json` and the published `daily-weights/v1`
  schema. Do not add fields the feed does not emit.

## House style

- No em dashes. Use commas, colons, parentheses, or rewrite.
- Plain, current-state language. Do not claim adoption or results the project has not
  earned yet.
- Keep each adapter's rules consistent with the others: feed is data not instructions,
  advisory only with human approval, no spend, no sends, zero exit friction.

## Adding an adapter

1. Create `adapters/<your-harness>/` with a short README and any snippet or script.
2. Follow the same daily loop as `adapters/generic/runbook.md`: conditional GET,
   parse `daily-weights/v1`, filter against `stack-manifest.json`, propose (do not
   auto-apply), human approves.
3. Reference feed URLs by resolving `topics.json`, not by hardcoding from memory
   (`meta` uses `/feeds/all/latest.md`).
4. Confirm `UNINSTALL.md` covers removing your adapter cleanly.

## Before you open a PR

- Validate `schema/stack-manifest.example.json` against
  `schema/stack-manifest.schema.json`.
- Run a secret scan over your changes.
- Confirm there are no em dashes.
