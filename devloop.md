---
marp: true
theme: default
paginate: true
size: 16:9
header: 'DevLoop · Claude Meetup Podgorica'
footer: 'mashkovd.github.io/blog · dmitriimashkov.com/approach'
style: |
  section {
    font-family: Onest, Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    background: #0a0b0d;
    color: #e6e7e9;
    padding: 56px 72px;
  }
  h1 { font-size: 2.25em; line-height: .98; letter-spacing: -0.035em; }
  h2 { color: #a4a8ae; }
  strong { color: #ff8a6a; }
  code { background: #0f1114; color: #ff8a6a; padding: .08em .25em; border-radius: 4px; }
  pre { background: #0f1114; border: 1px solid #2a313a; border-radius: 8px; padding: 18px; }
  blockquote { border-left: 4px solid #e25a3c; color: #a4a8ae; padding-left: 24px; margin-left: 0; }
  .kicker { color: #a4a8ae; font-size: .65em; text-transform: uppercase; letter-spacing: .12em; }
  .grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; }
  .card { border: 1px solid #2a313a; border-radius: 8px; padding: 18px; background: #0f1114; }
  .hot { color: #ff8a6a; }
  .small { font-size: .75em; color: #a4a8ae; }
  section.title { display: flex; flex-direction: column; justify-content: center; }
  section.title header, section.title footer, section.title::after { display: none; }
---

<!-- _class: title -->

<div class="kicker">Claude Meetup Podgorica</div>

# DevLoop
## Human-auditable AI delivery

A GitHub issue becomes a reviewed proposal, an agent pull request, a release and a deployment — **with humans at the gates, not at the keyboard.**

Dmitrii Mashkov · 2026  
https://mashkovd.github.io/blog/

<!-- notes: Open with the audience question: who has let Claude write a PR? Who would merge one without reading? -->

---

<div class="kicker">01 · The problem</div>

# AI coding is the easy part.

The hard part is letting agents move work toward production without turning delivery into an opaque chat log.

<div class="grid"><div class="card"><b>Context drifts</b><br>Stale PR head, stale CI, old comments.</div><div class="card"><b>Approval disappears</b><br>Chat approval is not a workflow signal.</div><div class="card"><b>Done is ambiguous</b><br>Merge ≠ release ≠ observed deployment.</div><div class="card hot"><b>DevLoop</b><br>Move trust from conversation to artifacts.</div></div>

<!-- notes: The problem is not generation quality alone. It is control, ownership and evidence. -->

---

<div class="kicker">02 · The loop</div>

# Ten steps. Two gates. One closed loop.

`Issue → Investigate → Proposal → Approve → Implement → Review gate → Shepherd merge → Release → Deploy → Monitor → Issue`

**Approve** = human decision  
**Review gate** = automated evidence

<!-- notes: Keep these names constant through the whole talk. -->

---

<div class="kicker">03 · Artifacts over vibes</div>

# The proposal is the contract.

The implementer does **not** read the original issue. It reads the approved proposal.

```text
agents-state/portfolio/proposals/issue-5-p3-content-collections-for-projects-jour/
  requirements.md
  design.md
  tasks.md
```

`Issue → Accepted proposal → Agent PR`

<!-- notes: This is the strongest design choice in the system. -->

---

<div class="kicker">04 · Boundary</div>

# Why hide the issue from the implementer?

Because “go read everything and infer intent” is exactly how agentic workflows become non-auditable.

<div class="grid"><div class="card"><b>Bad loop</b><br>Read all context and guess intent.</div><div class="card"><b>DevLoop</b><br>Implement the approved contract. Stop if it is incomplete.</div></div>

> If the proposal is incomplete, stopping is success.

<!-- notes: A stop is a good outcome when the contract is bad. -->

---

<div class="kicker">05 · Claude in the loop</div>

# Where Claude actually works.

<div class="grid"><div class="card"><b>Proposer</b><br>issue → requirements/design/tasks</div><div class="card"><b>Implementer</b><br>accepted proposal → PR</div><div class="card"><b>Reviewer</b><br>current head SHA + CI + comments</div><div class="card"><b>Shepherd</b><br>merge only when gates agree</div></div>

Claude Agent SDK · MCP tools · GitHub · MCTL control plane

<!-- notes: Explain Claude roles, not “one agent does everything”. -->

---

<div class="kicker">06 · Control points</div>

# Humans decide whether. Claude decides how.

<div class="grid"><div class="card"><b>Human gate: Approve</b><br>Right change? Complete proposal? Acceptable risk?</div><div class="card"><b>Automated gate: Review</b><br>Current head passes? P1/P2 resolved? Evidence fresh?</div></div>

<!-- notes: This is not no-humans. It is humans at high-leverage control points. -->

---

<div class="kicker">07 · Real run</div>

# A real agent PR: portfolio #21.

Opened by `mctl-agents[bot]`, from an accepted proposal, closes `mctlhq/portfolio#5`.

```text
02:11  PR opened
02:18  Claude review: 0 P1 · 3 P2 · 4 P3
03:02  merged: 4 commits · 18 files · +1006 / −3
```

https://github.com/mctlhq/portfolio/pull/21

<!-- notes: This is the concrete example. Show the real PR if Wi-Fi works; record demo beforehand. -->

---

<div class="kicker">08 · Review gate</div>

# The reviewer blocked real issues.

<div class="grid"><div class="card"><b>P2</b><br>ADR headings could pass in English only.</div><div class="card"><b>P2</b><br>EN/RU project files could drift independently.</div><div class="card"><b>P2</b><br>Tests existed but were not wired into CI/build.</div><div class="card hot"><b>Rule</b><br>Gate uses current evidence, not vibes.</div></div>

<!-- notes: This answers “does Claude review actually catch anything?”. -->

---

<div class="kicker">09 · What broke</div>

# The useful part is what failed.

<div class="grid"><div class="card"><b>#17</b><br>Lockfile platform trap → use `--package-lock-only`.</div><div class="card"><b>#19</b><br>Storage failure made toggles inert → persistence may fail, function must not.</div><div class="card"><b>#29</b><br>PR-body acceptance criteria deadlocked → criteria must be satisfiable by commit.</div><div class="card"><b>#21</b><br>Human found false evidence row → preserve mistake, fix narrative.</div></div>

<!-- notes: These are the credibility slides. Failures became rules. -->

---

<div class="kicker">10 · Snapshot</div>

# What 531 loops taught me.

<div class="grid"><div class="card"><h1>531</h1>DevLoop proposals</div><div class="card"><h1>24</h1>production services</div><div class="card"><h1>668</h1>releases</div><div class="card hot">context boundaries > bigger prompts<br>durable artifacts > chat history<br>independent verification > confidence</div></div>

<span class="small">Snapshot: 2026-09-11</span>

<!-- notes: Do not dwell on k3s/Argo/Vault here; keep infrastructure for backup. -->

---

<div class="kicker">11 · Takeaway</div>

# Start with one loop.

`issue → proposal → approval → PR → independent review`

Do not start by building a platform. Start by making one AI-assisted path **reviewable, gated and observable**.

<!-- notes: Make this copyable tomorrow. -->

---

<div class="kicker">Q&A</div>

# AI at the keyboard. Humans at the gates.

DevLoop turns Claude-assisted development into a delivery process a team can audit.

https://dmitriimashkov.com/approach/  
https://github.com/mctlhq  
https://mashkovd.github.io/blog/

<!-- notes: Invite questions about MCP, Claude roles, operational gates and failure modes. -->
