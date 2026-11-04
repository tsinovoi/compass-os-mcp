# Install Compass OS in Cline

Compass OS is a hosted (remote) MCP server. There is nothing to clone, install, build or run locally, and no API key to set.

## Steps

1. Open Cline's MCP settings file (`cline_mcp_settings.json`: MCP Servers, then Configure) and add this entry inside `mcpServers`. Keep `"type": "streamableHttp"`; without it Cline falls back to the older SSE transport.

   ```json
   {
     "mcpServers": {
       "compass-os": {
         "type": "streamableHttp",
         "url": "https://compass-os.dev/api/mcp",
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

   Or use the Remote Servers tab: name `compass-os`, URL `https://compass-os.dev/api/mcp`, transport Streamable HTTP.

2. Sign in. The server uses OAuth. When Cline asks you to authenticate the server, a Compass OS sign-in opens in your browser. Sign in and allow access. Do not add an `Authorization` header by hand.

3. You need a Compass OS account on the Plus or Pro plan. Plans: https://compass-os.dev/#pricing

4. Check it works: ask "Where do my applications stand?" or "What should I do next?"

## Notes for the agent

- Do not create or ask for an API key, token or environment variable. Sign-in is OAuth only.
- Anything that would change the user's account (tracking a role, editing the profile, drafting a resume) waits for the user to confirm it.
- If the server shows as unauthenticated, the user hasn't finished signing in yet. Ask them to authenticate the server in Cline and sign in to Compass OS.

Privacy policy: https://compass-os.dev/privacy
