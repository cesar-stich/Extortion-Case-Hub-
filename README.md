# Extortion Case Hub

**A private, on-device case hub that turns the extortion threats bus drivers receive into hash-verified, connected reports on their company's UGREEN AI NAS.**

An AI Skill for UGREEN AI NAS, built for the UGREEN Hackathon 2026 on AI NAS (Round 1).
Track: **Automate Your Workflow**. Skill name: `extortion-case-hub`.

## The problem

In Lima and Callao, most public transport is run by hundreds of private companies, each holding one fixed route and operating dozens of microbuses. Criminal groups charge these companies a daily "cupo" (protection money) per bus and shoot at the buses and depots of those who refuse.

The demands arrive as WhatsApp voice notes and messages from disposable numbers, photos of the bus or the driver's family, letters left at the depot and phone calls. Reporting falls short today because:

- the evidence is scattered across many personal phones and drivers delete it out of fear;
- phone numbers change constantly, so every complaint looks isolated;
- what reaches the police is a pile of loose files with no order and no proof of integrity.

Public figures: 26,585 extortion complaints in Peru in 2025 (22,361 in 2024); more than 85,000 complaints produced only 20 sentences in five years; transport leaders estimate about 80% of the roughly 400 urban transport companies in Lima and Callao are extorted, often by several groups at once. See [`extortion-case-hub/references/peru-context.md`](extortion-case-hub/references/peru-context.md) for the full context.

## What the Skill does

A company cannot stop the gangs, but it can control the quality of its own evidence. The company keeps a UGREEN AI NAS at its depot, with a private folder per driver. Drivers' phones back up their chat media to those folders. On request, the Skill reads every voice note, screenshot, exported chat, photo and payment capture, fingerprints each original with SHA-256 and produces:

1. **Driver report**: timeline, verbatim threats, indicators, escalation level, cupos paid and a SHA-256 evidence index, ready for a police complaint.
2. **Company report**: cross-member matches (same collection account, identical file, same alias or demand pattern), an evidence-based escalation level per member, total cupos paid and incidents per route segment.
3. **Anonymized indicator file**: another transport company can cross-check it on its own NAS, with no victim names and no files.
4. **Update mode**: only what is new since the previous report.

The Skill reports verifiable coincidences, never conclusions. It does not identify suspects, contact anyone, advise paying or file the complaint, and nothing leaves the NAS.

## How it uses the UGREEN AI NAS

The Skill only delegates to registered NAS expert agents. It never runs actions itself.

| Expert agent | What it does | Workflow step |
|---|---|---|
| `file-agent` | Inventory, cross-folder duplicate scan, SHA-256, approved copy with checksum verification | 1, 6, 9 |
| `photo-agent` | OCR and neutral description of screenshots, photos and payment captures | 2 |
| `knowledge-agent` | Spanish transcription of voice notes, saving reports, reading indicator files | 3, 9, 10 |
| `document-agent` | Cited extraction from exported chats, documents and the route file; formal draft for the complaint | 4, 8 |
| `security-monitor-agent` | Optional: depot camera events near the time of an in-person incident | 5 |

User accounts, per-driver folder permissions and phone backup over the depot Wi-Fi are native NAS features. All read steps run before any write, and every write waits for platform approval.

Why a NAS and not a cloud chatbot: the value comes from volume, privacy, multi-user folders and evidence integrity working together. Victims' evidence stays in-house, a driver can only obtain their own report, and all processing is local.

## Core user flow

1. Drivers' phones back up chat media to private NAS folders over depot Wi-Fi. After a threatening call, the driver records a short voice memo.
2. The manager asks Uliya for the company report.
3. The Skill confirms folders and period, runs the read steps and shows the report, including gaps.
4. After platform approval, it saves the report and copies the originals, verifying every checksum.

## Safeguards

- Matches are verifiable coincidences between files. They do not establish that incidents are connected or who is responsible; that assessment belongs to the police and the prosecutor.
- No accusations, no suspect names, no advice to pay, negotiate or confront.
- Never deletes, moves, edits or renames an original file; it only copies.
- Pseudonyms by default; respects NAS folder permissions.
- Unreadable or inaudible material is marked as such; nothing is invented.
- In case of immediate danger, the Skill first tells the user to call the police or emergency services.

## Current status

- **Implemented:** the full Skill package (`SKILL.md` plus seven references) passes the official Uliya Skill Kit static checker with 0 errors and 0 warnings. It includes the match rules, the escalation ladder, a complete synthetic example and a validation plan with known expected results.
- **Not implemented:** nothing has run on a NAS yet.
- **Pending validation if selected as a Finalist:** Spanish transcription quality, batching, approval flows, camera events.

## Validation plan

A synthetic five-driver data set with planted answers, all marked "SYNTHETIC TEST".

- **Core test 1:** exactly two strong matches are found (a shared collection account and an identical image) and none for two unrelated drivers.
- **Core test 2:** a full report is produced, then saved and the originals copied after approval, with every checksum matching its original.
- **Edge case:** an inaudible audio, an undated screenshot, an ambiguous bus stop and a restricted account. Gaps are listed, nothing is invented and the restricted member obtains only their own report.

Details: [`extortion-case-hub/references/validation-plan.md`](extortion-case-hub/references/validation-plan.md).

## Known limitations

- No voice or face biometrics.
- A match suggests, but never proves, a link: accounts can be borrowed and numbers spoofed.
- Transcription quality for slang-heavy Spanish is unverified.
- Phone calls and view-once messages are not captured; a call is only documented through the driver's own voice memo.
- File hashes support, but do not replace, official forensic examination.
- Drivers must choose to upload their files.
- Assumes the company or its association keeps a UGREEN AI NAS at the depot.
- No external dependencies and no data flows outside the NAS.

## Repository contents

| Path | Description |
|---|---|
| [`Extortion-Case-Hub_Round1-Proposal.pdf`](Extortion-Case-Hub_Round1-Proposal.pdf) | Round 1 proposal (ten answers) |
| [`extortion-case-hub.zip`](extortion-case-hub.zip) | Initial Skill Package, as submitted |
| [`extortion-case-hub/`](extortion-case-hub/) | Source of the Skill: `SKILL.md` and `references/` |

The package contains only original Markdown files: no scripts, executables, binaries, third-party code, models, media or datasets. All example data is synthetic.

### References inside the Skill

| File | Purpose |
|---|---|
| [`case-report-format.md`](extortion-case-hub/references/case-report-format.md) | Layout of the three outputs and indicator normalization |
| [`cross-case-rules.md`](extortion-case-hub/references/cross-case-rules.md) | Match strength, wording, false-positive warnings, route segments |
| [`escalation-ladder.md`](extortion-case-hub/references/escalation-ladder.md) | The four evidence-based escalation levels |
| [`synthetic-example.md`](extortion-case-hub/references/synthetic-example.md) | A complete synthetic company report |
| [`validation-plan.md`](extortion-case-hub/references/validation-plan.md) | Test cases with known expected results |
| [`peru-context.md`](extortion-case-hub/references/peru-context.md) | Background for readers outside Peru |
| [`setup-and-roles.md`](extortion-case-hub/references/setup-and-roles.md) | NAS setup, roles, phone backup and route file |

## Built with

UGREEN AI NAS, UGOS, the official UGREEN Skill Developer Package (Uliya Skill Kit 0.7.7) and its static checker, and Markdown.
