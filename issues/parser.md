## Problem

The shared parser treats dates as MM/DD even for day-first tenants. A booking for 7 April becomes 4 July (R-41200). The tenant locale, not the reporter's browser locale, determines the expected format.

## Reports covered

379 unique reports in the 2026-10-04 export are classified as parser, across 11 tenants, received 2026-04-01 through 2026-10-04. The export has 427 rows but only 412 report IDs; overlapping export pages must not count twice. The other 33 reports belong to the separate form-hint problem.

Of these 379 reports, 356 carry the parser intake tag and 23 carry the hint intake tag. Those tags are intake guesses, not root-cause evidence.

## Unresolved evidence

Five reports remain counted in the parser group by the supplied classification logic but do not establish month/day reversal: R-41202 (12 May versus 11 May), R-41209 (June bookings one day off), R-41236 (invite before booking), R-41344 (Lisbon Tuesday versus Toronto Monday), and R-41620 (6 October versus Monday). Investigate date-only/timezone conversion and event ordering before assuming the parser fix resolves these. The export establishes 374 other parser-classified reports and five unresolved exceptions, not a confirmed third root cause.

## Fix and acceptance

Parse using the tenant's documented date convention or unambiguous ISO dates. Verify day-first locales with dates such as 07/04 and 04/07, all report channels, and both booking versions. Ensure month-first tenants remain correct. Re-test the five exceptions independently.

## Evidence

src/lib/data/reports-4471.json; src/lib/data/tenants/*.json; src/lib/data/desk-notes.json; src/lib/kb/causes.ts (causeOf, uniqueById); rendered CauseTable for #4471. Snapshot counts are not current support-queue totals.
