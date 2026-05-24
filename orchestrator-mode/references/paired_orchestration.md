# Paired & Senior orchestration (the apex form)

For the largest builds — big planning runs and especially code build/edit campaigns — a single orchestrator isn't the ceiling. The strongest form runs **two peer managers at once**, coordinated through one shared ledger, and grows into a three-agent family as context thins.

## The two peers

- **Executor** — runs the build and is the **only** instance that edits the tree or commits. One editor keeps the work clobber-safe and the commit trail clean.
- **Shadow** — not a sub-agent but a *peer*: its own thread, its own waves. It reads the source fresh and challenges whether the Executor's *premises* are actually true, **while the work is still steerable** — and, by default, touches nothing but the ledger. The Shadow can be a different model or engine, for a genuinely independent framing.

The Shadow's value is the live, independent second framing: it course-corrects before mistakes compound, instead of reporting late. On code work it functions as a second team member auditing the management, the changes, and the math/code as they land.

## The Coordination Ledger

Both peers share one **append-only, author-tagged** document and write into it as they orchestrate. This is the artifact that turns a passive shadow into a steering peer. Mark types:

`OBSERVATION` (no ack needed) · `STEER` (advisory, must respond) · `BLOCKING` (halts that unit) · `ACK` (acted on it) · `DEFER` (parked with reason) · `ESCALATE` (to the operator)

**Steering contract — advisory + mandatory-ack.** A mark is advisory, but **no peer may silently ignore one.** Every mark must be met with an ACK-and-act, a DEFER-with-reason, or an ESCALATE. Unresolved BLOCKING marks escalate straight to the operator. Coordination flows both ways — it is cooperation, not surveillance. See `assets/coordination_ledger_template.md`.

## The Senior backstop (the 3-agent family)

A manager's context window is finite. When it runs low, it hands its *active* load to a fresh same-role successor — cold-started from a handover doc plus the ledger — and the outgoing instance becomes the **Senior**: a light-touch backstop that carries the full history at near-zero ongoing cost. The Senior defers to the active pair and steps in only on a trigger:

- an escalation,
- a peer disagreement,
- an active agent gone quiet,
- an unaudited commit,

on a periodic (~20-minute) cadence. Roles persist across instances, so the run becomes a three-agent family: Executor + active Shadow + Senior. Use `assets/handover_template.md` for the cold-start. This buys continuity and a senior voice at near-zero context cost — the role outlives the instance.

## Dynamic load-sharing (still maturing)

The Shadow need not *only* audit. The collision-safe default splits work by **phase**: the Shadow owns *scope · settle · verify* (next-chapter file-disjointness maps, math-seam settling, spec drafting, deep verification, decision-package prep); the Executor owns *build · commit*. If the Shadow also *edits* the tree (true co-build), that relaxes the one-editor rule and is allowed only with **all four** guards: a declared disjoint file-partition, a single committer, operator confirmation, and an independent verifier of anything the Shadow authored.

## Load-bearing invariants (why it stays safe)

- **One editor / non-collision.** Exactly one instance edits the tree and commits — clobber-safety plus a clean, linear commit trail; you always know which voice authored what.
- **The independent second framing is the value.** It catches what one framing, or the author, cannot — e.g. a cross-file mismatch that a per-file read passes but a holistic secondary audit, corroborated by the shadow, catches.
- **Build behind gates.** Work is built uncommitted and reversible, gated on a secondary audit plus the operator's sign-off — so a missed bug never ships, even when the first read called it "sound."
- **File-disjoint parallelism in one tree.** Partition parallel work units by file in the one main tree and commit each independently, so held or gated work stays reversible. (No invented isolation; no worktrees.)
- **Operator-reserved decisions.** Choices that belong to the user surface with evidence at their point of evidence. Agents prepare and *float* them; they never self-sign the user's decision-gates.

## Activation

You cannot spawn a peer yourself — sub-agents are subordinate; peers are launched by the user. When you enter a campaign large enough to warrant a paired run, **recommend it to the user** ("this surface is large enough to warrant a Shadow + Coordination Ledger — want me to set one up?"), then behave per the ledger contract once they launch the second instance. Both peers still run their own full wave machinery internally; paired orchestration sits *on top of* the loop, it does not replace it. Two instances each running orchestrator mode, coordinated through one ledger, is strictly stronger than one.
