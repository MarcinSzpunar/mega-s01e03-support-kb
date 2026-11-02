## Problem

booking-v3 displays MM/DD/YYYY under its date field, while the form interprets input using the day-first tenant locale. Users following that hint can enter a date that the form reads with month and day reversed. This is separate from the shared parser bug and needs its own fix.

## Reports covered

33 unique reports in #4471 in the 2026-10-04 export, received 2026-04-17 through 2026-09-22. All are form-channel reports for booking-v3 tenants: Alder Physio (de-DE), Copper Studio (es-ES), and Pale Harbour (pt-PT). Intake tagged 18 as hint and 15 as parser; classification must use tenant locale, booking version and report channel.

Examples: R-41230 (Copper Studio, 1 June instead of 6 January), R-41241 (Alder Physio, 8 June instead of 6 August), R-41251 (Pale Harbour, 7 January versus 1 July).

## Fix and acceptance

Generate the hint from the same locale and format contract used to interpret the field. Verify booking-v3 with de-DE, es-ES and pt-PT, including ambiguous dates, and a month-first locale. Test booking-v2 and non-form channels independently; those do not belong to this group merely because their browser locale or subject matches.

## Evidence

src/lib/kb/causes.ts (DATE_HINT and causeOf), src/lib/kb/locales.ts, src/lib/data/tenants/*.json and deduplicated src/lib/data/reports-4471.json. The rendered CauseTable identifies these 33 as having no ticket of their own. Counts describe the exported snapshot, not the live queue.
