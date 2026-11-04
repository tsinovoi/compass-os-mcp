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
| Official MCP Registry | `io.github.tsinovoi/compass-os` |

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

- **Today and this week:** your next setup step, the one most urgent move, and what's due this week.
- **Your search:** every role you track and where it stands, the best fits from your last scan, one role's posting, recruiter mail not yet matched to a job, and public web pages when you ask it to look something up.
- **Your profile and resume:** your profile, its gaps, Resume Studio's check, your master, tailored resumes and cover letters, your wins log and career timeline, your Rewind, your LinkedIn profile's audit, and your LinkedIn drafts in Brand studio.
- **Your interviews:** your story bank, practice progress and scored answers, practice cases and mock interviews to play in the card, saved interview prep and company research, and posted pay for the roles you search.

## What it changes only with your yes

Track a role from its posting and score your fit; move or remove a role; edit your profile; draft a tailored resume or cover letter, or save your edits to one; apply Resume Studio's edits; update your LinkedIn headline and About; write or edit a LinkedIn draft; log, edit or delete a win; save an interview story; make interview prep and company research for a role. Your AI app can ask for any of these, but nothing saves until you press yes on the card. It never applies, posts or contacts the company.

In apps that don't show cards, you get the same answer as text, and a link to finish a change in Compass OS.

## Tools

The server's tools, as listed by `tools/list` on 2026-11-04:

`today`, `week`, `next_step`, `readiness`, `pipeline`, `find_jobs`, `job_details`, `track_job`, `move_job`, `remove_jobs`, `inbox`, `pay_range`, `web_search`, `read_page`, `get_profile`, `update_profile`, `add_profile_line`, `profile_gaps`, `link_roles`, `career_timeline`, `resume_check`, `edit_resume`, `get_material`, `tailor_material`, `edit_material`, `wins`, `log_win`, `edit_win`, `delete_win`, `rewind`, `linkedin_audit`, `update_linkedin`, `brand`, `create_draft`, `edit_draft`, `story_bank`, `add_story`, `practice`, `cases`, `mock_interview`, `interview_prep`, `make_interview_prep`

## Privacy

What you ask and what the app answers stay between you and your AI app; Compass OS records which tool ran, not what was said. Disconnect an app anytime in Compass OS Settings, under Connected apps.

- Privacy policy: https://compass-os.dev/privacy
- Terms: https://compass-os.dev/terms

## Support

support@compass-os.dev

## License

The docs in this repository are MIT licensed. Compass OS itself is a hosted service under its [terms](https://compass-os.dev/terms).
