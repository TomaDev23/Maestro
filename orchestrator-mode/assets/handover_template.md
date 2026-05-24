# Handover — template (context-thinning succession)

When a manager's context runs low, it hands its *active* load to a fresh same-role successor and becomes the **Senior** backstop. The successor cold-starts from this doc plus the Coordination Ledger. Keep it tight — it is read once, fast.

```
## 1. IDENTITY & ROLE
- Role being handed over: <Executor | Shadow>
- Outgoing instance -> becomes: Senior backstop (light-touch)
- Coordination Ledger path: <...>

## 2. MISSION IN ONE PARAGRAPH
<What the campaign is building and why; the current phase.>

## 3. LIVE STATE
- Done: <committed / settled items, with ledger #ids>
- In flight: <what is mid-build right now, and which seat owns it>
- Next: <the immediate next action>

## 4. LOCKED PREMISES / DECISIONS (do not relitigate)
<The frozen reference set the successor must honor; ledger #ids of resolved marks.>

## 5. OPEN / FLOATING TO OPERATOR
<Reserved decisions prepared and floated, awaiting the user.>

## 6. SENIOR WATCH (for the outgoing instance)
Step in only on: an escalation · a peer disagreement · an active agent gone quiet ·
an unaudited commit. Otherwise defer to the active pair. Sweep ~every 20 minutes.
```

## Why a handover doc plus the ledger

The ledger carries the *event history*; the handover doc carries the *active state* — what is settled, what is mid-flight, and what must not be relitigated. A successor that reads only the ledger has to reconstruct the present from scratch; a successor that reads only the handover loses the audit trail. Together they let the role outlive the instance at near-zero re-onboarding cost.
