# Coordination Ledger — template

A shared, **append-only, author-tagged** log that two peer managers (and a Senior) write into as they orchestrate. Never delete a mark; resolution is a *new* entry referencing the original. The ledger is the audit trail of the paired run.

## Header

```
RUN: <campaign name>
PEERS: [EXEC] <executor id/model>  ·  [SHADOW] <shadow id/model>  ·  [SENIOR] <senior id, if active>
CONTRACT: advisory + mandatory-ack. No peer silently ignores a mark.
          Every mark -> ACK-and-act | DEFER-with-reason | ESCALATE.
          Unresolved BLOCKING -> operator.
```

## Mark format

```
#<id>  <TYPE>  [<AUTHOR>]  <ISO-time>
<body — one clear claim or instruction; reference prior #ids when resolving one>
```

Types: `OBSERVATION` · `STEER` · `BLOCKING` · `ACK` · `DEFER` · `ESCALATE`

## Example exchange

```
#L-014  OBSERVATION  [SHADOW]  2026-05-24T10:02
Re-walked the spec from source. The normalization divisor in §4 is described two
different ways across the plan and the design doc — flagging before it hardens.

#L-015  STEER  [SHADOW]  2026-05-24T10:09
TIME-CRITICAL. The dispatch pins a fixed divisor, but the architecture says it should be
measured empirically per stratum. A fixed value silently re-creates the exact flaw this
work exists to remove. Don't lock the fixed divisor.

#L-016  ACK  [EXEC]  2026-05-24T10:14
Converges with my own seat's independent verdict — triangulated across two voices.
RESOLUTION ADOPTED: empirical per-stratum scale. The fixed divisor is dead.

#L-021  DEFER  [EXEC]  2026-05-24T10:31
Logging-format nit acknowledged but parked — out of scope for this unit; filed for the
cleanup pass with a tracking note so it isn't lost.

#L-027  BLOCKING  [SHADOW]  2026-05-24T10:58
Two source modules disagree on the contract this unit depends on. Cannot verify either
reading is safe. Halting this unit — needs an operator call on which contract is canonical.

#L-033  STEER  [SENIOR]  2026-05-24T11:40
Periodic sweep. Commit at #L-031 landed with no audit mark, and [SHADOW] has been quiet
two cycles. HOLD further commits until [SHADOW] confirms it verified #L-031, or operator clears it.
```
