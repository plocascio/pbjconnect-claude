# PBJConnect for Claude

Ask questions about staffing, census, quarter readiness and saved staffing forecasts across your authorized PBJConnect organizations. The hosted tools retrieve and calculate evidence; Claude explains the results. No local SQL driver or API key is required.

The hosted integration and all seven tools were tested in Claude and the official MCP Inspector on November 16, 2026. Sign-in, organization consent, token renewal and disconnection/reconnection worked. Aggregate results were compared with PBJConnect. Release 0.2.1 adds public repository installation and marketplace metadata to the tested 0.2.0 plugin; the tools and skills are unchanged. Public source availability does not imply an approved Anthropic directory listing.

## Connect

1. Upload this ZIP in Claude under Customize > Plugins > Add > Upload plugin.
2. Open the plugin's Connectors tab and add/connect PBJConnect. For a custom connector, use `https://pbjconnect.com/api/integrations/mcp`.
3. Use OAuth sign-in with automatic client registration. No client secret is required.
4. Sign in on PBJConnect, choose the organizations to share, and approve. Keep passwords and codes out of conversations.
5. Ask Claude to check your PBJConnect connection. It must report connected before using your data.

## Install in Claude Code

Run these commands in Claude Code:

```text
/plugin marketplace add plocascio/pbjconnect-claude
/plugin install pbjconnect@pbjconnect
```

Then use `/mcp` to connect PBJConnect and complete the same organization consent. OAuth supports the documented localhost and 127.0.0.1 callback on a variable port. You can also clone this repository and load it with `claude --plugin-dir ./pbjconnect-claude`.

Repository: https://github.com/plocascio/pbjconnect-claude

## Workflows

- Setup: confirm connection and selected organizations.
- Portfolio analysis: compare facilities across the dates requested or all available history.
- Quarter review: identify missing staffing days, census coverage and recorded submission feedback.
- Census reconciliation: compare saved PCC physical occupancy, billable ledger census, facility-recorded census and CMS-published counts.
- Staffing forecast: explain saved scenarios, assumptions and improvement gaps.

Try: "Compare staffing trends across my facilities over all available history," "Review last quarter's reporting gaps," or "Compare PCC and CMS census for July through September 2026."

## Access and data

The server uses your current PBJConnect membership and the organizations you selected at consent. Its tools return aggregates with source dates, missing-data warnings and demonstration labels. They do not return resident or employee identities, run SQL or procedures, change operational data, refresh connectors or submit to CMS. Missing data is not a confirmed zero; a staffing forecast is not an official overall CMS rating.

Access lasts up to 90 days. Manage or revoke it at https://pbjconnect.com/plugin/claude. To choose different organizations, disconnect and reconnect from Claude. A disabled account, password reset or removed membership stops effective access.

PBJConnect calculations do not call a model API. Your Claude and PBJConnect account requirements still apply. Tools execute on the hosted PBJConnect service; the plugin bundle contains no credentials or customer data.

Documentation: https://pbjconnect.com/plugin

Privacy: https://pbjconnect.com/plugin/privacy

Terms: https://pbjconnect.com/plugin/terms

Support: https://pbjconnect.com/#contact

Directory listing and publication are subject to Anthropic review. The package remains proprietary under the included LICENSE and existing PBJConnect terms; public access to this repository does not open-source the server or include customer data. Report product or security issues through the support link above; do not include credentials or patient information in public issues.
