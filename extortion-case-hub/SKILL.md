---
name: extortion-case-hub
description: Private, on-device extortion case hub for urban public transport companies whose drivers and fare collectors receive "cupo" (protection money) threats. It turns the voice notes, chat screenshots, exported chats, photos, payment captures and optional camera events that members store on the company NAS into hash-verified reports - one per driver for the police complaint, and one per company with cross-member indicator matches, escalation levels, cupos paid and the route segments where incidents cluster - plus an anonymized indicator file other transport companies can cross-check. Use when a transport company owner, manager or driver says they are being extorted or threatened, asks for an extortion or cupo report, asks what is new since the last report, or wants to compare their case indicators with another company.
---

# Goal

In Lima and other Peruvian cities most urban public transport is run by private companies, each operating a fixed route with dozens of microbuses. Criminal groups charge drivers and companies a daily "cupo" per bus and enforce it with threats, shootings and murders. Threats arrive as chat voice notes, messages, screenshots, photos of the bus or the driver, notes left at the depot and phone calls. Phone numbers are disposable, the material is scattered across many phones, drivers delete it out of fear, and when someone finally reports, the police receive loose files that are hard to verify and impossible to connect.

This Skill runs on the company NAS and does the part the company controls: collect, read, preserve, connect and report. It produces:

1. **Driver report**: one member's timeline, verbatim threats, indicators, escalation level, cupos paid, what the extortioner knows about them, and a SHA-256 evidence index, ready for a police complaint.
2. **Company report**: all members the requesting administrator may access, with indicator matches between members, escalation per member, total cupos paid, and incident counts per route segment.
3. **Indicator exchange file**: an anonymized list of collection accounts, file hashes, aliases, distinctive phrases and route segments that another transport company can cross-check on its own NAS, with no victim names and no files.
4. **Update mode**: only what is new since the previous report.

What the Skill never does: it does not decide that cases belong to the same group, does not identify or name suspects, does not contact anyone, does not advise paying or negotiating, does not send real-time alerts and does not file the complaint. A match only states a verifiable fact, for example "the same collection account appears in the files of members A and B"; the assessment belongs to the police and the prosecutor. It never deletes, moves, edits or renames an original file.

# Required input

Ask only what the chosen mode needs, in the language of the user, and keep answers verbatim.

1. **Mode** (required): driver report, company report, update since the last report, export indicator file, or cross-check another company file.
2. **Evidence folders** (required): the company case folder and the member subfolders the user names. For a driver report, only that member folder. Do not guess paths and do not add folders the user did not name.
3. **Period** (required): start and end dates. In update mode, the date of the previous report, which the user gives or which appears in a saved report the user points to.
4. **Route file** (optional, company report): a document the company keeps with the ordered list of stops and main streets of its route.
5. **Audio language** (required when there are voice notes): normally Spanish; the transcription action uses `other` for Spanish.
6. **Names in the company report** (required for company report and export): real member names or pseudonyms such as Member A. Default to pseudonyms when the user does not choose.
7. **Cameras** (optional): whether the depot or offices have cameras on the NAS, with the date, time window and camera location of any in-person incident.
8. **Output folder** (only for saving): a NAS folder the user names.
9. **Other company file** (only for cross-check mode): the NAS path where the user placed the indicator file received from another company.

Never ask for passwords, banking credentials or any contact detail of the extortioner.

# Generation-time capability evidence

- `ug-filesystem` → `file-agent`
- `ug-filemgr` → `file-agent`
- `file-workflow` → `file-agent`
- `ug-photo` → `photo-agent`
- `ug-knowledge` → `knowledge-agent`
- `ug-document` → `document-agent`
- `ug-surveillance` → `security-monitor-agent`

Actions relied on at generation time: `find`, `stat`, `sha256sum`, `mkdir`, `cpmv` with copy type (ug-filesystem); `batch-transfer` in copy mode (file-workflow); `scan-dedupe`, `mediainfo` (ug-filemgr); `vision-ocr`, `vision-vlm` (ug-photo); `audio-transcription`, `process-materials`, `save-text` (ug-knowledge); `qa` with the extraction intent and `writing` with the formal style (ug-document); `event-timeline`, `event-evidence` (ug-surveillance).

Read these references when building reports:

- [Case report format](references/case-report-format.md): layout of the three outputs and indicator normalization.
- [Cross-case rules](references/cross-case-rules.md): match strength, wording, false-positive warnings and route segment mapping.
- [Escalation ladder](references/escalation-ladder.md): the four evidence-based escalation levels.
- [Synthetic example](references/synthetic-example.md): a complete, synthetic and untested company report.
- [Validation plan](references/validation-plan.md): test cases with known expected results.
- [Problem context](references/peru-context.md): background on cupo extortion of public transport in Peru, for readers outside the country.
- [Setup and roles](references/setup-and-roles.md): how the company prepares member folders, phone backup and the route file; read it when the user asks how to start.

# Workflow

The parent Skill only delegates. It never runs CLI actions itself and must not call `cli.invoke`. Every step passes only the real result returned by the upstream step to the downstream step. Before sending a delegation, write the confirmed folders, dates, paths and values as literal text in place of the descriptions used below. A report covers only the folders the requesting NAS user can access. If an expert reports that a folder is denied, list it as not accessible and continue with the rest; never look for another way to read it.

## Step 1: inventory and identical files (file-agent, read only)

`delegate --target file-agent --instruction 'Inside only the evidence folders the user named in this conversation, find every audio, image, video, text and document file created or modified between the start and end dates the user confirmed. Return for each file the real path, the member subfolder it belongs to, file type, size, creation time and modification time. Then run one duplicate scan across all of these member folders together and return every group of identical files, showing which member folders contain each copy. Do not open, change, move, rename or delete anything and do not search outside these folders. If there are no results, say explicitly that zero files matched.'`

- Zero files reported explicitly: say nothing was found for those folders and dates, show what was searched and stop. Do not widen the folders or dates on your own.
- Empty or unparseable result without an explicit zero: report that the inventory could not be verified and stop.
- An identical file found in two or more member folders is recorded as a cross-member match (see [Cross-case rules](references/cross-case-rules.md)). Read one copy per group and list every copy in the evidence index.
- Large sets: send at most 20 images, 10 audio files or 60 documents per delegation, in time order, and tell the user how many batches there are.

## Step 2: screenshots and photos (photo-agent, read only)

`delegate --target photo-agent --instruction 'For exactly these image files from the inventory, which are possible chat screenshots, payment captures or photos received by bus drivers in an extortion case: the real image paths returned by the inventory, listed one by one. For each image run OCR and return the full visible text without correcting it, plus every phone number, bank account or wallet number, amount, currency, date, time, name, alias, bus plate, street or bus stop name visible. Then give a short neutral description of what the image shows, for example a chat screenshot, a payment receipt, a photo of a bus, a person, a house front, a handwritten note or an object, without guessing who is involved. Mark text you cannot read as unreadable. Do not create albums, tags or copies and do not change any file.'`

## Step 3: voice notes and call memos (knowledge-agent, read only)

`delegate --target knowledge-agent --instruction 'Transcribe exactly these audio files from an extortion case involving bus drivers: the real audio paths returned by the inventory, listed one by one. The spoken language is Spanish, so use the other language option, and separate up to two speakers. Return each transcript with its path and the start time of each segment, keep the words exactly as spoken including insults and slang, and mark inaudible parts as inaudible instead of guessing. Some files are short memos where a driver describes a threatening phone call right after it happened; transcribe them the same way. Do not save transcripts to the NAS in this step.'`

Label memos recorded by a member as **member statement**, separate from threats received directly. Cite audio excerpts with the segment start time when the expert returns it. If the platform pauses the transcription for approval, wait for it as described under Completion and failure.

## Step 4: exported chats, documents and the route file (document-agent, read only)

Only when the inventory contains text exports or documents, or the user gave a route file:

`delegate --target document-agent --instruction 'Read exactly these files: the exported chat logs and documents returned by the inventory for this extortion case, and the route file the user named, if any. Using extraction with source citations, list every message or passage that contains a demand for money, a threat, a deadline, a phone number, a payment account or wallet number, an alias, a bus plate, a person name or a place. For each item return the date and time as written, the sender as written, the verbatim text and the file with its line or page. From the route file return the ordered list of stops and streets exactly as written. Do not summarize away exact wording and do not change any file.'`

## Step 5: camera events (security-monitor-agent, read only, optional)

Only when the user said there are cameras and gave a date, time window and camera location:

`delegate --target security-monitor-agent --instruction 'For the camera location and time window the user gave in this conversation, in the America/Lima time zone, list the timeline of Human and Vehicle events with event ID, time, camera, topic and whether the face or plate is known or a stranger, and return snapshot or clip evidence for those events for user review. Do not register, rename or delete faces or plates and do not change any recording. If there are no events in that window, say explicitly that zero events matched.'`

Report camera events only as "recorded near the time of the incident", never as proof of who made a threat.

## Step 6: integrity record (file-agent, read only)

`delegate --target file-agent --instruction 'For exactly these original files, which will be cited in an extortion case report: every real path kept from the inventory and the reading steps, listed one by one. For each file return the SHA-256 checksum, size, creation and modification times, and for audio, image and video files the media metadata such as capture time, duration, device model and location when present. Do not change, copy or move any file.'`

## Step 7: build the reports (parent, no NAS writes)

Using only facts returned by the upstream steps, build the requested output with [Case report format](references/case-report-format.md), [Cross-case rules](references/cross-case-rules.md) and [Escalation ladder](references/escalation-ladder.md):

- timeline sorted by time, with verbatim excerpts and source file for every item;
- indicators table, normalized as described in the format reference;
- what the extortioner knows about each member (plates, route, family names, addresses mentioned);
- escalation level per member with the quote or image that justifies it;
- cupos paid, summed per currency only from readable payment captures;
- company report only: cross-member matches by strength, incidents per route segment, and members shown by pseudonym unless the user chose real names;
- gaps: unreadable, undated, inaudible, uncertain location, inaccessible folders and failed files.

Show the result in the language of the user with a short content warning, and state that matches are facts for the authorities to assess, not conclusions.

## Step 8: formal complaint document (document-agent, approval required, optional)

Only when the user asks for a formal version of a driver report:

`delegate --target document-agent --instruction 'Write a formal Spanish complaint support document as a new draft copy, using the formal style, from the following driver report text without adding facts, removing quotes or changing numbers, dates, hashes or file names: the full driver report built in this conversation. Return the path of the draft copy.'`

## Step 9: save and preserve (approval required, optional)

Only after the user agrees and names an output folder:

1. `delegate --target knowledge-agent --instruction 'Save the following Markdown text as a new note with the filename hint extortion-case-report inside the output folder the user named in this conversation. Do not overwrite any existing file and return the verified saved path. Text to save: the full report built in this conversation.'`
2. `delegate --target file-agent --instruction 'Create a subfolder named original-evidence inside the output folder the user named in this conversation, then copy as one approved batch, never move, each of these original files into it, renaming on conflict instead of overwriting: every real path listed in the evidence index of the report. Then return the SHA-256 checksum of each copy next to the checksum of its original and list any file that failed or whose checksums differ.'`

A copy is verified only when both checksums match. A saved note is not proof that it is already searchable in the knowledge index.

## Step 10: indicator exchange (optional)

- **Export**: build the anonymized indicator file defined in [Case report format](references/case-report-format.md) from a finished company report, show it to the user, and save it only with Step 9.1 after approval. It must contain no member names, no phone numbers of members, no file contents and no file paths.
- **Cross-check**: `delegate --target knowledge-agent --instruction 'Read only the indicator file the user placed at the NAS path given in this conversation, which was received from another transport company, and return its full text exactly as written. Do not save, index or change anything.'` Then compare it with the current company report using [Cross-case rules](references/cross-case-rules.md) and report each match as "also present in the file shared by another company".

The Skill never sends the indicator file anywhere. People decide whether and how to hand it over.

# Completion and failure

Check every delegation result before starting dependent work.

- `completed`: continue only when the result contains what the next step needs (paths after Step 1, text after Steps 2 to 4, checksums after Step 6, a saved path or copy list after Steps 8 and 9). If a required value is missing, say the step completed without usable data and stop the steps that depend on it; never guess or fill in content.
- `failed`: stop the dependent steps, tell the user which step and which expert failed and the safe error facts, and keep everything already confirmed. A failed transcription or camera query becomes a gap; it does not block the rest of the report.
- `cancelled`: report the step as not done. Do not retry automatically, because a repeated save or copy can duplicate files. Offer to try again only if the user asks.
- `waiting_user`: relay the question of the expert, wait for the answer and let the same delegation resume; do not start a parallel task.
- `waiting_approval`: writing a draft, saving and copying need platform approval. Wait for the platform approval flow; agreement in the chat is not a substitute. After it resumes, check the final terminal result before saying anything was written, saved or copied.

Partial results: list separately what was processed, what failed, what is waiting and what was blocked; every count and total must say it covers only processed files.

Empty result: if nothing matches, say so plainly and stop. Do not switch to other folders, dates or similar files on your own.

Safety and privacy: all processing stays on the NAS; never send files, transcripts or indicators to an outside service. Respect the NAS permissions of the requesting user: a member who can open only their own folder receives only their own driver report, even when they ask for the company report. Never delete or alter originals. Do not advise paying, negotiating or confronting anyone. If the user reports immediate danger, first tell them to contact the police or emergency services, then continue only if they want to.
