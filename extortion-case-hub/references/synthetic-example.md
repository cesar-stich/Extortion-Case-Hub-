# Synthetic example

Back to [SKILL.md](../SKILL.md).

> **Everything on this page is a synthetic, untested illustration.** The company, people, phone numbers, accounts, hashes, file names and quotes are invented. It was not produced on a NAS and it is not a device response. It only shows what the finished outputs are meant to look like.

## Scenario

"Line 47 (synthetic)" is an urban bus company with one fixed route. Five members stored evidence in their own folders on the company NAS between 2026-10-05 and 2026-10-25. The administrator asks: "Give me the company extortion report for the last three weeks, with pseudonyms."

Processed: 5 member folders, 33 evidence files (10 voice notes, 12 screenshots, 4 payment captures, 4 photos, 2 exported chats, 1 call memo) and 1 route file.

## Company report (excerpt)

**Extortion case report - Line 47 (synthetic)**
Period: 2026-10-05 to 2026-10-25. Members shown by pseudonym. Built from files stored on the NAS; not a police record.

### Overview

| Item | Value |
|---|---|
| Members affected | 5 |
| Incidents | 16 |
| Distinct extortioner phone numbers | 8 |
| Distinct collection accounts | 2 |
| Cupos paid (readable captures only) | S/ 420 from 3 captures; 1 capture unreadable and not summed |

### Escalation board

| Member | Level | Reached | Justification |
|---|---|---|---|
| Member B | 4 Physical act | 2026-10-23 | Photo taken by the member of a handwritten note left at the depot gate (IMG_B_012.jpg). Level 1 on 2026-10-06, 17 days earlier |
| Member A | 3 Explicit violence threat | 2026-10-15 | Voice note PTT_A_003.opus, 0:18: "si no pagas el lunes quemamos la unidad" |
| Member C | 3 Explicit violence threat | 2026-10-20 | Received photo showing ammunition on a table (IMG_C_004.jpg) |
| Member D | 1 Demand | 2026-10-09 | Screenshot SCR_D_001.png: single demand of S/ 5,000 |
| Member E | 1 Demand (member statement) | 2026-10-14 | Call memo MEMO_E_001.opus recorded by the member after a call |

### Cross-member matches

**Strong**

1. Same collection account. The account 000-0000001-0-01 appears in files of Member A (SCR_A_002.png; PAY_A_001.png) and Member B (PTT_B_002.opus, 0:42; PAY_B_001.png). The threats reached them from different phone numbers (999 000 111 and 999 000 112 for A; 999 000 221, 999 000 222 and 999 000 223 for B).
2. Identical file. IMG_B_009.jpg in the folder of Member B and IMG_C_004.jpg in the folder of Member C are the same file (same duplicate group, SHA-256 beginning 5f2c...e91a). Each member received it from a different number.

**Medium**

3. Same alias. "los sinteticos del norte" appears in files of Member A (PTT_A_001.opus, 0:05) and Member B (CHAT_B_001.txt, line 14).
4. Same demand pattern. Member A and Member B were both told S/ 20 per bus per day, payable every Monday.

**No match found**

- Member D: account 000-0000009-0-09, alias "el tio", number 999 000 441. None of these values appears in any other member folder.
- Member E: no account, alias, file or phrase shared with another member. Same district and same week as Member A are context only and are not a match.

Collection accounts are often third-party accounts and numbers can be spoofed. Matches are verifiable coincidences between files. They do not establish that incidents are connected or who is responsible; that assessment belongs to the police and the prosecutor.

### Route segments

Route file: ROUTE_LINE47.md, 20 stops. Seven incidents mention a place.

| Segment | Incidents | Sources |
|---|---|---|
| Stop 12 Mercado to Stop 13 Puente | 4 | PTT_A_003.opus, SCR_B_003.png, IMG_B_007.jpg, PTT_C_001.opus |
| Stop 05 Colegio to Stop 06 Grifo | 1 | SCR_D_002.png |
| Stop 01 Terminal (depot) | 1 | IMG_B_012.jpg |
| Uncertain location | 1 | PTT_A_004.opus says "la curva"; no stop with that name in the route file |

### What the extortioner knows

| Member | Detail mentioned | Source |
|---|---|---|
| Member A | Bus plate, route number, the time the first trip leaves | PTT_A_002.opus |
| Member B | Bus plate, home district, that a daughter attends a school (name withheld in this report) | CHAT_B_001.txt, lines 20 to 22; IMG_B_007.jpg is a photo of the bus at a stop |
| Member C | Bus plate | PTT_C_001.opus |

### Camera events

Depot gate camera, 2026-10-23, 02:10 to 02:25, America/Lima: one Vehicle event at 02:13 (motorcycle, plate not recognized) and one Human event at 02:14 (stranger). Recorded near the time Member B reported the note at the gate. This is not proof of who left it.

### Cupos paid

| Member | Date | Amount | Destination as written | Source |
|---|---|---|---|---|
| Member A | 2026-10-12 | S/ 140 | 000-0000001-0-01 | PAY_A_001.png |
| Member A | 2026-10-19 | S/ 140 | 000-0000001-0-01 | PAY_A_002.png |
| Member B | 2026-10-12 | S/ 140 | 000-0000001-0-01 | PAY_B_001.png |
| Member B | unreadable | unreadable | unreadable | PAY_B_002.png (not summed) |

### Evidence index (first rows)

| File | Folder | Type | Original time | SHA-256 |
|---|---|---|---|---|
| PTT_A_001.opus | Member A | audio, 0:31 | 2026-10-06 21:14 | 1a7d...03c2 (synthetic) |
| SCR_A_002.png | Member A | image | 2026-10-08 07:02 | 9be0...44af (synthetic) |
| IMG_B_009.jpg | Member B | image | 2026-10-19 22:40 | 5f2c...e91a (synthetic) |
| IMG_C_004.jpg | Member C | image | 2026-10-20 06:15 | 5f2c...e91a (synthetic) |

### Gaps

- PTT_E_002.opus: inaudible; no text extracted.
- SCR_E_003.png: cropped screenshot with no visible date; placed in the timeline by file time and marked "undated".
- PAY_B_002.png: amount and destination unreadable; not summed.
- PTT_A_004.opus: location "la curva" is uncertain.

## Indicator exchange file (excerpt)

Anonymized extortion indicator file. Issuer: "Urban bus company 1 (synthetic)". Period 2026-10-05 to 2026-10-25.

- Collection accounts (normalized digits): 0000000001001; 0000000009009.
- Threat file hashes: 5f2c...e91a (image).
- Aliases: "los sinteticos del norte"; "el tio".
- Demand patterns: S/ 20 per bus per day, Mondays; single demand S/ 5,000.
- Route segments: Stop 12 Mercado to Stop 13 Puente, 4 incidents.
- Extortioner phone numbers (low reliability, disposable): 8 values.

No member names, member numbers, bus plates, file paths or file contents are included.

## Cross-company check (excerpt)

The administrator of "Line 12 (synthetic)" places that file on their own NAS and asks for a cross-check. Result:

- Strong: the collection account 0000000001001 is also present in the file shared by another company; in Line 12 it appears in the files of Member K (SCR_K_005.png).
- No other value in the shared file appears in the Line 12 case folders.

The same closing statement applies: a shared value is a coincidence to hand to the authorities, not a conclusion.
