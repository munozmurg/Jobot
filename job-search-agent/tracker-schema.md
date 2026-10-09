# Tracker schema

The agent logs each posting as one document in the tracker's `applications` collection. The candidate updates `status` and `notes` by hand; the agent only ever creates new documents and never edits existing ones.

| Field | Filled by | Description |
|---|---|---|
| company | agent | Company name |
| role | agent | Job title as posted |
| track | agent | Which target track it matches (e.g. Solutions Engineer) |
| source | agent | Where it was found: Company site, LinkedIn, Indeed |
| location | agent | On-site city, hybrid, or remote |
| comp | agent | Posted salary range, blank if not listed |
| link | agent | URL to the posting |
| fit | agent | 2 to 3 sentences on why the role fits |
| angle | agent | 1 to 2 sentences on how to position for it |
| notes | candidate | Left blank by the agent |
| status | candidate | Starts as `New`; candidate changes it (Applied, Interviewing, Passed, etc.) |
| dateFound | agent | Date the agent found it, YYYY-MM-DD |
| addedBy | agent | Always `assistant` for agent-created rows |

## Dedupe rule

A posting is skipped if its normalized link OR its normalized (company, role) pair matches an existing row.
