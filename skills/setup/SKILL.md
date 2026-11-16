---
name: setup
description: Connect PBJConnect to Claude, check authorized organizations, change shared organizations, or revoke access.
---

Use this plugin's PBJConnect MCP tools; host prefixes can vary.

1. Call `connection_status` first. When connected, use its returned organization IDs and current roles. Never infer membership from a name or email.
2. If the remote connector is disconnected, ask the user to open PBJConnect's Connectors tab in Claude and connect. The server is `https://pbjconnect.com/api/integrations/mcp`. It uses OAuth with automatic client registration, not an API key. The user signs in on PBJConnect and chooses organizations there.
3. After the user finishes, call `connection_status` again. Only claim success when it reports `connected: true`.
4. `connect_account` returns the management link for the existing authorization. It does not grant additional access. To change organizations, the user reconnects from Claude and chooses them on PBJConnect's consent screen.
5. Never request passwords, API keys, one-time codes, cookies, or database credentials in chat. Never invent tokens, disable authentication, or use another service as a substitute if connection fails. Report the actual error.

This connection returns facility and organization aggregates. It does not return individual resident or employee records, run SQL or procedures, start imports, alter operational records, or submit to CMS. PBJConnect rechecks current membership and approved organizations on every request. Grants expire after 90 days and can be revoked at the returned management URL.

After confirming access, suggest a relevant question such as comparing facility trends, reviewing a quarter, reconciling saved census, or explaining saved staffing forecasts. Do not run a broad analysis unless requested.
