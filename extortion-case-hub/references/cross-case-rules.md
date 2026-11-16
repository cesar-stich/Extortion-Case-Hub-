# Cross-case rules

Back to [SKILL.md](../SKILL.md). A match is a fact that two or more members' files contain the same value. It is never a conclusion about who is behind the threats.

## Match strength

| Strength | Shared value | Why |
|---|---|---|
| Strong | Identical file (same SHA-256 or same duplicate group from the scan) in two or more member folders | The exact same image, audio or video reached different members |
| Strong | Same collection account, interbank code or wallet number | Extortioners must receive money; accounts are harder to replace than phones |
| Medium | Same alias or group name | Groups sign threats so victims know who collects |
| Medium | Same distinctive phrase of at least 6 words, ignoring case and accents | Shared scripts |
| Medium | Same demand pattern: same amount per bus, same frequency and same payment day | Shared collection scheme |
| Low | Same extortioner phone number | Disposable lines; report it but never alone as a link |
| Not a match | Same district, same week, same common words, same generic insult | Context only; never list as a match |

Report the strongest evidence first. Two medium matches between the same members may be described as "several content coincidences", never upgraded to strong.

## Required wording

- Use: "The collection account ending 482 appears in files of Member A (IMG_0412.jpg) and Member B (PTT-20251007.opus, 0:42)."
- Never use: "same gang", "the same criminals", "confirmed link", "the suspect", or any name of a person as responsible.
- Always close the section with the statement in [Case report format](case-report-format.md).

## False-positive warnings to include when relevant

- Collection accounts are often third-party or rented accounts; a shared account suggests a connection but does not prove it.
- Caller numbers can be spoofed or reused.
- A forwarded file may have been shared by the members themselves; check the member statement before treating an identical file as received from the extortioner.
- OCR can misread digits; show the source image name so a person can check it.

## Cross-company check

Compare the current company report only against values present in the received indicator file. Report each match as "also present in the file shared by another company", with strength from the table above. Do not infer anything about the other company's members.

## Route segment mapping

1. The route file gives an ordered list of stops and streets.
2. A place mentioned in an incident maps to a stop only when the written name matches a stop name after normalization, or the text explicitly names two consecutive stops.
3. A street that crosses several segments, a nickname not in the route file or a misspelling with more than one candidate is "uncertain location".
4. Count incidents per segment (stop N to stop N+1). Never estimate positions or distances; there is no GPS or map data.
