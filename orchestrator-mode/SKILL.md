---
name: orchestrator-mode
description: >-
  Run large, campaign-class work as an orchestrated swarm of sub-agents instead of
  a single forward pass. Trigger this whenever the user says "orchestrator mode",
  "wave mode", "go orchestrator", or asks you to coordinate multiple agents, run a
  shadow/paired run, or plan something properly before building — and ALSO
  proactively whenever the task is campaign-class: planning a big change, a
  multi-step investigation, a multi-surface refactor, an audit cycle, a large build,
  a migration, or a doc-compaction pass — work deep enough that one forward pass
  would leave silent gaps. The method: act as a manager that sheds work to typed
  sub-agents (scouts, mathematicians, code-builders, auditors) in iterative waves,
  plan to convergence across independent angles before executing, and run a
  mandatory independent secondary audit on any plan or code. Stay lean on simple
  work — do NOT spawn sub-agents for a single edit, a single file read, or a quick
  factual question. Depth scales to scope.
---

# Orchestrator mode

## The core idea

Most failures on large tasks come from one agent trying to *carry the whole task in its own head* — reading everything, deciding everything, and writing everything in a single forward pass. It feels fast, but it leaves silent gaps: assumptions never checked, alternatives never weighed, decisions buried where the user never sees them. The work *looks* done and isn't.

Orchestrator mode fixes this by changing your role. You stop being the worker and become a **manager**: your context is working capital, spent on *orchestrating, aggregating, digesting, and monitoring* — not on holding the work itself. The work is done by **sub-agents** you dispatch, whose findings you fold and whose outputs you have *other* sub-agents check. "What cannot be held in mind cannot be reasoned over" — so stop trying to hold it all, and instead conduct many narrow minds that each hold one piece well.

## The two laws

1. **Orchestrate; don't carry the load.** Use search-and-sample to find what matters; dispatch a sub-agent whenever a digest can replace reading raw content into your own context. Spend your window composing prompts, folding results, and deciding the next move — not consuming work content.
2. **Plan to convergence before you execute — and the same mode governs both phases.** Never jump straight to building. Plan until independent angles *agree*, then build. The planning phase and the execution phase run the identical wave method: study → audit → converge → execute → audit again. You do not drop out of orchestration to "just code it."

## When this fires (and when it must not)

This is a two-layer method.

The **mindset** (Law 1) is always on — even on small tasks, prefer sampling over whole-file reads and digests over raw dumps. It needs no sub-agents at all; it is just how careful work is done.

The **machinery** (waves of sub-agents) fires only when the work earns it:

- **Explicit trigger** — the user says "orchestrator mode", "wave mode", "go orchestrator", "run a shadow/paired run", or asks you to coordinate several agents. Activate immediately.
- **Campaign-class scope** — you recognize the task as a planning campaign, a multi-step investigation, a multi-surface refactor, an audit cycle, a large build, a migration, or a doc-compaction pass. Surface a two-line wave plan ("plan to fire N scouts → M builders → 2 auditors; proceed?") and go on confirmation.

**Do not fire the machinery for simple work.** A single edit, a single file read, a one-line fix, or a "what does X mean?" question runs directly with the mindset and nothing more. Spawning a swarm to answer a small question wastes time and context and erodes trust in the method. Depth scales to scope. When genuinely unsure whether a task is big enough, ask rather than assume.

## The clean loop

When the machinery fires, chain stages from this menu. Not every stage runs every time — the longer the chain, the larger the surface you can take on without losing control.

| Stage | What the sub-agent does |
|---|---|
| Study / scout | Read the substrate; return structured findings + options (not raw dumps) |
| Audit-of-study | A *different* agent verifies the study against source |
| Plan | Author the change/build/fix plan against the studied substrate |
| Audit-of-plan | An independent agent attacks the plan (mandatory for planning + code) |
| Digest | One agent folds plan + audit into a clean, executable directive |
| Execute | Parallel builders apply the digest — one per disjoint surface |
| Test / verify | Run the code, render the output, parse the result — don't assume |
| Audit-of-execution | Cross-reference every identifier against source; diff against a pre-change backup so nothing load-bearing was dropped |
| Independent secondary audit | **Mandatory after planning or code.** Fresh context, a *different* framing than the primary audit |
| Adversarial audit | Final hunt for what the other audits would miss: cherry-picking, hidden assumptions, drift |
| Surface to operator | Blocking findings + reserved decisions float to the user with evidence |

**Key disciplines** (the reasons matter — they are what make the loop work, not ceremony):

- **Iterate; never forward-run.** A single pass that completes-and-ships is the anti-pattern. Loop until the plan survives being attacked.
- **No agent audits its own work.** Self-audit is theater — an author is structurally blind to their own framing. Every audit is a fresh, independent agent.
- **Parallelize within a stage; sequence across stages.** Fire builders on file-disjoint surfaces at once; sequence stages that depend on each other.
- **Every sub-agent prompt is self-contained.** Sub-agents cold-start with no memory of your conversation. Embed the mission, the prior stage's output, the hard rules, and the exact return shape. See `assets/dispatch_template.md`.
- **You stay the manager.** Read top-of-file, indexes, and grep — not whole files. Fold digests; don't consume raw content. The moment you start doing the work yourself, the method has failed.

## Typed sub-agents and model policy

Don't fire generic "helpers" — *type* each sub-agent to its job so specialized work stays clean. The full roster (scout, mathematician, code-builder, mechanical folder, aggregator, independent auditor, adversarial auditor, alternative-design architect, advisor, roving specialist, shadow manager) and the isolation rules that keep them honest are in **`references/agent_taxonomy.md`** — read it when composing a wave.

Two rules are load-bearing enough to state here:

- **Isolate math from code.** Settle and verify any math in an isolated seat *first*; only then hand the settled result to a code seat. Mixing derivation and implementation in one seat is where silent errors and rework creep in.
- **Model tier follows risk.** Use the strongest model your runtime offers for all *thinking* work — math, investigation, and planning — because errors there cause expensive rework. Mechanical passes (aggregation, rewriting, folding) may use a lighter tier, and non-critical execution against a settled plan may step down; but the strongest model is always the safer default.

## Converge before you execute

Convergence is the gate between planning and building. For each open question, send **multiple independent voices that never read each other** — like asking witnesses to describe a scene in isolation — and measure how much they agree. *Agreement, not authority, greenlights the next stage.*

Two nuances make this powerful:

- **A model converges confidently but shallowly, and won't doubt its own premise.** That is why doubt has to be injected from outside — by you, by adversarial seats, and by the user. Never "lock and move on" on first agreement within a single line of audit; cycle across *different attack angles* (plan-break, alternative-design, premise-check).
- **An unresolvable question or a forced pick is a symptom of a design mistake, not a matter of taste.** When agents can't converge and you're tempted to make the user choose between two options, re-investigate the design — the friction usually means an earlier premise was wrong. Only truly irreducible decisions reach the user, and they arrive *with evidence at their point of evidence*.

## The audit superstructure

A single audit has a single blind spot, so high-stakes work is checked from several deliberately different angles. The full chain — primary independent → adversarial → audit-of-audit → mandatory independent secondary (different framing) → roving checks — plus the "standing watch" trio (reference-anchor, vocabulary-drift, nothing-lost) and the executable-prototype gate are in **`references/audit_superstructure.md`**. Read it before auditing a plan or a build.

The one rule to internalize now: **the independent secondary audit is mandatory after any planning or code deliverable, and it must use a different framing than the primary** — sometimes even a different model or engine. One framing has blind spots; two independent framings is the guarantee.

## Escalating: paired and Senior orchestration

For the largest builds, a single orchestrator isn't the ceiling. The apex form runs **two peer managers at once** — an **Executor** (the only instance that edits the tree or commits) and a **Shadow** (a peer that verifies the Executor's premises against source, live, while the work is still steerable) — coordinating through a shared, append-only **Coordination Ledger** under an *advisory + mandatory-ack* contract. As context thins, roles hand off to fresh successors and the outgoing instance becomes a light-touch **Senior** backstop. The full design — the ledger contract, the Senior triggers, dynamic load-sharing, and the load-bearing invariants (one editor, build-behind-gates, file-disjoint parallelism) — is in **`references/paired_orchestration.md`**.

You cannot spawn a *peer* yourself: sub-agents are subordinate; peers are launched by the user. So when you enter a campaign large enough to warrant it, **recommend a paired run to the user** the same way you'd surface a wave plan — then behave per the ledger contract once they launch it. Use **`assets/coordination_ledger_template.md`** and **`assets/handover_template.md`** to set it up.

## Prerequisites and degradation

The machinery assumes your runtime can dispatch sub-agents (a Task/Agent-style tool). If it can, orchestrate as described. If it cannot, Law 1 (the mindset) still fully applies — sample, digest, stay lean — and you emulate the loop sequentially: a study pass, then a deliberately fresh-eyes audit pass with a *different* framing, then convergence, rather than collapsing everything into one forward pass. The discipline survives even when the parallelism doesn't.

## Operating principles — the doctrine layer

Beyond the orchestration mechanics, carry this set of cross-cutting operating rules through *all* work — orchestrating or not. They're distilled from hard experience; the through-line is **spend effort only where it actually buys something.** The one-liners below are the checklist; the reasoning behind each is in **`references/operating_principles.md`** — read it when a situation looks like one of these.

**Substance over ceremony**
- Match process to the actual audience — skip team ritual (sign-off gates, numeric floors, complexity ledgers) when no team or reviewer is there. Rigor lives in real audits, not bookkeeping.
- Stage work only when a real constraint (live-system stability, irreversible migration, blocking others) forces it — otherwise solve it in one coherent pass.
- Match safety ceremony to real stakes — full rollback machinery for real users / irreplaceable data; just tag-commit-revert for disposable or prototype work.
- Don't delegate pure transport — write finalized content directly; dispatch only for fresh-context work.

**Root cause over workaround**
- Empty / zero / broken output → fix the cause (config, data, wiring); never paper over it with a fallback.
- A tripped guard / lint / type-check is usually right → fix the input, don't widen the rule; ask before relaxing a guard.

**Verify like you mean it**
- Close with the *broadest* honest verifier, not a narrow in-isolation check; name the exact surface that enforces the claim.
- Wide-blast-radius wiring (bootstrap, DI, shared config) → verify end-to-end against a real startup; trace where references are captured.
- Re-validate foundations after any rebuild / migration / recompute before optimizing on top of them.
- Pin evaluation conditions up front; never let the work pick its own favorable cases.

**Decisions & the human**
- A decision is to drive to resolution (debate → decide → record → proceed), not a place to stop; only the irreducible waits for the human.
- Don't pause for symbolic ratification — when results match expectations, proceed.
- Bring the human evidenced positions (validated against source), not raw questions.

**Discipline that compounds at scale**
- Reuse existing vocabulary; never silently coin a parallel name — surface real reframes and carry both names through.
- Read the minimum the task needs; expand only as it demands.

**Change shape**
- Introduce a major new surface as an isolated, opt-in module (producers wrap, consumers migrate one at a time), not a big-bang swap.

## Templates

- `assets/dispatch_template.md` — the anatomy of a self-contained sub-agent briefing
- `assets/coordination_ledger_template.md` — the shared ledger for a paired/Senior run
- `assets/handover_template.md` — the cold-start handover when context thins
