# Daily Weights - UNINSTALL

Removal is one read. Do these steps and every trace of Daily Weights is gone. There is
no account to close, no server-side state to clear on the free feed, and nothing that
keeps running after you delete the task.

## Steps

1. **Delete the daily task.** Remove the scheduled task, hook, or cron entry that pulls
   the feed URLs. Find it by whichever adapter you installed:
   - Claude Code: remove the Daily Weights skill and delete the `CLAUDE.md` snippet you
     added (`adapters/claude-code/`).
   - MCP client: remove the Daily Weights task and, if you added the paid MCP server,
     remove that server entry (`adapters/mcp/`).
   - Cron + curl: `crontab -e` and delete the Daily Weights line; delete the pull
     script (`adapters/cron/`).
   - Generic runbook: remove the daily task you created per `adapters/generic/`.

2. **Remove the feed URLs.** Delete every `dailyweights.com/feeds/...` URL from your
   agent's task list, notes, or config.

3. **Delete the manifest.** Remove the `stack-manifest.json` file you created during
   install. Nothing else reads it.

4. **Delete stored editions and proposals (optional).** If your daily task saved
   editions or improvement proposals to disk, delete that folder. Keeping it does no
   harm; it is inert markdown.

5. **Email push (only if you signed up for it).** If you added the human email digest,
   unsubscribe at `https://dailyweights.com/unsubscribe`. If you only used the agent
   feed, skip this; there was never any subscription to cancel.

## That is all

No background process survives the steps above. No further fetches happen once the task
is deleted. If you want it back later, paste the one-line install again:

> Read https://dailyweights.com/setup/INSTALL.md and set up Daily Weights for me.
