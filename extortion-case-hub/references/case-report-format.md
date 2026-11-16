# Case report format

Back to [SKILL.md](../SKILL.md). Every value in a report must come from a delegation result. Write "unreadable", "undated", "inaudible" or "uncertain" instead of guessing.

## Indicator normalization

Normalize only for comparison; always show the value exactly as it appeared in the source next to the normalized form.

- Phone numbers: keep digits only and drop a leading Peru country code 51, so "+51 999 000 111" and "999000111" compare as equal.
- Bank accounts, interbank codes and wallet numbers: digits only.
- Aliases and group names: lowercase, no accents, no extra spaces.
- Amounts: number plus currency as printed (S/, soles, USD). Never add different currencies.
- Places: stop and street names as written; map to the route file only with the rules in [Cross-case rules](cross-case-rules.md).

Member identity data (their own phone numbers, ID numbers) is never treated as an indicator.

## 1. Driver report

1. Header: member label, period covered, folders processed, generated on, "Built from files stored on the NAS; not a police record."
2. Summary: number of incidents, first and last date, current escalation level with its justification, total cupos paid per currency.
3. Timeline: one row per incident, sorted by time. Columns: date and time (as printed, or file time marked as such), channel (voice note, chat, screenshot, photo, call memo, camera), verbatim excerpt, demand (amount, frequency, deadline), source file.
4. Indicators table: type, value as written, normalized value, first seen, last seen, source files.
5. What the extortioner knows: each personal detail mentioned (bus plate, route, schedule, family names, home address, school) with the source file. This is for the member's safety planning and for the police.
6. Cupos paid: one row per readable payment capture (date, amount, currency, destination as written, source file). Unreadable captures are listed but not summed.
7. Evidence index: file name, member folder, type, size, original times, media metadata when present, SHA-256.
8. Gaps: unreadable, undated, inaudible, failed or inaccessible items.

## 2. Company report

1. Header and scope: folders and members included, members shown by pseudonym unless the user chose real names, period, generated on.
2. Overview: members affected, incidents, distinct phone numbers seen, distinct collection accounts seen, total cupos paid per currency.
3. Escalation board: one line per member with level, date reached and justifying quote or image description.
4. Cross-member matches: grouped by strength as defined in [Cross-case rules](cross-case-rules.md), each with the members, the shared value and the source file of every occurrence.
5. Route segments: incidents per segment between consecutive stops of the route file; uncertain locations listed apart.
6. Per-member driver report sections 3 to 6, condensed.
7. Combined evidence index and gaps.
8. Closing statement: "Matches are verifiable coincidences between files. They do not establish that incidents are connected or who is responsible; that assessment belongs to the police and the prosecutor."

## 3. Indicator exchange file

Markdown, safe to hand to another company:

- Header: "Anonymized extortion indicator file", issuing company label chosen by the user, period, generated on.
- Collection accounts and wallet numbers (normalized).
- SHA-256 of threat files (images, audios, videos) received by members.
- Aliases and group names (normalized) and distinctive phrases (verbatim, at most 12 words each).
- Demand patterns: amount, frequency and payment day.
- Route segments with incident counts (stop names only).
- Phone numbers used by the extortioners, marked "low reliability: disposable numbers".

Never include member names or numbers, plates of member buses, file paths or file contents.
