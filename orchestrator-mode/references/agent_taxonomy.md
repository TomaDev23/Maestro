# Agent-type taxonomy & model policy

Type every sub-agent to its job. A swarm is only as good as its role discipline: each sub-agent gets a narrow job, an **isolation rule** that stops it contaminating other roles, and a model tier. The isolation rules are the load-bearing part — they are what make the audits independent and the math trustworthy.

> Throughout, a "seat" means one typed sub-agent instance doing one job.

## The roster

| Role | What it does | Isolation rule | Model tier |
|---|---|---|---|
| **Scout / explorer** | Reads substrate (code, docs, data); returns structured findings, not opinions | Returns a digest, never a raw dump | Top |
| **Worker** | Produces a concrete deliverable: a plan, a design, a report | — | Top |
| **Mathematician** | Derives and verifies formulas; runs throwaway prototypes to test them | Math never shares a seat with code — settle the math first, in isolation | Top |
| **Code-builder** | Turns a settled plan into code | Receives the settled math/plan as input; does not re-derive it in the same seat | Top (non-critical execution may step down) |
| **Mechanical folder** | Aggregation, rewriting, doc-folding, mechanical edits | Lowest-judgement work | Lighter tier OK |
| **Aggregator** | Folds many outputs into one surface | Folds but never *decides* — preserves dissent rather than collapsing it | Lighter tier OK |
| **Independent auditor** | Verifies a deliverable it did NOT write, against source | An author can never audit their own work | Top |
| **Adversarial auditor / plan-breaker** | Attacks the converged plan from a new angle | A different framing than the primary audit | Top |
| **Alternative-design architect** | Proposes a rival design as a sanity check | Reads only the final plan, not the history | Top |
| **Advisor** | Axis-sliced review — one concern at a time | — | Top |
| **Audit-of-audit** | Verifies the audit itself was complete and well-scoped | — | Top |
| **Independent secondary / cross-model voice** | Fresh auditor with a *different* framing; sometimes a different model or engine entirely | Mandatory after planning or code | Top / other engine |
| **Roving specialist** | Time-travel (re-walk history), plan-break, rules/memory inspection | Fired *alongside* the waves whenever a check is wanted — not a terminal stage | Top |
| **Shadow manager** | A peer manager auditing the main run live (see `paired_orchestration.md`) | Its own thread & waves; verifies premises against source | Top |

"Top" means the strongest model your runtime offers (for Claude, that's the Opus tier). The taxonomy is model-agnostic; what matters is that thinking work gets the best model available.

## Two isolation rules that carry the most weight

- **Math/code isolation.** Derive and verify math in an isolated mathematician seat, settle it, *then* hand the settled result to a code seat. Combining derivation and implementation in one seat is where go-arounds and silent errors creep in. The math seat owns "is this correct?"; the code seat owns "is this wired correctly?" — never both at once.
- **The roving specialist runs alongside the waves.** Time-travel, plan-break, and rules/memory checks don't have to wait for a terminal audit wave. Fire a roving specialist at any point to keep adversarial pressure continuous and off your own context.

## Model policy

Default to the **strongest model for all thinking work**, and prefer it everywhere; reach for a lighter tier only as a deliberate, non-critical exception.

| Work type | Model |
|---|---|
| Math | Strongest (always) |
| Investigation | Strongest (always) |
| Planning | Strongest (always) — planning errors cause rework; never economize here |
| Mechanical / aggregation / rewriting | May use a lighter tier; prefer strongest |
| Execution against a settled plan | May step down if non-critical; prefer strongest |

Rule of thumb: plan and reason with the strongest model; only mechanical or non-critical execution may step down — and even then the strongest model is the safer default.
