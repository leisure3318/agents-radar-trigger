# agents-radar-trigger

`leisure3318/agents-radar` is a **fork**, and GitHub disables `schedule`
(cron) events on forked repositories — confirmed empirically: every run of
its `daily-digest.yml` so far has been a manual `workflow_dispatch`, never
an automatic `schedule` run.

This standalone repo (not a fork, so its own cron works normally) runs a
daily schedule and calls the GitHub API to dispatch
`leisure3318/agents-radar`'s `daily-digest.yml` via `workflow_dispatch`.

## One-time setup (required — only you can do this)

The trigger needs a token with permission to dispatch workflows on
`leisure3318/agents-radar`. Create a fine-grained Personal Access Token:

1. Go to https://github.com/settings/personal-access-tokens/new
2. **Repository access** → "Only select repositories" → `leisure3318/agents-radar`
3. **Permissions** → Repository permissions → **Actions: Read and write**
4. Generate the token, copy it
5. In **this repo** (`agents-radar-trigger`) → Settings → Secrets and
   variables → Actions → New repository secret:
   - Name: `DIGEST_REPO_PAT`
   - Value: the token you just copied

Once the secret is set, the workflow runs daily at 23:37 UTC (≈ 07:37 CST)
and triggers the digest — no more manual clicking.

You can also trigger it manually any time via the Actions tab
("Run workflow" on "Trigger agents-radar daily digest").
