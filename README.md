# The Orchestration Method

A method for running large, campaign-class work with AI agents — and the tooling to put it into practice.

One human operator directs a **manager** agent that, instead of doing the work in its own context, **orchestrates** waves of typed sub-agents (scouts, mathematicians, builders, auditors) to plan and execute work too large for any single context to hold. You plan to convergence across independent angles *before* you execute; every deliverable is checked by a *different* agent than the one that produced it; and the largest builds run two peer managers at once — an **Executor** and a live **Shadow** auditor — coordinating through a shared, append-only ledger.

This repository contains two things.

## 1. The teaching page — `Orchestration_Method.html`

A single, self-contained explainer (no external dependencies) that walks through the whole method: the two laws, the manager-progression flowchart, the agent-type taxonomy, the dispatch anatomy, multi-dimensional convergence, the audit superstructure, paired/shadow orchestration, the operating principles, and a worked example.

- **Open it locally:** open `Orchestration_Method.html` in any browser.
- **Live version** (once GitHub Pages is enabled on this repo): `https://tomadev23.github.io/orchestration-method/Orchestration_Method.html`

## 2. The skill — `orchestrator-mode/` (packaged at `dist/orchestrator-mode.skill`)

A portable Claude skill that operationalizes the method. When it loads, the agent adopts the orchestrator disposition: it recognizes campaign-class scope, plans to convergence before executing, dispatches typed sub-agents in waves, runs a mandatory independent secondary audit on any plan or code, and escalates to paired/Senior orchestration on the biggest builds — while staying lean on simple tasks (it will **not** spawn a swarm for a one-line edit or a quick question).

It also carries an **operating-principles** layer: a set of cross-cutting engineering rules (root cause over workaround, verify broadly, match ceremony to real stakes, decide-don't-block, …), each stated with its reasoning so it can be applied with judgment.

### Install / use

- **As a packaged skill:** `dist/orchestrator-mode.skill` — a zipped skill bundle; install it in a Claude client that supports skills.
- **From source:** point your agent at `orchestrator-mode/SKILL.md`; it progressively loads the `references/` and `assets/` only as needed.

### What's inside the skill

```
orchestrator-mode/
├── SKILL.md                          core: the two laws, trigger logic, the clean loop,
│                                     escalation, and the operating-principles layer
├── references/
│   ├── agent_taxonomy.md             the roster of typed seats + isolation rules + model policy
│   ├── audit_superstructure.md       the audit chain, standing watch, prototype gate, when-to-build
│   ├── paired_orchestration.md       Executor / Shadow, the Coordination Ledger, the Senior backstop
│   └── operating_principles.md       cross-cutting operational doctrine, each rule with its "why"
└── assets/
    ├── dispatch_template.md           a self-contained sub-agent briefing
    ├── coordination_ledger_template.md
    └── handover_template.md
```

## The method in one breath

Orchestrate; don't carry the load. Plan to convergence before you execute, in the same mode you execute. No agent audits its own work — a second, independent framing is where the real defects get caught. Simple things stay simple; deep things get the full wave chain.
