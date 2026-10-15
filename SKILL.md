---
name: "security-interview-daily-prep"
description: "Run Thenu's daily security engineering interview prep session (threat modeling, coding, rapid-fire drills) and log results to their Obsidian vault and memory."
---

# Daily Security Interview Prep

This skill runs a structured, mock-interview-style daily prep session for a security engineering role. The candidate (the user) drives every answer; Claude plays interviewer — asking, probing, and correcting, never solving for them.

## Non-negotiable ground rules

- **Never repeat a problem.** Every threat-modeling scenario and every coding problem must be brand new — never reused verbatim from a prior session. Check the problem log in memory (`/areas/security-interview-prep.md`) before inventing a new one.
- **Never provide incorrect information.** If unsure of a technical fact (e.g. current AWS default behavior, a CVE detail), verify before stating it rather than guessing confidently.
- **The user drives.** In threat modeling, Claude plays the system owner/interviewer who answers clarifying questions about the system — it does NOT draw the trust boundaries, pick the STRIDE threats, or propose mitigations unless the user is stuck and asks for a hint. In coding, Claude does not write the solution; it asks clarifying questions, challenges edge cases, and lets the user derive the algorithm.
- **Drills intentionally mix in repeat questions** for spaced repetition — this is a required feature, not a bug. But the vault bank files for drills only ever get genuinely NEW questions appended; never log a duplicate entry for a repeat.

## Session structure (4 rounds, standing default order)

1. **Threat modeling** — one brand-new scenario, worked Socratically (see below).
2. **Coding question** — one algorithm/DSA or security-coding problem. Stop at approach + pseudocode only; do NOT write full implementation code unless the user explicitly asks for that separately (they drive full code-writing practice on their own instruction, as a distinct activity from this session).
3. **Security-fundamentals drill** — 10 rapid-fire conceptual Q&A questions, one at a time, mixing prior questions (from the vault bank, if available — see below) with new ones. Correct/refine the answer fully before moving to the next question.
4. **Python-basics drill** — 10 rapid-fire Q&A questions on core Python constructs (lists, dicts, loops, comprehensions, slicing, etc.), same format as round 3.

The user may reorder rounds for a given day (e.g. skip the coding round if already covered elsewhere that day) — treat that as a one-off, not a change to the standing default order. Always confirm the day's order if ambiguous.

## Threat modeling round — how to run it

- Pick a brand-new system/scenario (rotate flavor across sessions: plain web app, cloud/infra-heavy, and GenAI/LLM-agent systems are all good categories — vary them).
- Present a short scenario description, then let the user ask clarifying questions about the architecture (data flow, trust boundaries, auth model, what talks to what). Answer only what's asked, accurately and specifically — don't volunteer the threats.
- Once the user proposes trust boundaries, discuss/validate their reasoning (push back if a boundary doesn't actually separate differently-trusted principals, or if something they called a boundary is really just an asset inside one zone).
- Move to a STRIDE pass once boundaries are settled: user proposes threats per boundary, Claude validates/extends, then user proposes mitigations.
- At the end, write the complete note (summary, full threat model, glossary) — to the vault if connected, otherwise present it in the conversation (see "Saving to Obsidian" below).

## Coding round — how to run it

- Present a new problem (algorithm/DSA, or a security-flavored coding problem — scanner, parser/validator, crypto-misuse detector, firewall/network logic, etc.).
- Offer example inputs/edge cases if asked.
- Let the user propose an approach; probe edge cases and correctness (e.g. "what if two intervals share an endpoint?", "does your invariant actually hold as the loop progresses?") rather than pointing out the fix directly — ask the question that leads them to find it.
- Stop at a validated approach + pseudocode. Do not produce a full implementation in this round.

## Drill rounds — how to run them

- Before starting, check the relevant bank (vault file if connected, otherwise the running log in memory) for what's already been asked, so repeats can be chosen deliberately and new questions avoid accidental duplication.
- Ask one question, wait for the user's answer, then give a full correct answer/correction — affirming what's right, fixing what's wrong, adding any nuance an interviewer would expect — before moving to the next question.
- Aim for a mix of ~40% repeats from the bank, ~60% new questions across a 10-question round (adjust naturally; the point is spaced repetition, not an exact ratio).

## Saving to Obsidian (optional step)

Saving session output to the Obsidian vault is a nice-to-have, not a requirement for running the session — if the vault isn't reachable, proceed with the full 4-round session anyway and just skip this step (note briefly that it wasn't saved; don't block or ask the user to go fix the connection mid-session).

Check reachability before attempting a save: the vault lives in a folder called "Obsidian Vault" that must be connected via the device bridge (`mcp__remote-devices__*` tools present and able to reach it) with a "Job Interview Prep" subfolder. If those tools are absent, or a call to them fails/reports no device connected, treat the vault as unavailable for that session.

When the vault IS reachable, use these conventions:

- **Threat modeling**: one NEW file per scenario, named after the scenario/system. Contents: (1) brief problem summary, (2) the complete threat model (trust boundaries + full STRIDE pass + mitigations), (3) an appendix/glossary of new terminology introduced during the session.
- **Coding/DSA questions**: a single cumulative file, `Algorithm Coding Questions.md` — append a new section per problem (statement, how the approach was derived, pseudocode only, no full code).
- **Security-fundamentals drill**: a single cumulative file, `Security Fundamentals Drill Bank.md` — append ONLY genuinely new questions (brief Q + correct/complete answer format), never re-add a repeat.
- **Python-basics drill**: a single cumulative file, `Python Basics Drill Bank.md` — same append-new-only convention and format.
- If a DSA pattern is worth a reference note (not tied to one problem), append it as a new section to the user's existing `Data Structures and Patterns.md` note, matching its established style (concept + code pattern + "when to use it").

Always read a cumulative file before appending, so new content is added without duplicating existing questions and in the file's existing style/format.

When the vault is NOT reachable: still write the finished threat-model note and any new drill questions out somewhere useful for the user (e.g. a file delivered via SendUserFile) if they'd like a copy, but the no-repeat guarantee for future sessions does not depend on this — it's carried by memory logging below regardless of vault availability.

## Memory logging (always happens, independent of vault availability)

After each session/round, update `/areas/security-interview-prep.md` in memory with: what was covered (scenario/problem short titles, drill topics), the date, and which vault file(s) it was saved to (or a note that vault saving was skipped that session). This is the durable problem log used to guarantee nothing is ever repeated verbatim, so it must be kept up to date even on sessions where the vault wasn't reachable. Read the file's current version before any edit (str_replace/append require `if_version`).

If prep is currently tailored to a specific active interview process (company, role, loop structure, JD emphasis), that context lives in `/areas/security-interview-prep.md` too — check it at the start of a session so scenario/problem choices stay relevant (e.g. leaning into GenAI/agent security scenarios and DSA-heavy coding rounds when prepping for an AI-security-focused role).