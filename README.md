![NetSentry](https://img.shields.io/badge/NETSENTRY-Criminal_Network_Analysis-1a1a2e?style=for-the-badge&labelColor=0f3460&color=e94560)
![SIH](https://img.shields.io/badge/SIH_2026-PS_26189-blue?style=for-the-badge&labelColor=16213e&color=0f4c75)
![Team](https://img.shields.io/badge/Team-F--ups-orange?style=for-the-badge&labelColor=16213e&color=f38181)

# 🕸️ NetSentry — Prototype Build Plan
### *Turning disconnected data into actionable intelligence*

---

## 🎯 What NetSentry Does (one breath)

NetSentry ingests scattered, disconnected police data — FIRs, call detail records (CDRs), financial transactions, surveillance logs, social media intel — and automatically builds a **connection graph** showing who is linked to whom, flags the most central/suspicious people in that network, and explains *why* each flag was raised. What used to take an investigator weeks of manual cross-referencing happens in minutes.

---

## 🌟 What's New / Your Two USPs

![USP1](https://img.shields.io/badge/USP_1-Alias_%26_Identity_Resolution-6a0572?style=flat-square)

**The problem it solves:** Criminals appear across records under different spellings, transliterations, or nicknames (*"Mohd. Aslam"*, *"Md Aslam"*, *"Aslam Bhai"*, *"अस्लम"*). Most graph tools built for clean Western data silently fail here — they treat these as different people, breaking the entire point of the system.

**What you'll build:** a fuzzy + phonetic matching layer that scores how likely two records are the same person, merging them into one graph node with a visible confidence score — instead of guessing silently.

![USP2](https://img.shields.io/badge/USP_2-Cross--Jurisdiction_Linking-ab3428?style=flat-square)

**The problem it solves:** Police databases across departments/states don't share a schema and often can't legally or technically talk to each other. A criminal network spanning two states looks like two unrelated smaller networks today.

**What you'll build:** a linking layer that unifies entity records from independently-structured "departments" — resolving shared phone numbers, vehicles, or resolved identities across them — **without needing a shared ID system.**

**Why judges remember this:** it directly answers the objection every judge has in their head — *"this only works if the data is already clean and centralized"* — with a working counter-example.

---

## 🏗️ Architecture Overview

```
┌─────────────┐      ┌──────────────────┐      ┌────────────────┐
│  Data Layer │─────▶│  Resolution Layer │─────▶│   Graph Layer   │
│ (synthetic  │      │ (alias matching + │      │ (Neo4j: nodes,  │
│  FIRs/CDRs/ │      │ cross-jurisdiction│      │  relationships) │
│  txns, 2-3  │      │  entity linking)  │      │                 │
│  "depts")   │      └──────────────────┘      └────────┬────────┘
└─────────────┘                                          │
                                                          ▼
                                              ┌────────────────────┐
                                              │   Analysis Layer    │
                                              │ (centrality, risk   │
                                              │  scoring, anomaly   │
                                              │  detection)         │
                                              └─────────┬──────────┘
                                                          │
                                                          ▼
                                              ┌────────────────────┐
                                              │  API Layer (FastAPI)│
                                              └─────────┬──────────┘
                                                          │
                                                          ▼
                                              ┌────────────────────┐
                                              │ Frontend (React +   │
                                              │ D3.js/Vis.js graph, │
                                              │ entity detail panel)│
                                              └────────────────────┘
```

---

## 🧩 Team Workstream Ownership

![Backend](https://img.shields.io/badge/WORKSTREAM-Backend_%26_Graph-0f4c75?style=flat-square) **Meer Mohammed Shoaib** — Neo4j setup, graph schema, FastAPI backend, integration glue

![AI](https://img.shields.io/badge/WORKSTREAM-AI_%2F_NLP_%2F_USPs-6a0572?style=flat-square) **Mohammed Maaz** — Alias resolution engine (USP 1), cross-jurisdiction linking (USP 2), NER, risk scoring

![Frontend](https://img.shields.io/badge/WORKSTREAM-Frontend_%2F_Visualization-ab3428?style=flat-square) **Prithvi S** — React app, graph visualization, entity detail panel, styling

![Data](https://img.shields.io/badge/WORKSTREAM-Data_Engineering-f38181?style=flat-square) **Sadiya Bareera** — Synthetic dataset design, department schema variation, alias/edge-case seeding

![QA](https://img.shields.io/badge/WORKSTREAM-QA_%2F_Integration-2b9348?style=flat-square) **Rabiya Kauser** — End-to-end testing, error-proofing, edge cases, demo rehearsal coordination

![Presentation](https://img.shields.io/badge/WORKSTREAM-Docs_%2F_Presentation-f7b32b?style=flat-square) **Nabiya Banu** — Slide polish, talking points, backup video recording, research/references, Q&A prep

> Two people (Sadiya, Nabiya) can work with daily coding load if needed but are **critical path owners** of two things demos always underestimate: realistic data and a bulletproof pitch. Don't skip their tracks to "help with code" — a broken demo from bad data or a fumbled pitch loses more points than a missing feature.

---

## 📅 Day-by-Day Plan

### 🗓️ Day 1 — Foundations

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Set up Neo4j AuraDB Free instance, store credentials in `.env`. Design graph schema on paper: node types (Person, Phone, Vehicle, BankAccount, Location, Department) and relationship types (CALLED, OWNS, TRANSACTED_WITH, LOCATED_AT, REPORTED_BY). Share schema doc with the team.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Research and shortlist fuzzy/phonetic matching libraries (`rapidfuzz`, `jellyfish`, `indic-transliteration`). Write 5-10 sample name-pairs (e.g. "Mohd. Aslam" vs "Aslam Bhai") to test matching approach before building the real module.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Set up React project (Vite), install Tailwind CSS, `react-force-graph`/`vis-network`, `axios`. Build a static placeholder graph with dummy nodes to confirm the visualization library works before real data exists.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Design the fictional criminal network on paper first: 3-4 core criminals, associates, shared phones/vehicles/accounts. Decide which 2-3 "departments" exist and what each one's data will look like.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Set up shared GitHub repo, `.gitignore` (critical: exclude `.env`), project structure, and a shared task tracker (Trello/Notion/GitHub Projects) mirroring this plan.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Review Slide 6 references (Neo4j docs, spaCy docs, Isolation Forest) and compile a one-page "why we chose this tool" cheat sheet the team can quote from during Q&A.

---

### 🗓️ Day 2 — Data & Backend Skeleton

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Write the Neo4j Python loader script (`neo4j` driver) to push nodes/relationships from CSV into the graph. Test with Cypher queries in Neo4j Browser to confirm structure.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Build the alias resolution module skeleton: `resolve_entities(record_a, record_b) -> confidence_score`. Implement phonetic matching first (`jellyfish`), test against Sadiya's planted alias pairs.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Build the entity detail side-panel UI (static/mock data for now) — name, aliases, connections list, risk score, explanation text placeholder.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Generate the full synthetic dataset using Python `Faker` for background noise + your hand-planted core network. Deliberately write the same person differently across 2 departments. Deliver as CSV/JSON.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Write a basic test checklist (what "working" means for each module) so every feature has a pass/fail definition from day one, not just "looks okay."

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Draft the presentation narrative arc (hook → problem → USP 1 demo → USP 2 demo → impact → close) so the team knows what story the app needs to visually support.

---

### 🗓️ Day 3 — Alias Resolution (USP 1) Complete

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Set up FastAPI project skeleton: `/entities`, `/entities/{id}`, `/graph` routes (mock responses for now). Add Pydantic models for request/response validation.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Finish alias resolution: add `rapidfuzz` fuzzy string scoring, combine with phonetic score into a weighted confidence. Add the human-in-the-loop rule: auto-merge above 85%, flag for review between 60-85%, ignore below.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Wire the graph visualization to load from a local JSON file (not live API yet). Add color-coding by risk score (green/yellow/red).

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Validate the dataset against Maaz's resolution module — run it through and check whether planted aliases are actually being caught. Adjust data if matches are too easy or too hard.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Begin integration testing between Meer's backend skeleton and Prithvi's frontend — confirm they can talk to each other with mock data before real logic is plugged in.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Write the exact talking-point script for the USP 1 (alias resolution) demo moment — see Section 9 below for base material to adapt.

---

### 🗓️ Day 4 — Cross-Jurisdiction Linking (USP 2)

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Build schema-mapping config (JSON/YAML) so each department's differently-named columns map to one internal entity model. Wire Maaz's resolution modules into the actual data pipeline feeding Neo4j.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Build cross-jurisdiction linking: exact-match hard identifiers (phone/vehicle/account) first, fallback to alias resolution score. Tag every cross-jurisdiction relationship with which departments contributed and confidence level.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Add jurisdiction color/badge indicators on nodes so cross-jurisdiction links are visually obvious at a glance (e.g. a small flag icon showing "linked from 2 departments").

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Double check the deliberately-mismatched schemas across departments are realistic, and stress-test with an extra "hard case" (e.g. a person with zero shared hard identifiers, only a weak alias match) to make sure the demo has a genuinely impressive moment.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Test the cross-jurisdiction pipeline end-to-end with Sadiya's hard case. Log every failure mode found so far into the shared tracker.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Write the exact talking-point script for the USP 2 (cross-jurisdiction) demo moment.

---

### 🗓️ Day 5 — NER, Risk Scoring & Explainability

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Connect FastAPI endpoints to the real Neo4j graph (replace mocks). Add try/except error handling with clean JSON error responses on every route.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Add spaCy NER + regex for phone/vehicle patterns to extract entities from free-text FIR narratives. Implement centrality scoring (Degree, Betweenness) via the Neo4j Graph Data Science library, plus a templated plain-English explanation generator.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Connect frontend to the real FastAPI backend (replace local JSON). Handle loading states and empty states gracefully.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Write a couple of realistic free-text FIR narrative paragraphs (not just structured fields) for the NER step, to prove the system handles messy real-world input, not just clean spreadsheets.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Run the full pipeline end-to-end for the first time today (data → resolution → graph → API → frontend). Document every break point.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Start building the final presentation deck slides that will host the live demo — where the switch to the live app happens, and what's said immediately before/after.

---

### 🗓️ Day 6 — Full Integration

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Fix integration bugs found on Day 5. Ensure the full pipeline runs from a single command/script (a "run everything" script the team can rely on).

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Tune confidence thresholds based on real test results from Rabiya's QA. Polish explanation text so it reads naturally, not robotically.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Visual polish pass: consistent colors, spacing, fonts, hover states, smooth transitions when the side panel opens.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Final dataset lock-in — no more data changes after today, so the rest of the team can rehearse against a stable dataset.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Full regression test of the entire flow. Try to break it deliberately (weird clicks, fast clicking, refresh mid-load) — this is when demo-day surprises get caught, not on demo day.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Finalize the presentation deck. Draft the opening hook and closing line (see Section 9).

---

### 🗓️ Day 7 — Error-Proofing & Hardening

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Add loading/empty/error UI states to every API call path. Test backend behavior with the network artificially slowed/killed (browser dev tools) to confirm graceful failure.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Add input validation edge cases to resolution/linking modules (empty names, duplicate records, missing fields) so nothing crashes on unexpected input.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Confirm the UI never shows a raw error or blank screen — every failure state has a friendly message.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Support Rabiya in stress-testing by generating a couple of intentionally malformed records to confirm the system doesn't crash on bad data.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Own the master error-proofing checklist today — go through every screen and every click path personally.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Record the backup demo video (OBS Studio or screen recorder) of a clean, full successful run, narrated exactly as it will be presented live.

---

### 🗓️ Day 8 — Rehearsal Round 1

![Meer](https://img.shields.io/badge/Meer-0f4c75?style=flat-square) Be the technical operator during rehearsal — run the app live, watch for backend issues in real time.

![Maaz](https://img.shields.io/badge/Maaz-6a0572?style=flat-square) Be ready to answer deep technical questions about USP 1 and USP 2 during mock Q&A.

![Prithvi](https://img.shields.io/badge/Prithvi-ab3428?style=flat-square) Fix any UI issues surfaced during rehearsal immediately.

![Sadiya](https://img.shields.io/badge/Sadiya-f38181?style=flat-square) Observe rehearsal as a "judge" — take notes on what's confusing or slow.

![Rabiya](https://img.shields.io/badge/Rabiya-2b9348?style=flat-square) Time the full demo. Target 3-4 minutes. Cut anything that overruns.

![Nabiya](https://img.shields.io/badge/Nabiya-f7b32b?style=flat-square) Lead the rehearsal as the primary presenter (or coordinate whoever is). Collect feedback and revise the script.

---

### 🗓️ Day 9 — Fixes & Rehearsal Round 2

**Everyone:** Fix every issue flagged on Day 8 in your own workstream. Re-run the full pipeline once fixes are in. Do a second full rehearsal, timed, in front of the whole team plus one outside person if possible — fresh eyes catch confusing moments insiders miss.

---

### 🗓️ Day 10 — Final Buffer & Polish

**Everyone:** No new features today — this is a buffer day for anything that slipped. Final rehearsal. Confirm the backup video plays correctly on the actual presentation machine. Charge laptops, confirm wifi/hotspot backup, pack any physical materials needed.

---

## 🛠️ Tool & API Key Summary Table

| Layer | Tool | API Key Needed? | Where Used | Owner |
|---|---|:---:|---|---|
| Data generation | Python `Faker` | No | Local script | Sadiya |
| Graph database | Neo4j AuraDB Free | Yes — connection URI + username/password | Env vars `NEO4J_URI`, `NEO4J_USER`, `NEO4J_PASSWORD`; used in backend driver connection | Meer |
| Alias resolution | `rapidfuzz`, `jellyfish`, `indic-transliteration` | No | Backend module | Maaz |
| NLP/NER | `spaCy` | No | Backend module | Maaz |
| Anomaly detection | `scikit-learn` | No | Backend module | Maaz |
| Backend API | FastAPI, Pydantic, uvicorn | No | Own server | Meer |
| Frontend | React (Vite), Tailwind CSS, `react-force-graph`/`vis-network`, `axios` | No | Own app | Prithvi |
| Backup recording | OBS Studio | No | Local recording | Nabiya |

**Note:** Deliberately keeping this stack free of paid third-party AI APIs (like OpenAI) is itself a talking point — your system runs on your own infrastructure with no per-request cost and no dependency on an external vendor's uptime, which matters for a government/law-enforcement deployment context.

Store all credentials in a `.env` file, **never committed to git**. Add `.env` to `.gitignore` on Day 1. Load with `python-dotenv` in the backend.

---

## 🎤 What To Say While Presenting

- **Opening hook:** *"Right now, if a criminal operates across two states, each state's police force sees only half the network. NetSentry sees the whole thing."*
- **On alias resolution:** *"Real police records don't come with clean, matching names — the same person shows up as 'Mohd. Aslam' in one FIR and 'Aslam Bhai' in another. NetSentry resolves these using phonetic and fuzzy matching combined with corroborating evidence like shared phone numbers — and when it's not confident, it flags the match for a human to confirm, rather than guessing silently."*
- **On cross-jurisdiction linking:** *"We deliberately built this using two datasets that don't share a common ID system, on purpose — because that's the real situation between Indian state police departments today. NetSentry links them anyway, using shared phone numbers, vehicles, and resolved identities."*
- **On explainability:** *"Every risk score comes with a plain-English reason. We didn't want a black box — an investigator needs to know why someone was flagged before acting on it in court."*
- **On the human-in-the-loop design:** *"NetSentry doesn't make arrests or accusations — it surfaces connections and evidence-driven leads. The investigator always makes the final call."*
- **Closing line:** *"NetSentry doesn't just process data — it reconnects a picture that was always there, just scattered across silos no single officer could see."*

**If asked "how is this different from just using a graph database":** *"A graph database is a tool. NetSentry is the resolution layer on top of it — the hard part isn't storing connections, it's figuring out which messy, inconsistent records actually refer to the same person or event across sources that were never designed to talk to each other. That's the part we built."*

---

## 🏆 Why This Version Is Better Than the "Standard" Pitch

| Standard graph-analysis pitch | NetSentry (yours) |
|---|---|
| Assumes clean, matching names across records | Explicitly resolves messy, inconsistent, aliased identities |
| Assumes one unified database | Explicitly links across incompatible, siloed department schemas |
| Gives a risk score with no reasoning | Gives a risk score *with a plain-English explanation* |
| Implicitly positions AI as decision-maker | Explicitly keeps a human-in-the-loop for medium-confidence matches and final calls |
| Depends on paid external AI APIs | Runs entirely on open-source/local tooling — no per-request cost, no external vendor dependency |

---

<p align="center">
<img src="https://img.shields.io/badge/Built_by-Team_F--ups-e94560?style=for-the-badge&labelColor=1a1a2e" />
</p>
