# The audit superstructure

A single audit has a single blind spot. High-stakes work is checked from several deliberately different angles, and a small standing watch rides along every wave.

## The layered audit chain

- **Primary independent audit** — framing A; verifies the deliverable against source. The author never audits their own work.
- **Adversarial audit** — framing B; hunts what the primary would *not* catch: cherry-picking, hidden assumptions, framing drift.
- **Audit-of-audit** — confirms the audit itself was complete and well-scoped (catches a mis-scoped or shallow audit).
- **Independent secondary** — **mandatory after planning or code.** Fresh context, a *different* framing than the primary — sometimes a different model or engine entirely. One framing has blind spots; two independent framings is the guarantee.
- **Roving checks** — time-travel, plan-break, and rules/memory probes, fired *alongside* the waves rather than as a terminal stage.

The author-can't-audit-own-work rule is why these are *separate, fresh-context* agents. An author is structurally blind to their own framing; independence is the precondition for catching real defects. Giving the secondary a different framing than the primary is what makes the two blind spots non-overlapping.

## The standing watch — re-run every wave

Three auditors are re-invoked on every wave, doing nothing but protecting the truth from erosion. Their folds are **additive** — they add without dropping:

- **Reference-anchor** — checks each wave's output against the frozen set of locked premises, so a later wave can't quietly contradict an earlier decision.
- **Vocabulary-drift** — catches a new name invented for an existing concept before it splits the work into two incompatible vocabularies.
- **Nothing-lost** — diffs against the previous version so no load-bearing item is silently dropped during a fold or rewrite.

## The executable-prototype gate

Before any real change, build a **throwaway prototype** against a synthetic case. Its job is not to work — its job is to *force hidden specification ambiguities to surface mechanically*. Every "wait, which behavior did we mean here?" the prototype exposes is value extracted. **Finding zero ambiguities is itself a red flag** — it usually means the prototype wasn't probing hard enough, not that the spec was perfect. A narrative walkthrough is not a substitute; only execution forces what reading conceals.

## The seven-round sliced audit (for the highest stakes)

For the highest-stakes deliverables, a single audit becomes a seven-round pattern:

1. **Worker** produces the deliverable.
2. **Layer-sliced auditors** each verify one horizontal layer.
3. **Axis-sliced advisors** each review one vertical concern.
4. **Aggregation** folds them — and *never collapses dissent* into false agreement.
5. **Audit-the-audit** checks the aggregation was complete.
6. **Additive fold** merges accepted findings without dropping anything.
7. **Delivery-verify** confirms the final artifact matches the contract.

## When are you allowed to build?

A plan is not build-ready because it is *written* — it is build-ready because it has **survived independent attempts to break it.** Build only after the converged plan has cleared: an independent audit, an adversarial attack, a differently-framed mandatory secondary, roving checks, and a nothing-lost pass — ideally prototype-backed. The cost of the gauntlet is paid once, up front; the cost of a silent gap is paid forever, downstream.
