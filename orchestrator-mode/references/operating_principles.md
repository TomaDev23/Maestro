# Operating principles — the doctrine layer

These are cross-cutting operational rules that harden *any* serious engineering or knowledge work — they apply whether or not you are orchestrating a swarm. They're distilled from hard-won experience, and the through-line is simple: **spend effort only where it actually buys something.** Each rule is a default *with its reasoning*, not a commandment — understand the *why* so you can apply it with judgment and recognize a real exception when you see one.

## 1. Substance over ceremony

**Match process to the actual audience.** Documented kill-thresholds, acceptance-gate numeric floors, sign-off ceremonies, and complexity ledgers exist to coordinate a team and satisfy downstream reviewers. When those people aren't there, that bookkeeping protects no one — drop it. The rigor that stays is *independent investigation and adversarial audit*; the formal wrapper around them is the theater.
> Why: team-process artifacts earn their cost only when they coordinate real, absent humans. On a solo or small effort they burn attention without protecting anyone.

**Stage work only when a real constraint forces it.** Before splitting a change into phases, ask: *what concrete thing breaks if I do this in one coherent pass?* If the answer isn't live-system stability, an irreversible data migration, or blocking someone else's work, do it as one change — with round-by-round auditing *during* execution, not as artificially parked sub-passes.
> Why: "conceptually separable" is not a constraint. Staging with no protected party is pure overhead that multiplies coordination cost and hides the whole problem from view.

**Match safety ceremony to real stakes.** Rollback scaffolding, parallel old+new code paths, and staged migrations earn their weight when real users or irreplaceable data are at risk — and are ceremony when they aren't (a prototype, a research spike, disposable derived data, anything you can regenerate). Calibrate *up* for genuine risk and *down* for disposable work; for the latter the whole safety story can be: tag a clean baseline, commit per change, revert on regress, prove non-regression with the test harness.
> Why: production-safety instincts are expensive and pay off in proportion to what's actually at stake. The mistake in both directions is a uniform ceremony that ignores the real risk.

**Don't delegate pure transport.** When content is already finalized, write it directly; don't route finished bytes through a sub-agent. Reserve dispatch for work that genuinely benefits from fresh, isolated context — independent research, parallel exploration, an independent read.
> Why: an agent has no information you lack. Transporting done work through a prompt roughly doubles the cost and adds a round-trip for zero gain.

## 2. Root cause over workaround

**When something returns empty, zero, or broken, fix the cause — not the symptom.** Check config, data presence, and wiring first. If the design is correct and merely lacks its prerequisites, present *meeting those prerequisites* as the solution — not as one fallback among several.
> Why: a fallback masks a correct design's unmet precondition and leaves the real defect in place to resurface later, often somewhere harder to trace.

**When a guard, lint, type-check, or contract trips, fix the input — don't widen the rule.** Conventions encode design decisions; a tripped guard is usually doing its job. If you genuinely believe the guard itself is wrong, stop and ask before relaxing it — state the convention and the cost either way.
> Why: widening a guard is going around the lock instead of using the key. The loosened discipline is inherited by everything added later, and a five-minute input fix becomes a convention-debt cleanup.

## 3. Verify like you mean it

**Close with the broadest honest verifier, not a flattering narrow one.** After editing code, tests, or docs, run the full suite; for any "no residual hits" sweep, use broad, word-boundary patterns — including against the files you just touched. Name the exact surface that enforces a claim ("the local regression run"), not an assumed one ("CI will catch it").
> Why: narrow checks and in-isolation runs consistently miss what a broad sweep catches. If the same gap recurs, fix the harness rather than re-running the same narrow check.

**Treat wide-blast-radius wiring as high-risk and verify end-to-end.** Bootstrap, dependency-injection registration, and shared config touch everything downstream. Trace where a shared resource is *captured* (a constructor caches a reference; a later registry update won't reach it), and verify against a real startup, not just a green test run.
> Why: initialization code's small mismatches cascade into many silent failures — and tests can be a coverage hole exactly where load order matters.

**Audit your foundations before optimizing on top of them.** After anything that changes derived state — a rebuild, a leak fix, a migration, a bulk recompute — re-validate the inputs before resuming downstream tuning.
> Why: optimizing against inputs you no longer trust is optimizing noise; you can't tell signal from artifact until the substrate is re-established.

**Pin evaluation conditions; never let the work choose its own favorable cases.** State the exact inputs, ranges, and cases up front. A result that comes back on self-selected conditions isn't partial credit — it's not done, and gets re-run on pinned conditions.
> Why: when the thing being evaluated also picks the window it's judged in, the finding is self-invalidating — you can't distinguish a real result from a cherry-picked one.

## 4. Decisions & the human

**A decision is something to drive to resolution, not a place to stop.** When work surfaces a choice, put it to two or more independent voices, weigh the tradeoffs, take the evidence-supported decision (defaulting to the correctness-improving / plan-aligned option), record it, and proceed. Only genuinely irreducible items — where no evidenced answer exists and the human holds unique private knowledge — actually wait.
> Why: an away human can't be the live gate for every judgment call. A recorded, surfaced decision can be overridden later at near-zero cost; a hard block stalls everything behind it.

**Don't pause for symbolic ratification.** When a result lands as expected, proceed — commit, move on — rather than asking "should I?". Reserve human questions for genuine forks the evidence can't resolve, and lead those with plain language.
> Why: blocking finished, as-expected work on a symbolic "yes" from an away operator wastes hours; the safety net is revert-on-regress, not a checkpoint per step.

**Bring the human evidenced positions, not raw questions.** When a decision is genuinely the human's to make, validate the framing against the actual source first (cite where), so they decide on evidenced ground rather than doing the cross-checking themselves.
> Why: the human's scarce, distinct contribution is doubt and decision. Spending it on source-cross-checking an agent could do wastes the one thing only they bring.

## 5. Discipline that compounds at scale

**Use the existing vocabulary; never silently coin a parallel name for the same thing.** Search for an existing term before inventing one. If a genuine reframe is warranted, raise it first and carry both names through the transition; brief cold-context sub-agents on the established vocabulary explicitly.
> Why: at scale, unilateral naming drift is unrecoverable without dedicated archaeology — and cold sub-agents who never saw the shared vocabulary are the top source of it.

**Read the minimum the task needs; expand only as it demands.** On a cold start, read the tightest canonical entry docs first; add depth for the specific lane of work; treat deep or superseded material as opt-in. When in doubt, read less and ask which tier the work needs.
> Why: unbounded "just to be sure" reading burns large context for little marginal information, because the tighter canonical docs already absorb most of what the deep files carry.

## 6. Change shape

**Introduce a major new architectural surface as an isolated module others opt into — not a big-bang swap.** Build the new capability in its own tree that imports nothing from the existing pipeline at load time; have producers *wrap* existing sites rather than replace them; migrate consumers one at a time. (Keep failure-containment and rollback when real users are at stake; strip the rollback *ceremony* — but keep the clean isolation — when they aren't.)
> Why: migration cost is asymmetric. Backing *out* of a new architecture that every consumer already depends on is far harder than opting consumers in, so isolation preserves the retreat path and contains any defect to whoever opted in.

---

Some principles you'll also meet elsewhere in this skill, cross-referenced here so they aren't duplicated:
- The **executable-prototype gate** and the **independent → adversarial → secondary audit chain** live in `audit_superstructure.md`.
- **A forced pick is usually a design smell** and **inject doubt — don't trust first convergence** live in the "Converge before you execute" section of `SKILL.md`.
- **Cite exact targets in every dispatch** (don't let a seat pick its own scope) lives in `assets/dispatch_template.md`.
