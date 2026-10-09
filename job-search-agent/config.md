# Configuration

| Setting | Value |
|---|---|
| Runs on | Claude scheduled task (cloud, no local machine needed) |
| Schedule | Daily, about 8:00 AM ET |
| Model | Claude Sonnet |
| Session | Fresh session each run, no carried-over memory |
| Tools | Web search, web fetch, tracker database read/write |
| Notifications | Push notification when a run finishes |
| Output | New rows in the job tracker page |

## Design notes

- **Human in the loop:** the agent finds and drafts, the candidate decides and applies.
- **Stateless runs:** all state lives in the tracker, so a run can fail or be re-run without side effects beyond adding missing rows.
- **Append-only writes:** the agent never edits or deletes existing rows, so manual status updates are never lost.
