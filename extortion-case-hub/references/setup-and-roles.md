# Setup and roles

Back to [SKILL.md](../SKILL.md). This page describes how a transport company prepares its NAS so the Skill has something to read. Accounts, folders, permissions and phone backup are standard NAS features; the Skill does not create or change them.

## Who does what

| Role | What they do | What they can see |
|---|---|---|
| Member (driver or fare collector) | Stores threat material in their own folder | Their own folder and their own driver report |
| Administrator (owner, manager or association leader) | Asks for company reports, decides what to save and what to hand to the police or to another company | The member folders the NAS lets them open |
| Authorities | Receive the report and the preserved copies if the company or member decides to report | Only what is handed to them |

## One-time setup

1. The administrator creates one NAS account per member and one case folder with a subfolder per member. Each member can open only their own subfolder.
2. Each member installs the NAS mobile app and turns on backup of the phone folders where chat voice notes, chat images and screenshots are stored, pointing to their subfolder. Backup runs when the phone joins the depot wireless network, so it uses no mobile data.
3. The administrator stores a route file in the case folder: an ordered list of the stops and main streets of the route, one per line.

## Daily use by members

- Nothing to do when backup is on. Material is copied before a frightened member deletes it from the phone.
- To add a full conversation, the member exports the chat with media from the chat app into their subfolder.
- After a threatening phone call, the member records a short voice memo saying the date, time, caller number if seen, the amount and the deadline. The Skill labels it as a member statement.

## What is not captured

- View-once and disappearing messages.
- Phone calls themselves; only the memo the member records afterwards.
- Anything a member chooses not to store. Participation is the member's decision.

## Privacy defaults

- Company reports use pseudonyms unless the administrator chooses real names.
- The indicator exchange file never contains member data.
- Nothing leaves the NAS unless a person copies it out.
