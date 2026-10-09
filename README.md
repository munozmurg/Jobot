# Job Search Agent

An AI agent that runs every morning, finds job postings that match what I'm looking for, and logs them to a tracker with a short note on why each one fits. It finds and drafts. I decide and apply.

![Job search tracker dashboard with sample data](images/tracker.png)

*The tracker dashboard, shown here with fictional sample data. Open `tracker.html` in a browser to try the demo.*

## Why I built it

Job searching was eating hours of my week, and most of that time went to scrolling through postings that were never a real fit. I wanted to automate the finding and filtering so I could spend my time on the roles I actually want and on making those applications stronger.

I deliberately stopped short of automating the applications themselves. Job boards block bots, the good roles need a tailored resume and answers, and I want to be the one choosing where I apply. So the agent does the searching and the first read, and I do the judgment.

It saves me about 10 hours a week.

## What it does

Every morning, the agent:

- Searches company job boards (Greenhouse, Lever, Ashby) and the web for my target roles
- Filters postings by role, location, and the type of work (see "Matching" below)
- Skips anything already in my tracker
- Writes a short "why it fits" and a "how to position myself" note for each new match
- Adds the new matches to my tracker with status `New`

I review the tracker, pick the roles worth pursuing, and update the status myself as I apply and interview.

### The dashboard

The tracker is where the agent's work turns into decisions. Each match shows the role, company, location, pay when posted, a link, and the agent's two notes. I move each one through a status (New, Reviewing, Applied, Interviewing, Offer, Rejected, Passed), and the counts at the top show where my search stands at a glance. A second tab, "Companies I like," keeps companies I want to watch even when they have no opening yet.

## How it works

1. **Load context.** Reads my profile: target roles, locations, company preferences, and background.
2. **Read the tracker.** Pulls every existing row to know what it has already found.
3. **Search.** Checks company job boards directly, then runs web searches.
4. **Filter.** Keeps only postings that match my criteria.
5. **Draft and log.** Writes the fit and positioning notes and adds new rows.
6. **Report.** Sends a short summary of what it added, or says plainly that nothing new matched.

It runs as a scheduled Claude task in the cloud, so it works whether or not my laptop is on.

### Matching

Beyond title and location, the main filter is the kind of role. I'm looking for roles where I define metrics and strategy and work with stakeholders and clients, not roles where I'd spend all day building and maintaining pipelines on my own. The agent screens for that, and also skips roles that require years of managing direct reports.

## Design choices

- **Human in the loop.** The agent never fills out or submits an application. Every application is a decision I make.
- **It never edits my rows.** The agent only adds new rows. It never changes or deletes an existing one, so my status updates and notes are never overwritten.
- **No duplicates.** A posting is skipped if its link or its company and role already appear in the tracker, even when the title is worded slightly differently.
- **Profile kept separate from the logic.** My personal details live in a profile file, not in the prompt. Anyone can reuse the agent by swapping in their own profile.
- **Honest about limits.** Web search only shows what is publicly indexed, so the agent reports what it actually found and doesn't claim full coverage.

## Files in this repo

| File | What it is |
|---|---|
| `tracker.html` | The dashboard. Opened locally, it runs as a demo with sample data |
| `images/tracker.png` | Screenshot of the dashboard |
| `prompt.md` | The full instructions the agent runs each morning |
| `profile.example.md` | Example profile showing the structure (fictional) |
| `tracker-schema.md` | The fields in each tracker row and who fills them |
| `config.md` | Schedule, model, tools, and design notes |
