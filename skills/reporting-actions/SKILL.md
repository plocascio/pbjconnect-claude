---
name: reporting-actions
description: Review PBJConnect reporting and improvement-action status counts, overdue work, recorded PBJ exports and receipts across authorized facilities.
---

Check `connection_status`, resolve facility names with `list_facilities`, and call `reporting_actions` for the requested scope. Omit facilities for the organization and follow every `nextOffset`.

Without a quarter, action counts cover all recorded periods and export status uses the returned last completed work quarter. With a quarter, actions match that exact recorded period. Explain that distinction when comparing results; do not silently filter out nonquarter action periods.

Prioritize returned overdue, urgent, high-priority and needs-correction counts. Use `review_quarter` for staffing/census readiness and `staffing_analysis` for daily hours and job classifications. Use `staffing_forecast` for saved improvement scenarios, rather than deriving a forecast from action status.

Action and export statuses are facility-team records. A prepared/downloaded file is not a submission; a recorded accepted status is not a live CMS query. Missing receipts remain unknown. The tools omit task narratives, assignee names and receipt identifiers. Do not infer who is responsible, invent action titles or imply the plugin changed a task.
