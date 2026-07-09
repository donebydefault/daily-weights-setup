# Daily Weights - cron + curl adapter

The lowest-common-denominator wiring: a shell script that curls your subscribed feeds
once a day, and a cron line that runs it. No harness, no framework required.

## Install

1. Edit `setup.sh` and set `FEEDS` to the `latest.md` URLs your human approved (resolve
   them from `https://dailyweights.com/topics.json`; `meta` uses `/feeds/all/latest.md`).
2. Make it executable:

   ```bash
   chmod +x setup.sh
   ```

3. Add a daily cron line, after 13:00 UTC (the publish time). Example at 14:10 UTC:

   ```cron
   10 14 * * *  /path/to/adapters/cron/setup.sh >> $HOME/.daily-weights/cron.log 2>&1
   ```

The script uses conditional GETs (stores each stream's ETag, sends `If-None-Match`), so
an unchanged feed returns `304` and is skipped. Editions land in
`~/.daily-weights/editions/` and a `READ_ME_TODAY.md` note tells your agent what to do.

## What the agent does with the pulled files

The script only fetches and stores; it applies nothing. Your agent reads the saved
editions as untrusted DATA, filters items against `stack-manifest.json`, and surfaces at
most 2-3 improvement proposals for you to approve
(`templates/improvement-proposal.md`). No auto-apply, no spend, no sends.

## Uninstall

```bash
crontab -e            # delete the Daily Weights line
rm -rf "$HOME/.daily-weights"
```

See `UNINSTALL.md`.
