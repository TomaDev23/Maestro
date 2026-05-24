# Sub-agent dispatch template

A sub-agent cold-starts with **no memory of your conversation** — its prompt must stand alone. Copy this template, fill every slot, and delete the bracketed guidance. A vague dispatch produces vague work; the few minutes spent here is the cheapest quality you will buy.

---

```
## §0 MISSION FRAMING  [why this seat exists]
You are a <ROLE: scout / mathematician / code-builder / independent auditor / ...> seat
in a larger orchestrated effort. The overall goal is <ONE SENTENCE>. Your specific job is
<NARROW TASK>, and "done" looks like <CONCRETE DEFINITION OF DONE>.

## §1 THE TASK INVARIANT  [echo verbatim — must not drift across the wave]
<The single, exact thing every seat in this wave is held to. Copy it verbatim into every
sibling dispatch so a parallel wave stays coherent.>

## §2 INPUTS  [the prior stage's output + exact targets]
- Substrate / files to read: <EXACT PATHS — not "find the relevant files">
- Prior stage output: <PASTE the digest the seat needs, or the exact path to it>
- Locked premises / constraints: <...>

## §3 HARD RULES
- Stay in your lane: <what this seat must NOT do or touch>
- Files NOT to edit: <...>
- <role-specific rules, e.g. "do not re-derive the math; it is settled in §2">

## §4 RETURN SHAPE  [exactly what to hand back]
Return <a structured digest / a table / a verdict of PASS|REVISE|FAIL + finding buckets>,
capped at <N words>. Do NOT dump raw file contents.
<If chair-facing: close with a 2-3 sentence plain-English summary.>
```

---

## Why each part matters

- **Mission framing** orients a context-less agent so it makes judgment calls in the right direction instead of following a narrow instruction off a cliff.
- **The task invariant, echoed verbatim,** is what keeps a parallel wave coherent — every seat is measured against the same yardstick, so their outputs fold cleanly.
- **Exact inputs** stop the agent from guessing which files matter. Guessing is where scope drift and wasted context come from; hand over the paths.
- **The return shape** keeps *your* context lean — you want a digest you can fold, not raw content you have to re-read. State the cap and the format.
- **Hard rules** (especially "files NOT to edit") are what make parallel builders collision-safe and keep a math seat from quietly re-deciding settled code.
