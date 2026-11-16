# Problem context: extortion of public transport in Peru

Back to [SKILL.md](../SKILL.md). This page explains, for readers outside Peru, the situation the Skill is designed for. It is background only; the Skill does not need it to run.

## How urban transport works in Lima and Callao

- Most daily trips are not served by a state operator. They are served by hundreds of private companies, each holding one fixed route and running dozens of microbuses and vans along it.
- A company is a small organization: an office, a depot where buses park overnight, a manager, and dozens of drivers and fare collectors who often own or rent their unit.
- The depot is where drivers meet every day and where a company NAS would sit.

## What a "cupo" is

A cupo is protection money. Criminal groups demand a fixed amount, usually per bus and per day, from the company or from each driver. Demands arrive as chat voice notes and messages from disposable phone numbers, as photos of the bus, the driver or the family, as letters left at the depot and as phone calls. Refusal is answered with shots at buses or depots, burned units and murders of drivers in front of passengers.

## Scale

- Peru recorded 26,585 extortion complaints in 2025, up from 22,361 in 2024 (INEI with National Police data, reported by Exitosa Noticias).
- More than 85,000 extortion complaints led to only 20 sentences in five years (Caretas).
- Martin Ojeda, general manager of the interprovincial transport association, said in a broadcast interview that Lima and Callao have about 400 urban transport companies, about 80% subject to extortion, more than half by one or two groups and some by four or five; the longer the route, the more groups a company faces. He also described a driver shortage of 30 to 35%, with about 2,500 drivers leaving each year.
- Hector Vargas, president of the Coordinadora de Empresas de Transporte Urbano, said on Exitosa that nearly all transport operators in Lima and Callao live in fear and are extorted by two or three gangs at once.
- Television reports in the same period showed three companies stopping service after threats: an extortion letter left for one company, a driver shot in front of passengers, shots fired from a motorcycle at a depot gate hitting seven buses, and a demand of 30,000 soles. One company said it was considering paying because it saw no other way out.
- Drivers interviewed at a protest said they keep working because they have families, while checking the mirrors in fear; one company had just lost a driver.

Transport workers have stopped the city several times in protest against extortion.

## Why reporting falls short today

- Evidence is scattered across the personal phones of many drivers.
- Drivers delete threats out of fear, or because the extortioner orders it.
- Phone numbers change constantly, so each complaint looks like an isolated case.
- What reaches the police is a set of loose files with no order and no proof of integrity.

## How each fact shaped the Skill

| Fact | Design decision |
|---|---|
| Several gangs extort the same company | Matches are graded and kept separate; the Skill never merges everything into one group |
| Disposable phone numbers | Matching relies on collection accounts, identical files, aliases and demand patterns |
| Longer routes face more groups | Incidents are counted per route segment |
| Letters left at depots, attacks on depot gates | OCR of photographed notes; optional depot camera events |
| Companies paying because they see no alternative | A report they can hand over, and a record of cupos paid |
| Fear of leaks and retaliation | Local processing only, pseudonyms by default, member opt-in |

## Assumption to state plainly

The Skill assumes a transport company or association keeps a UGREEN AI NAS at its office or depot. This is an assumption about adoption, not an observed fact.

## Source note

The figures and statements above come from official statistics and published press and broadcast interviews. The entrant conducted no interviews for Round 1 and could not independently verify the statements made by the interviewees.
