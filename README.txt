THT CUSTOMER SURVEY 2.1 — MASTER GOOGLE SHEET SYNC v7

DATA SOURCE (unchanged): THT Customer Survey 2.0 Master
Spreadsheet ID: 1NVbvqA1ldmIvKOS8p9c-3y_y0B-dahfH4pg9zTjHGSs

CHANGES:
- Existing original Web_Content now holds 7 Likert statements, 5 scale labels,
  per-item VI/EN explanations, overall satisfaction texts, and 5 overall explanations.
- getSurveyConfig requires the above content from Google Sheet (no silent stale fallback).
- Scoring_Methodology documents the methods; Data_Quality flags orphaned test rows.
- The old R1 historical dataset, calculations, all existing survey submissions,
  issue log, action tracker and clarifications remain unchanged.
- Legacy vs CSAT remains selectable in Admin; default is Legacy.
- Client keeps mobile UI, PIN Admin, and PDF report.

DEPLOY SEQUENCE:
1) Open the existing Apps Script project (Survey 2.0 webapp).
2) Replace Code.gs and Save.
3) Deploy > Manage deployments > Edit current active deployment > New version > Deploy.
4) Test ?action=apiInfo => 2026-10-16-likert-v7-mastersheet.
5) Test ?action=getSurveyConfig: questions[0].vi should be the new Likert statement;
   questions[0].explanations.vi must contain 5 texts.
6) Replace ONLY index.html in existing GitHub Pages repo. Keep assets/ intact.
7) Test Customer survey and Admin; do not treat orphaned historic test details as completed submissions.

CAUTION: The spreadsheet currently contains Survey_Detail test rows without
Survey_Response parent IDs. These records were not edited or repaired because
respondent and survey identity cannot be inferred safely.
