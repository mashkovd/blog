---
marp: true
theme: default
paginate: true
size: 16:9
header: 'DevLoop · human-auditable AI delivery'
footer: 'dmitriimashkov.com/approach'
style: |
  section {
    font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    padding: 54px 68px;
    background: #0f1720;
    color: #f5f7fa;
  }
  h1, h2, h3 { color: #ffffff; }
  h1 { font-size: 2.3em; line-height: 1.05; }
  h2 { font-size: 1.7em; margin-bottom: .35em; }
  h3 { font-size: 1.05em; text-transform: uppercase; letter-spacing: .08em; color: #70c7ff; }
  p, li { font-size: .88em; line-height: 1.42; }
  strong { color: #70c7ff; }
  code { background: #182532; color: #dff2ff; }
  blockquote { border-left: 4px solid #70c7ff; color: #d6dee6; margin-left: 0; padding-left: 22px; }
  .kicker { color: #70c7ff; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; font-size: .72em; }
  .muted { color: #8fa1b3; }
  .big { font-size: 1.35em; line-height: 1.25; }
  .metric { font-size: 2.0em; font-weight: 800; color: #ffffff; }
  .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; }
  .grid3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
  .card { background: #17232e; border: 1px solid #263746; border-radius: 18px; padding: 20px 22px; }
  .flow { font-size: .92em; font-weight: 700; background: #17232e; border-radius: 16px; padding: 20px; text-align: center; }
  .arrow { color: #70c7ff; padding: 0 .35em; }
  section.title { display: flex; flex-direction: column; justify-content: center; }
  section.title h1 { font-size: 2.8em; }
  section.title header, section.title footer, section.title::after { display: none; }
---

<!-- _class: title -->

# DevLoop
## Human-Auditable AI Delivery

**From written issue to observed deployment — with every step recorded for a person to audit.**

<div class="flow">issue <span class="arrow">→</span> proposal <span class="arrow">→</span> approval <span class="arrow">→</span> PR <span class="arrow">→</span> deploy</div>

<span class="muted">Dmitrii Mashkov · 2026</span>

---

<div class="kicker">Why this talk</div>

# The problem is not code generation

<div class="grid2"><div><div class="big">AI can create code fast.</div>

Teams still need **trust, ownership, and a safe path to production**.
</div><div class="card">

### Without a loop, automation becomes hard to review

- unclear source of truth
- stale context in agent runs
- approval hidden in chat
- merge decisions without evidence

</div></div>

---

<div class="kicker">Core idea</div>

# DevLoop in one sentence

> A change starts as a written issue and ends as a deployment that the platform observed.

<div class="flow">Issue <span class="arrow">→</span> Proposal <span class="arrow">→</span> Approval <span class="arrow">→</span> Implementation <span class="arrow">→</span> Review <span class="arrow">→</span> Deploy</div>

Every step leaves a record a person can audit.

<div class="grid3"><div class="card"><strong>Issue</strong><br><span class="muted">source of truth</span></div><div class="card"><strong>Approval</strong><br><span class="muted">durable signal</span></div><div class="card"><strong>Deploy</strong><br><span class="muted">observed evidence</span></div></div>

---

<div class="kicker">Mechanics</div>

# The design choice: artifacts over vibes

<div class="grid2"><div>

## The implementer never reads the issue.

It reads only the **approved proposal**.

That forces the proposal to contain the full acceptance criteria **before approval**.

</div><div class="card">

**issue** → intent  
**proposal** → contract  
**approval** → signal  
**implementation** → agent reads this  
**PR + tests** → review evidence

</div></div>

---

<div class="kicker">Control points</div>

# Gates turn automation into a process

The cycle continues only when the control point passes.

<div class="grid2"><div class="card">

### Proposal gate
Acceptance criteria are complete before implementation.

### Approval gate
Human approval is a durable workflow signal.

</div><div class="card">

### Review gate
Unresolved high-severity findings block merge.

### Branch gate
Main requires review, merge commits, no admin bypass.

</div></div>

---

<div class="kicker">Production snapshot</div>

# What is already running

<div class="grid3"><div class="card"><div class="metric">531</div>DevLoop proposals</div><div class="card"><div class="metric">24</div>production services</div><div class="card"><div class="metric">668</div>releases</div></div>

<div class="grid2" style="margin-top: 28px;"><div class="card">

### Platform layer
k3s on Hetzner + OpenTofu  
ArgoCD / Workflows / Rollouts  
Vault, Postgres, metrics and logs

</div><div class="card">

### Agent layer
Backstage as the portal  
Temporal for workflow state  
Claude Agent SDK + release automation

</div></div>

<span class="muted">Snapshot: 2026-09-11</span>

---

<div class="kicker">Workflow</div>

# Example: event-driven PR review

A GitHub event wakes the workflow. The workflow then reads **current evidence — not stale memory**.

<div class="flow">GitHub event <span class="arrow">→</span> read head SHA <span class="arrow">→</span> read CI + reviews <span class="arrow">→</span> blockers? <span class="arrow">→</span> notify / ready to merge</div>

<div class="card" style="margin-top: 32px;">

### Key rule
The agent reports only what it can verify from the **current PR head, checks, reviews, and comments**.

</div>

---

<div class="kicker">Takeaways</div>

# What teams can copy tomorrow

<div class="grid2"><div class="card">

### 1 · Start with one loop
Pick a narrow workflow: **issue → proposal → PR → review**.

### 2 · Make artifacts durable
Approvals, criteria, and evidence must survive chat history.

</div><div class="card">

### 3 · Put gates before execution
Agents should move only when the control point passes.

### 4 · Observe the result
A deployment counts when the platform sees it, not when someone says it happened.

</div></div>

---

<div class="kicker">Q&A</div>

# Closing thought

<div class="big">The goal is not “AI writes code”.</div>

The goal is a delivery loop where AI work is **reviewable, gated, and observable**.

<div class="card" style="margin-top: 30px;">

### Discussion prompts
Which part of your delivery process is currently invisible?  
What should become a durable artifact?  
Where should a human approval be required?

</div>
