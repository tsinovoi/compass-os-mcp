<p align="center"><img src="logo.png" width="96" height="96" alt="Compass OS logo"></p>

# Compass OS MCP server

Compass OS, the Career OS, is also a remote MCP server. Connect it to the AI app you already use, and it answers from your own Compass OS account: your profile, wins, pipeline and interview stories, with Compass OS cards in the chat. Anything that would change your account waits for your yes.

This repository holds the connection docs only. The server is hosted by Compass OS; there is nothing to install or run.

| | |
|---|---|
| Server URL | `https://compass-os.dev/api/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth 2.1 (you sign in to Compass OS from your app) |
| Plan | A Compass OS account on **Plus or Pro** ([pricing](https://compass-os.dev/#pricing)) |
| Docs | [compass-os.dev/mcp](https://compass-os.dev/mcp) |
| Official MCP Registry | `dev.compass-os/compass` |

## Connect it

Every app uses the same address, and you sign in to Compass OS from your app. Don't paste a key or token; sign-in is OAuth.

### Claude

[Open in Claude](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Compass+OS&connectorUrl=https%3A%2F%2Fcompass-os.dev%2Fapi%2Fmcp) with Compass OS filled in. Check that the name is Compass OS and the address matches, then choose Add. Choose Connect, sign in to Compass OS, and allow access.

By hand:

1. In Settings, open Connectors and choose Add custom connector.
2. Name it Compass OS and paste `https://compass-os.dev/api/mcp`.
3. Choose Connect, sign in to Compass OS, and allow access.

### Claude Code

```sh
claude mcp add --transport http compass https://compass-os.dev/api/mcp
```

Then run `/mcp` in Claude Code, choose compass, sign in to Compass OS in the browser, and allow access.

### ChatGPT

1. In Settings, open Apps & Connectors and create a connector. Some plans ask you to turn on developer mode first.
2. Paste `https://compass-os.dev/api/mcp` and pick OAuth for sign-in.
3. Sign in to Compass OS when ChatGPT asks, and allow access.

### Gemini

1. In Settings, open Connected Apps and choose Add a custom app.
2. Paste `https://compass-os.dev/api/mcp` and choose Next.
3. Sign in to Compass OS when Gemini asks, and allow access.

### Cursor

In Cursor Settings, open MCP and choose Add custom MCP, or add this to `~/.cursor/mcp.json` (the same entry is in [`.mcp.json`](.mcp.json)):

```json
{
  "mcpServers": {
    "compass-os": {
      "url": "https://compass-os.dev/api/mcp"
    }
  }
}
```

Sign in to Compass OS in the browser when Cursor opens it, and allow access.

### VS Code

1. Run **MCP: Add Server** from the Command Palette and choose HTTP.
2. Paste `https://compass-os.dev/api/mcp` and name it compass.
3. Start the server, sign in to Compass OS in the browser, and allow access.

Or in `.vscode/mcp.json`:

```json
{
  "servers": {
    "compass": {
      "type": "http",
      "url": "https://compass-os.dev/api/mcp"
    }
  }
}
```

### Cline

See [llms-install.md](llms-install.md). In short, add this to `cline_mcp_settings.json` and authenticate the server when Cline asks:

```json
{
  "mcpServers": {
    "compass-os": {
      "type": "streamableHttp",
      "url": "https://compass-os.dev/api/mcp"
    }
  }
}
```

### Other MCP clients

1. Add a remote MCP server in your app's settings.
2. Paste `https://compass-os.dev/api/mcp`. Pick Streamable HTTP and OAuth if it asks.
3. Sign in to Compass OS when it asks, and allow access.

## What your AI app can see

Each answer comes from your own Compass OS account. Nothing else in your account is shared.

- **Your next step and your plan:** one card picked from your account: your next setup step, today's most urgent move, or what's due this week; or ask for any of the three. And your career plan: your goal, the gaps between your work and the roles you track for it, and this week's steps.
- **Your search:** every role you track and where it stands, a role's to-dos and notes, the best fits from your last scan, one role's posting, recruiter mail not yet matched to a job, companies you follow, and public web pages when you ask it to look something up.
- **Your profile and resume:** your profile, its gaps, Resume Studio's check, your master, tailored resumes and cover letters, your wins log and career timeline, your Rewind, your LinkedIn profile's audit, and your LinkedIn drafts in Brand studio.
- **Your interviews:** your story bank, practice progress and scored answers, practice cases and mock interviews to play in the card, saved interview prep and company research, and posted pay for the roles you search.

## What it changes only with your yes

Set or change your career goal; track a role from its posting and score your fit; move or remove a role; add a to-do or a note on a role, or check a to-do off; follow a company; edit your profile, a line at a time if you like, or call two roles at one company a promotion or a role change; draft a tailored resume or cover letter, or save your edits to one; apply Resume Studio's edits; update your LinkedIn headline and About; write or edit a LinkedIn draft; log, edit or delete a win; save an interview story; make interview prep and company research for a role. Your AI app can ask for any of these, but nothing saves until you press yes on the card. For 24 hours after, the card has an Undo button, and your AI app can ask to undo the change, again with your yes. A mock interview you play in the card saves its score when you choose to score and save it. Ask it to upgrade and the card shows Plus, Pro, the 7-day pass or a credit pack with its price and whether it renews; you pay on Stripe's page, never in the chat (ChatGPT links to the plans page instead). It never applies, posts or contacts the company.

In apps that don't show cards, you get the same answer as text, and a link to finish a change in Compass OS.

## Tools

The server's model-facing tools, as registered by the Compass OS MCP server on 2026-11-26 (from `src/lib/crew/tools.ts` and `src/lib/crew/mcp.ts` in [tsinovoi/compass-os](https://github.com/tsinovoi/compass-os)). Writes wait for your yes on a confirmation card.

### Reads

- `get_next_step` — Your next setup step, today's most urgent move, or the week's plan; or one card picked from your account
- `career_plan` — Your career goal, the gaps for that goal, and this week's steps on the plan
- `list_pipeline` — Every role you track, with stage, Requirements match, and a link to its card
- `find_jobs` — The best untracked roles from your last scan, ranked by Role fit
- `get_job` — One role's posting, pay, stage and score, from the pipeline or the last scan
- `list_todos` — A tracked role's to-dos, next step, and job-page history
- `search_web` — Search the open web for roles, companies or people
- `read_page` — Read one public web page, and pull out a posting's details when it is one
- `list_inbox` — Recruiter mail not yet matched to a job, and upcoming interviews
- `get_profile` — Your profile, one section, one role, or its gaps
- `list_wins` — Your wins log
- `get_career_timeline` — Your career as a timeline of employers and wins
- `get_rewind` — A Rewind of your wins (year, role, career or date range), with share images
- `check_resume` — Resume Studio's check on the master resume or a tailored resume
- `get_material` — The master resume, or a tracked role's tailored resume or cover letter
- `list_stories` — Your interview story bank
- `get_interview_prep` — Saved interview prep and company research for a tracked role
- `get_pay_range` — Posted pay for the roles you search
- `list_companies` — Companies you follow, with new roles and posted pay
- `audit_linkedin` — The score of your saved LinkedIn headline and About, with the top fixes (Compass OS's copy, not LinkedIn itself)
- `list_brand_posts` — Your LinkedIn drafts, scheduled and published pieces in Brand studio
- `get_practice` — Your practice path, streak and scored answers
- `list_cases` — Practice cases and recent mock interview scores
- `start_mock_interview` — Start a ready-made mock interview in a card; the score saves when you finish in the card

### Writes (wait for your yes)

- `set_goal` — Save or change your career goal
- `upgrade` — Open a Stripe payment page for Plus, Pro, the 7-day pass or a credit pack; nothing is charged in the chat. Not listed in ChatGPT, which gets a link to the plans page instead
- `track_job` — Add a role to your pipeline and, given a posting URL, save the posting and score your fit
- `move_job` — Move a tracked role to another stage
- `remove_jobs` — Remove tracked roles
- `add_todo` — Add a to-do on a tracked role
- `complete_todo` — Check off a to-do on a tracked role
- `add_note` — Add a dated note on a tracked role
- `update_profile` — Replace a profile section or a role's accomplishments
- `add_profile_line` — Add one accomplishment line to a role in your profile
- `link_roles` — Record whether two roles at the same company were a promotion, a role change, or separate jobs
- `update_linkedin` — Save a new LinkedIn headline and/or About for you to paste; never posts to LinkedIn
- `log_win` — Log a win
- `edit_win` — Edit a logged win
- `delete_win` — Delete a logged win
- `edit_resume` — Apply a Resume Studio edit (fix, shorten, add keywords, or improve a bullet)
- `tailor_material` — Draft a tailored resume or cover letter for a tracked role
- `edit_material` — Save your own edits to the master resume or a role's resume or cover letter
- `add_story` — Save a new interview story
- `make_interview_prep` — Make or remake interview prep and/or company research for a tracked role
- `follow_company` — Follow a company so new roles and posted pay are checked weekly
- `create_draft` — Save a new LinkedIn draft in Brand studio; never posts
- `edit_draft` — Edit a LinkedIn draft in Brand studio; never posts
- `undo` — Put back a save from the last 24 hours, again with your yes

## Privacy

What you ask and what the app answers stay between you and your AI app; Compass OS records which tool ran, not what was said. Disconnect an app anytime in Compass OS Settings, under Connected apps.

- Privacy policy: https://compass-os.dev/privacy
- Terms: https://compass-os.dev/terms

## Support

support@compass-os.dev

## License

The docs in this repository are MIT licensed. Compass OS itself is a hosted service under its [terms](https://compass-os.dev/terms).
