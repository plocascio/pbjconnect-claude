# PBJConnect for Claude

Compare staffing, census, quality measures, inspections and ownership across the facilities you authorize in PBJConnect. Review reporting gaps and saved staffing-star scenarios. PBJConnect retrieves and calculates the evidence; Claude explains it. Ask about an entire organization and its available history without choosing one facility or quarter first.

Version **0.3.0** provides eight workflows for the hosted server's **14 read-only tools**. It adds quality and inspection analysis, public ownership, source coverage and report history, daily staffing/job mix, and reporting-action summaries. The MCP connector is already published in Claude's directory. The separate plugin bundle was submitted previously; updated bundles remain subject to Anthropic's validation and review.

## Connect in Claude

1. Install the PBJConnect plugin from its directory listing when available, or upload the plugin folder as a ZIP under Claude's Plugins controls.
2. Open its Connectors tab and connect PBJConnect. For a custom connector, use `https://pbjconnect.com/api/integrations/mcp`.
3. Complete OAuth sign-in on PBJConnect. Automatic client registration is supported; no API key or client secret is needed.
4. Choose the organizations to share and approve on the PBJConnect consent page. Keep passwords and codes out of conversations.
5. Ask Claude to check the connection. The `connection_status` result must report `connected: true` before analysis.

An existing PBJConnect account with access to the requested organization is required. Your Claude plan and connector availability also apply. Installing the plugin does not create an account or add organization permissions.

## Install in Claude Code

```text
/plugin marketplace add plocascio/pbjconnect-claude
/plugin install pbjconnect@pbjconnect
```

Use `/mcp` to connect and complete the same organization consent. OAuth supports localhost and 127.0.0.1 callbacks with a variable port. Alternatively, clone this repository and load the folder with `claude --plugin-dir ./pbjconnect-claude`.

Repository: https://github.com/plocascio/pbjconnect-claude

## Workflows

- **Setup:** check access, selected organizations and connection management.
- **Portfolio analysis:** compare facilities and trends over requested dates or all available history; inspect daily staffing and PBJ job/pay-type mixes when supporting hour records exist.
- **Quality and inspections:** examine published measures, benchmarks, quality/inspection stars, deficiencies, penalties and QRP/VBP results.
- **Ownership and sources:** inspect public owners, management roles, chain affiliations, separate bed counts, data coverage and saved CMS report history.
- **Quarter review:** identify missing staffing days, zero-RN indicators, census gaps and recorded export/receipt status.
- **Census reconciliation:** compare saved PCC operational occupancy, billable ledger census, facility-recorded census and CMS-published daily census.
- **Staffing forecast:** explain saved scenarios, points, assumptions and supported improvement gaps.
- **Reporting and actions:** summarize recorded work by status, priority and overdue counts without task narratives or assignee names.

Try: "Compare staffing trends across my facilities over all available history," "Which facilities have recurring inspection tags?", "Show public ownership and when those sources were published," or "Review last quarter's reporting gaps."

## Every tool and what it returns

| Tool | Purpose and returned evidence |
| --- | --- |
| `connect_account` | Returns the existing authorization's PBJConnect management link. In the remote Claude connector it does not create a grant or expand access. |
| `connection_status` | Checks the current authorization and lists explicitly shared organizations and current roles. |
| `list_facilities` | Lists authorized IDs, names, states, CCNs and licensed beds; supports name/CCN search and facility pagination. |
| `analyze_portfolio` | Compares aggregate staffing, census, HPRD, published stars and turnover over available history or supplied dates. |
| `data_coverage` | Lists saved source families, covered periods, freshness, operational import counts and demonstration periods. Metadata and counts only, not file contents. |
| `staffing_analysis` | Returns daily staffing, matched census/HPRD, missing-day and zero-RN indicators, and PBJ job/pay-type breakdowns when supporting hour records exist. |
| `quality_measures` | Returns saved public MDS/claims measures, suppression, footnotes, matched benchmarks, quality-star trends and QRP/VBP results. |
| `health_inspections` | Returns saved public health/fire citations, scope/severity, recurring tags, corrections, inspection cycles, penalties and inspection-star trends. |
| `facility_ownership` | Returns public CMS owner/manager names, roles, percentages and association dates, chain affiliation, CMS-certified beds and separately recorded state-licensed beds. |
| `cms_source_history` | Lists saved public CMS report metadata, work/performance periods, publication/retrieval dates, row counts and original public links. No uploaded contents or private storage links. |
| `review_quarter` | Calculates staffing/census coverage, missing-day and zero-RN flags, and recorded export/receipt status for a work quarter. |
| `staffing_forecast` | Recalculates saved staffing-star scenarios from existing inputs and returns points, gaps, completeness, assumptions and methodology. Does not save changes. |
| `census_reconciliation` | Compares saved daily census series, differences, counting bases, coverage and retrieval times without resident details. Requires dates spanning at most 366 days per request. |
| `reporting_actions` | Returns reporting/improvement-action counts by domain, status and priority, overdue counts and recorded PBJ export/receipt status. |

Omitting facility IDs requests the authorized organization. Tools with pagination return continuation offsets; skills follow them rather than treating a first page as the complete portfolio. CMS publication quarters are distinct from PBJ work quarters. Source publication, performance/work period and retrieval dates remain separate.

## What runs, what is sent, and what is fetched

The bundle contains Markdown skills, JSON configuration and brand images. It has no hooks, executable scripts, local MCP process, SQL driver, shell commands or package-install dependencies. It does not inspect local files, environment variables or credentials. The optional Claude Code commands above install this repository; they do not install a database connector.

Claude sends the requested tool name and structured arguments, such as organization/facility IDs, dates, quarter, filters and pagination, to the HTTPS MCP endpoint at **pbjconnect.com**. Requests carry the OAuth authorization obtained through sign-in. The server does not request the conversation, Claude memory, local files, passwords or API keys. Authentication and organization consent also take place on **pbjconnect.com**.

The server reads saved, authorized records from PBJConnect and returns facility/organization aggregates and public CMS records. Those results become available to Claude for the answer. Source links may point to public CMS websites; reading those links is optional and is not a background import. The plugin does not directly sign in to PCC, iQIES, SQL Server or CMS, and does not start connector pulls. PBJConnect's deterministic calculations do not call a separate model API.

The service rechecks current membership and consented organizations on every request. An administrator's broader portal access does not broaden a Claude grant. Access lasts up to 90 days and can be revoked at https://pbjconnect.com/plugin/claude. To choose different organizations, disconnect and reconnect from Claude. Removed membership, a disabled account or a password reset can stop access.

## Evidence and limitations

Results distinguish published CMS history, operational uploads, saved PCC census and demo carry-forward records. Public owner names are public source records; resident and employee identities, clinical narratives, raw SQL rows, uploaded file contents and private download keys are excluded. Tools cannot run SQL/procedures, start imports, alter operational data, approve exports or submit to CMS.

Missing or suppressed data stays unknown, not zero. Census `connectorOnline: null` means there is no saved connector-health evidence; it does not mean offline. `false` reflects a saved inactive/stale connector observation. The response's retrieval/freshness dates show the evidence's age. Saved census can remain available when live detail is unavailable. PCC ledger census is not CMS-accepted MDS census.

A staffing forecast is an estimate from saved inputs, not an official overall CMS rating or a guarantee of CMS acceptance. Quality and inspection domains need their own evidence. A prepared file is not proof of submission, and recorded receipt status is not a live CMS query.

If access expires, reconnect through the host. Input and scope errors include the relevant status and next step; bounded responses identify pagination or a smaller requested scope. Temporary service errors do not establish a missing source or a zero value. Keep credentials and patient information out of support requests and public issues.

## Documentation and support

- Documentation: https://pbjconnect.com/plugin
- Privacy: https://pbjconnect.com/plugin/privacy
- Terms: https://pbjconnect.com/plugin/terms
- Support: https://pbjconnect.com/#contact
- Manage Claude access: https://pbjconnect.com/plugin/claude

The package remains proprietary under the included LICENSE and PBJConnect terms. Public access to this repository does not open-source the backend or include customer data. Directory publication and listing placement are decided by Anthropic.
