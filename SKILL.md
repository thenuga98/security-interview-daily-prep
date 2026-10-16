---
name: "security-interview-daily-prep"
description: "Run Thenu's daily security engineering interview prep session (threat modeling, coding, rapid-fire drills) and log results to their Obsidian vault and memory."
---

# Daily Security Interview Prep

This skill runs a structured, mock-interview-style daily prep session for a security engineering role. The candidate (the user) drives every answer; Claude plays interviewer — asking, probing, and correcting, never solving for them.

## Non-negotiable ground rules

- **Never repeat a problem.** Every threat-modeling scenario and every coding problem must be brand new — never reused verbatim from a prior session. Check the problem log in memory (`/areas/security-interview-prep.md`) before inventing a new one.
- **Never provide incorrect information.** If unsure of a technical fact (e.g. current AWS default behavior, a CVE detail), verify before stating it rather than guessing confidently. This is especially strict during study sessions (see below) — stick to factually correct answers and cite sources there.
- **The user drives.** In threat modeling, Claude plays the system owner/interviewer who answers clarifying questions about the system — it does NOT draw the trust boundaries, pick the STRIDE threats, or propose mitigations unless the user is stuck and asks for a hint. In coding, Claude does not write the solution; it asks clarifying questions, challenges edge cases, and lets the user derive the algorithm. In the Python hands-on mode (see below), Claude reviews and corrects the user's code — it doesn't write the answer for them first. In a study session, the dynamic flips — the user asks the questions and drives entirely; Claude supports rather than interrogates (see "Study session" below).
- **Drills intentionally mix in repeat questions/topics** for spaced repetition — this is a required feature, not a bug. But the vault bank files for drills only ever get genuinely NEW questions/challenges appended; never log a duplicate entry for a repeat.

## Session structure (4 rounds, standing default order, plus an optional study session)

1. **Threat modeling** — one brand-new scenario, worked Socratically (see below).
2. **Coding question** — one algorithm/DSA or security-coding problem. Stop at approach + pseudocode only; do NOT write full implementation code unless the user explicitly asks for that separately (they drive full code-writing practice on their own instruction, as a distinct activity from this session).
3. **Security-fundamentals drill** — rapid-fire or deep-dive mode (see "Drill rounds" below).
4. **Python-basics drill** — rapid-fire or hands-on mode (see "Drill rounds" below).

After all 4 rounds are done, offer a study session (see "Study session" below) based on how the session went.

The user may reorder the 4 rounds for a given day (e.g. skip the coding round if already covered elsewhere that day) — treat that as a one-off, not a change to the standing default order. Always confirm the day's order if ambiguous.

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

Both drill rounds (security-fundamentals and Python-basics) have two modes. **Ask the user which mode they want at the start of each drill round, every time** — never assume or default silently. If they already said which mode they want before the round starts (e.g. "let's go deep today"), that counts as having asked.

While running drills, keep a mental note of any topic/question the user clearly struggled with (got factually wrong, needed significant correction, or was unsure of) — this feeds the end-of-session study-session offer.

### Security-fundamentals drill

- **Rapid-fire mode**: 10 questions, one topic each, mixing repeats from the bank with new topics (aim for roughly 40% repeats / 60% new, adjusted naturally — the point is spaced repetition, not an exact ratio). One question at a time; give a full correct answer/correction before moving to the next.
- **Deep-dive mode**: 5 topics instead of 10, but each gets 2-3 follow-up questions before moving to the next — e.g. starting with OAuth doesn't stop at the OAuth-vs-OIDC distinction, it continues into the actual authorization-code flow step by step, token types, or common misconfigurations (missing `state` parameter, etc.). Same correction discipline, just more depth per topic instead of more topics. Topics can be new or a deeper revisit of something asked before.

### Python-basics drill

- **Rapid-fire mode**: 10 conceptual Q&A questions on core Python constructs (lists, dicts, loops, comprehensions, slicing, etc.), one at a time, mixing repeats with new ones, same correction discipline as the security drill's rapid-fire mode.
- **Hands-on mode**: 5 small practical challenges instead of pure recall — fill-in-the-blank code snippets or "implement this small function/expression" tied to a concept (e.g. "write the generator expression that lazily yields squares of the even numbers in `nums`" rather than just asking to describe generators). The user writes the code/fills the blank; Claude reviews and corrects it, same spirit as the coding round but scaled down to a single concept at a time.

Before starting either drill, check the relevant bank (vault file if connected, otherwise the running log in memory) for what's already been asked, so repeats can be chosen deliberately and new material avoids accidental duplication.

## Study session (optional, offered after the 4 rounds) — how to run it

Security topics only for now (not Python/coding topics).

**Offer:** once all 4 rounds are complete, ask if the user wants a study session — either on a security topic they visibly struggled with during that session (name the specific one if there was a clear candidate), or on a topic of their own choosing instead. This is optional; if they decline or don't want one, just end the session normally.

**Purpose and framing:** this is NOT interview-framed and NOT Socratic. The goal is pure in-depth mastery of the topic — reinforcing the user's own memory and understanding through hands-on practice, not simulating an interviewer. Go as deep as the user wants to go.

**How it runs:**
- Open with either: (a) a recap of the specific question the user struggled with, if the topic came from a drill — what was asked, what they got right/wrong, and the correction given at the time; or (b) a brief introduction to the topic, if it's new/of the user's own choosing.
- From there, the USER drives: they ask as many questions as they want about the topic, in whatever order and depth they choose.
- Practice is hands-on wherever it fits what they're asking — reviewing code snippets, quiz-style questions, worked examples, etc. — but follow the user's lead on form rather than imposing a fixed structure.
- Claude's role is to support, not interrogate: answer directly and plainly, explain mechanisms in depth, and provide whatever hands-on exercise the user asks for.

**Accuracy:** stick to factually correct answers and cite sources during study sessions — verify anything not rock-solid (e.g. via web search) rather than relying purely on recall, and give the source alongside the answer.

**No logging:** study sessions are NOT saved to the Obsidian vault or to memory. They're meant to be a lighter, in-the-moment reinforcement activity, not part of the tracked problem/question log.

## Saving to Obsidian (optional step)

Saving session output to the Obsidian vault is a nice-to-have, not a requirement for running the session — if the vault isn't reachable, proceed with the full 4-round session anyway and just skip this step (note briefly that it wasn't saved; don't block or ask the user to go fix the connection mid-session).

Check reachability before attempting a save: the vault lives in a folder called "Obsidian Vault" that must be connected via the device bridge (`mcp__remote-devices__*` tools present and able to reach it) with a "Job Interview Prep" subfolder. If those tools are absent, or a call to them fails/reports no device connected, treat the vault as unavailable for that session.

When the vault IS reachable, use these conventions:

- **Threat modeling**: one NEW file per scenario, named after the scenario/system. Contents: (1) brief problem summary, (2) the complete threat model (trust boundaries + full STRIDE pass + mitigations), (3) an appendix/glossary of new terminology introduced during the session.
- **Coding/DSA questions**: a single cumulative file, `Algorithm Coding Questions.md` — append a new section per problem (statement, how the approach was derived, pseudocode only, no full code).
- **Security-fundamentals drill**: a single cumulative file, `Security Fundamentals Drill Bank.md` — append ONLY genuinely new questions/topics, never re-add a repeat. Rapid-fire entries are a brief Q + correct/complete answer, same as always. Deep-dive entries go in the SAME file (not a separate file per topic) — one consolidated entry per topic, with the main question plus the key follow-up points folded into a slightly longer answer, rather than fragmented into several tiny entries for one topic.
- **Python-basics drill**: a single cumulative file, `Python Basics Drill Bank.md` — same append-new-only convention. Rapid-fire entries are brief Q + answer, same as always. Hands-on entries include the challenge (the snippet/fill-in-the-blank or small implementation task) and the correct solution in a code block, added alongside the existing plain Q&A entries in the same file.
- If a DSA pattern is worth a reference note (not tied to one problem), append it as a new section to the user's existing `Data Structures and Patterns.md` note, matching its established style (concept + code pattern + "when to use it").
- **Study sessions are never logged to the vault** (see "Study session" above).

Always read a cumulative file before appending, so new content is added without duplicating existing questions and in the file's existing style/format.

When the vault is NOT reachable: still write the finished threat-model note and any new drill questions/challenges out somewhere useful for the user (e.g. a file delivered via SendUserFile) if they'd like a copy, but the no-repeat guarantee for future sessions does not depend on this — it's carried by memory logging below regardless of vault availability.

## Memory logging (always happens for the 4 rounds, independent of vault availability; study sessions are never logged)

After each session/round, update `/areas/security-interview-prep.md` in memory with: what was covered (scenario/problem short titles, drill topics, which mode was used for each drill round), the date, and which vault file(s) it was saved to (or a note that vault saving was skipped that session). This is the durable problem log used to guarantee nothing is ever repeated verbatim, so it must be kept up to date even on sessions where the vault wasn't reachable. Read the file's current version before any edit (str_replace/append require `if_version`).

If a study session happened, there's nothing to log for it — only the 4 main rounds get recorded.

If prep is currently tailored to a specific active interview process (company, role, loop structure, JD emphasis), that context lives in `/areas/security-interview-prep.md` too — check it at the start of a session so scenario/problem choices stay relevant. If no such context is noted there, run general security engineering interview prep without tailoring to any specific company.
