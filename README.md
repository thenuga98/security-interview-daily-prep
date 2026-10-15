# Security Interview Daily Prep

A Claude skill that runs a structured, mock-interview-style daily prep session for a security engineering role. Claude plays the interviewer — asking, probing, and correcting — while the candidate drives every answer.

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
