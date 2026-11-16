# Validation plan

Back to [SKILL.md](../SKILL.md).

Status: the package passes the official static checker. Nothing has been run on a UGREEN AI NAS yet. This plan is for the single assigned finalist testing day.

## Test set (synthetic, built before the testing day)

The set mirrors the scenario in [Synthetic example](synthetic-example.md): one fictional bus company, five member folders, 33 evidence files and one route file. No real victim data is used.

- Voice notes: recorded by volunteers reading a written script in Peruvian Spanish, including slang, street noise and one deliberately inaudible clip.
- Screenshots, payment captures and exported chats: generated for the test and visibly marked "SYNTHETIC TEST".
- One handwritten note photographed with a phone.
- Planted facts with known answers: one collection account shared by Member A and Member B; one identical image in the folders of Member B and Member C; Member D unrelated; Member E sharing only district and week with Member A.

## Core test case 1: cross-member matches

Request: "Company extortion report for the last three weeks, with pseudonyms."

Expected:

- Strong match A-B on the shared collection account, with both source files named.
- Strong match B-C on the identical image, reported from the duplicate scan and confirmed by equal SHA-256 values.
- Member D and Member E listed under "No match found".
- No sentence stating that incidents are connected or naming anyone as responsible.

## Core test case 2: full report, save and custody

Request: the same company report, then "save it and preserve the originals in the case folder".

Expected:

- Timeline with verbatim excerpts and a source file for every row.
- Escalation board: Member B at level 4 with the note photo as justification.
- Cupos paid: S/ 420 from three readable captures; the unreadable capture listed and not summed.
- Route segments: four incidents between the two planted consecutive stops.
- The save and the copy each wait for platform approval; after approval the saved path is reported, every copy has the same SHA-256 as its original, and no original was moved, renamed or changed.

## Edge case: unreadable, undated, ambiguous and restricted

Inputs: the inaudible voice note, a cropped screenshot with no date, a place nickname that is not in the route file, and a request for the company report made from a member account that can open only its own folder.

Expected:

- The three items appear under Gaps as inaudible, undated and uncertain location.
- No amount, date, name or place is invented for them.
- The member account receives only its own driver report, and the other folders are listed as not accessible.

## Additional checks if time allows

- Update mode: add three new files and ask "what is new since the last report"; only those three are processed.
- Cross-company check: place a second synthetic indicator file on the NAS; only the planted shared account is reported as also present.
- Empty result: point the Skill at an empty folder; it reports zero files and stops.

## Metrics and targets

| Metric | Target |
|---|---|
| Planted matches reported | 2 of 2 strong, 2 of 2 medium |
| False links (D or E linked to anyone) | 0 |
| Cited original files with a SHA-256 value | 100% |
| Invented values for unreadable inputs | 0 |
| Copies whose checksum equals the original | 100% |
| Spanish voice notes with a usable transcript | measured and reported, no target claimed |
| Time from request to company report | measured and reported |

## Testing day schedule

1. First block: install the Skill, create the five member folders and one administrator, upload the test set.
2. Second block: run core test case 1 and the edge case; record results against the expected values.
3. Third block: run core test case 2 with the approval steps; verify checksums.
4. Fourth block: fix wording or batching problems in the Skill, rerun failed cases, record the demo video, back up logs and outputs before the reset.

Any expected result that fails is reported as a failure in the final documentation; it is not hidden.
