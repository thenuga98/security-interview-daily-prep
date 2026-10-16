# Security Interview Daily Prep

A Claude skill that runs a structured, mock-interview-style daily prep session for a security engineering role. Claude plays the interviewer — asking, probing, and correcting — while the candidate drives every answer.

## Recent changes

- **Two modes per drill round.** The security-fundamentals drill now offers rapid-fire (10 questions, broad coverage) or deep-dive (5 topics, each with 2-3 follow-ups probing the mechanics further). The Python-basics drill now offers rapid-fire (10 conceptual Q&A) or hands-on (5 small code challenges — fill-in-the-blank or "implement this" — instead of pure recall). Claude asks which mode you want at the start of every drill round, every time.
- **Study sessions.** After the 4 main rounds, Claude offers an optional study session on a topic you struggled with that day, or any topic of your choosing (security topics only, for now). Unlike the rest of the session, this isn't Socratic or interview-framed — the candidate drives entirely, asking as many questions as they want, with Claude supporting via recaps, explanations, and hands-on practice (code review, quizzes, etc.). Claude is required to stick to factually correct answers and cite sources during these sessions. Study sessions are never logged to the vault or memory.
- **No more company-specific tailoring.** The skill previously leaned on an active-interview-process context (loop structure, JD emphasis) stored in memory to steer scenario/problem choices. That's been removed — the skill now runs general security engineering prep by default, and would only re-tailor itself if that context is reintroduced later.

## What it does

Each session runs four rounds, in a standing default order:

1. **Threat modeling** — a brand-new system/scenario, worked Socratically: Claude answers clarifying questions about the architecture, the candidate proposes trust boundaries and a STRIDE pass, Claude validates and pushes back where reasoning is off.
2. **Coding question** — one algorithm/DSA or security-flavored coding problem (scanner, parser, validator, crypto-misuse detector, etc.). Stops at a validated approach + pseudocode, not a full implementation.
3. **Security-fundamentals drill** — 10 rapid-fire conceptual Q&A questions, mixing repeats (for spaced repetition) with new material.
4. **Python-basics drill** — 10 rapid-fire questions on core Python constructs.

## Ground rules

- Every threat-modeling scenario and coding problem is brand new — never reused verbatim across sessions.
- No incorrect information — technical claims are verified, not guessed.
- The candidate drives: Claude never hands over the trust boundaries, the threats, the mitigations, or the algorithm — it asks the next good question instead.
- Drills intentionally repeat old questions in conversation (that's the point), but logged question banks only ever gain new entries, never duplicates.

## Logging (optional vault, required memory)

- If an Obsidian vault is connected, sessions are logged there: a new file per threat-modeling scenario, and cumulative append-only files for coding questions, the security drill bank, and the Python drill bank.
- The vault is optional — if it isn't connected, the session still runs in full; only the vault write is skipped.
- A running problem log is kept in Claude's memory regardless of vault availability, so repeats are never accidental.

## Usage

Install this skill in Claude (Cowork or Claude Code) and invoke it to start a session — e.g. "let's do today's security interview prep." See `SKILL.md` for the full instructions Claude follows.
