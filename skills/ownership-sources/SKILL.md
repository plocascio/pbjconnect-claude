---
name: ownership-sources
description: Read PBJConnect public CMS ownership, management roles, chain affiliations, licensed and certified beds, data coverage and saved CMS source-report history.
---

Check `connection_status` and use `list_facilities` to resolve names or exact CCNs within the authorized organization. Never use a shared CCN to bypass organization selection.

Use `facility_ownership` for public owners/managers, roles, percentages, association dates, chain affiliation and bed counts. An optional quarter is a publication-as-of selection. Current PBJConnect organization membership and current chain affiliation do not establish historical ownership. CMS-certified beds and state-licensed beds are separate fields. Blank ownership percentages remain unknown.

Use `data_coverage` to see saved source families and freshness. Original SQL/file hour-import counts are separate from committed staffing hours; do not add them together. Saved demo metadata does not prove a demo is still active or actual reporting is complete.

Use `cms_source_history` to find source reports and original public links. Filter a source kind or publication dates when useful. Read all facility pages and follow each facility's `recordPagination.nextRecordOffset` for the remaining source/owner records. A source's publication date, retrieval date and performance/work period are distinct. Undated files cannot prove historical as-of values. Source row counts can overlap between releases and are not unique people or total staffing hours.

Public owner names are permitted source records; resident and employee identities are outside this plugin. Return public source links and the portal link for saved-file downloads. Do not invent download URLs, expose private storage keys, or return uploaded report contents.
