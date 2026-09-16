---
marp: true
theme: default
paginate: true
size: 16:9
header: 'MCTL / DEVLOOP'
footer: 'dmitriimashkov.com/approach'
style: |
  @import url('https://ui.mctl.ai/0.5.0/mctl.css');
  @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=JetBrains+Mono:wght@400;500;600&family=Onest:wght@400;500;600;700&display=swap');
  section {
    --surface-bg: var(--mctl-surface-dark-bg, #0a0b0d);
    --surface-elevated: var(--mctl-surface-dark-elevated, #0f1114);
    --surface-card: var(--mctl-surface-dark-card, #15181d);
    --surface-line: var(--mctl-surface-dark-line, #1f242b);
    --surface-line-strong: var(--mctl-surface-dark-line-strong, #2a313a);
    --surface-fg: var(--mctl-surface-dark-fg, #e6e7e9);
    --surface-fg-muted: var(--mctl-surface-dark-fg-muted, #a4a8ae);
    --accent: var(--mctl-accent-terracotta-dark-primary, #e25a3c);
    --accent-highlight: var(--mctl-accent-terracotta-dark-highlight, #ff8a6a);
    --accent-soft: var(--mctl-accent-terracotta-dark-soft, #241512);
    --font-display: var(--mctl-typography-font-family-display, 'Onest', system-ui, sans-serif);
    --font-mono: var(--mctl-typography-font-family-mono, 'JetBrains Mono', monospace);
    --font-editorial: var(--mctl-typography-font-family-editorial, 'Instrument Serif', Georgia, serif);
    font-family: var(--font-display);
    padding: 60px 72px;
    background: var(--surface-bg);
    color: var(--surface-fg);
  }
  section::before {
    content: '';
    position: absolute;
    inset: 0;
    pointer-events: none;
    background-image: linear-gradient(var(--surface-line) 1px, transparent 1px), linear-gradient(90deg, var(--surface-line) 1px, transparent 1px);
    background-size: 64px 64px;
    opacity: .35;
  }
  section > * { position: relative; z-index: 1; }
  header, footer, section::after { font-family: var(--font-mono); color: var(--surface-fg-muted); font-size: 13px; }
  h1 { color: var(--surface-fg); font-size: 2.2em; line-height: .98; letter-spacing: -.035em; }
  h2 { color: var(--surface-fg); font-size: 1.3em; line-height: 1.08; }
  h3 { color: var(--surface-fg-muted); font-family: var(--font-mono); font-size: .62em; text-transform: uppercase; letter-spacing: .08em; }
  p, li { font-size: .78em; line-height: 1.45; }
  strong { color: var(--accent-highlight); }
  em { color: var(--accent-highlight); }
  .eyebrow { font-family: var(--font-mono); font-size: .52em; font-weight: 600; letter-spacing: .12em; text-transform: uppercase; color: var(--surface-fg-muted); margin-bottom: 16px; }
  .eyebrow::before { content: '— '; color: var(--accent); }
  .lede { font-family: var(--font-editorial); color: var(--surface-fg-muted); font-size: 1.18em; line-height: 1.12; max-width: 900px; }
  .muted { color: var(--surface-fg-muted); }
  .mono { font-family: var(--font-mono); }
  .grid2, .grid3, .grid4 { display: grid; gap: 20px; margin-top: 26px; }
  .grid2 { grid-template-columns: repeat(2, 1fr); }
  .grid3 { grid-template-columns: repeat(3, 1fr); }
  .grid4 { grid-template-columns: repeat(4, 1fr); }
  .panel { border: 1px solid var(--surface-line-strong); border-radius: 8px; background: var(--surface-elevated); padding: 20px; }
  .panel.accent { border-color: var(--accent); background: var(--accent-soft); }
  .panel.gate { border: 2px dashed var(--accent); }
  .n { display: block; color: var(--accent-highlight); font-family: var(--font-mono); font-size: .48em; margin-bottom: 10px; }
  .flow { display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px; margin-top: 26px; }
  .node { display: grid; place-items: center; min-height: 64px; padding: 8px; border: 1px solid var(--surface-line-strong); border-radius: 8px; background: var(--surface-elevated); text-align: center; font-size: .64em; }
  .node.gate { border: 2px dashed var(--accent); }
  .arrow { color: var(--accent); font-family: var(--font-mono); }
  .chain { display: grid; grid-template-columns: 1fr auto 1.2fr auto 1fr; gap: 12px; align-items: stretch; margin-top: 28px; }
  .artifact { display: flex; flex-direction: column; justify-content: space-between; min-height: 130px; padding: 20px; border: 1px solid var(--surface-line-strong); border-radius: 8px; background: var(--surface-elevated); }
  .artifact small { font-family: var(--font-mono); color: var(--surface-fg-muted); }
  .statement { border-left: 3px solid var(--accent); padding: 18px 0 18px 24px; margin-top: 28px; font-family: var(--font-editorial); font-size: 1.25em; line-height: 1.08; }
  .stats { display: grid; grid-template-columns: repeat(3, 1fr); border-block: 1px solid var(--surface-line); margin-top: 28px; }
  .stat { padding: 20px 0; }
  .stat + .stat { border-left: 1px solid var(--surface-line); padding-left: 20px; }
  .stat-value { display: block; font-size: 2.6em; line-height: .9; }
  .stat-label { font-family: var(--font-mono); color: var(--surface-fg-muted); font-size: .48em; letter-spacing: .08em; }
  section.title { display: flex; flex-direction: column; justify-content: center; }
  section.title h1 { font-size: 4em; line-height: .82; letter-spacing: -.06em; margin-bottom: .12em; }
  section.title h2 { font-family: var(--font-editorial); font-weight: 400; color: var(--surface-fg-muted); font-size: 1.7em; }
  section.title header, section.title footer, section.title::after { display: none; }
---

<!-- _class: title -->

<div class="eyebrow">Human-auditable AI delivery</div>

# DevLoop
## AI at the keyboard. Humans at the gates.

<div class="lede">From a written issue to a deployment the platform observed — with every step leaving a durable record a person can audit.</div>

<div class="mono muted" style="margin-top: 42px; font-size: 15px;">Dmitrii Mashkov · 2026 · MCTL UI tokens 0.5.0</div>

---

<div class="eyebrow">01 · Why this talk</div>

# AI coding is the easy part.

<div class="lede">The hard part is turning generated code into a delivery process a team can trust.</div>

<div class="grid4">
<div class="panel"><span class="n">01 / INTENT</span><h2>What?</h2><p>Where does the request come from, and what exactly was approved?</p></div>
<div class="panel"><span class="n">02 / OWNERSHIP</span><h2>Who?</h2><p>Who owns each phase — human, agent, or deterministic automation?</p></div>
<div class="panel"><span class="n">03 / CONTROL</span><h2>When?</h2><p>What must be true before the workflow is allowed to continue?</p></div>
<div class="panel"><span class="n">04 / EVIDENCE</span><h2>Prove it.</h2><p>Can the result be verified from current, durable artifacts?</p></div>
</div>

---

<div class="eyebrow">02 · The actual loop</div>

# Ten steps. Two gates. One closed loop.

<div class="flow">
<div class="node">Issue</div><div class="node">Investigate</div><div class="node">Proposal</div><div class="node gate">Approve</div><div class="node">Implement</div>
</div>
<div class="flow">
<div class="node">Monitor ↺</div><div class="node">Deploy</div><div class="node">Release</div><div class="node">Shepherd merge</div><div class="node gate">Review gate</div>
</div>

<div class="mono muted" style="margin-top:16px;font-size:13px;"><span class="arrow">- - -</span> dashed outline = control point · Approve = human · Review gate = automated</div>

---

<div class="eyebrow">03 · Contract boundary</div>

# The proposal is the contract.

<div class="lede">The implementer does <em>not</em> read the original issue. It works from the approved proposal.</div>

<div class="chain">
<div class="artifact"><small>INTENT</small><b>Issue</b><small>what should change</small></div>
<div class="arrow">→</div>
<div class="artifact" style="border-color:var(--accent)"><small>CONTRACT</small><b>Approved proposal</b><small>requirements · design · tasks</small></div>
<div class="arrow">→</div>
<div class="artifact"><small>EXECUTION</small><b>Implementer</b><small>works only from the contract</small></div>
</div>

<div class="panel accent" style="margin-top:24px;">Acceptance criteria must be complete <strong>before</strong> approval — not discovered halfway through implementation.</div>

---

<div class="eyebrow">04 · Control points</div>

# Two gates. Different owners.

<div class="grid2">
<div class="panel gate"><span class="n">HUMAN</span><h2>Approve</h2><p>Is this the right change? Is the proposal complete? Is the risk acceptable?</p><p class="mono muted">intent → durable approval signal</p></div>
<div class="panel gate"><span class="n">AUTOMATED</span><h2>Review gate</h2><p>Does the current PR head pass checks? Are blocking findings resolved? Is the evidence current?</p><p class="mono muted">head SHA + CI + reviews → gate result</p></div>
</div>

<div class="statement">Humans decide <em>what should happen</em>. Automation proves <em>what is true now</em>.</div>

---

<div class="eyebrow">05 · Production snapshot</div>

# This is not a diagram-only workflow.

<div class="stats">
<div class="stat"><span class="stat-value">531</span><span class="stat-label">DEVLOOP PROPOSALS</span></div>
<div class="stat"><span class="stat-value">24</span><span class="stat-label">SERVICES IN PRODUCTION</span></div>
<div class="stat"><span class="stat-value">668</span><span class="stat-label">GITHUB RELEASES</span></div>
</div>

<div class="mono muted" style="font-size:13px;margin-top:12px;">SNAPSHOT · 2026-09-11 · MCTL PLATFORM STATE + GITHUB</div>

<div class="grid2">
<div class="panel"><h3>Platform</h3><p>k3s · Hetzner · OpenTofu · ArgoCD · Workflows · Rollouts · Vault · CloudNativePG · VictoriaMetrics · Grafana · Loki</p></div>
<div class="panel"><h3>Agentic layer</h3><p>Role-specific agents · Temporal · MCP · Backstage · release automation · auditable Git artifacts</p></div>
</div>

---

<div class="eyebrow">06 · Event-driven review</div>

# Fresh evidence beats agent memory.

<div class="lede">A GitHub event wakes the workflow. The reviewer then re-reads the world as it exists <em>now</em>.</div>

<div class="flow">
<div class="node"><b>Event</b></div><div class="node"><b>Head SHA</b></div><div class="node"><b>Evidence</b></div><div class="node gate"><b>Gate</b></div><div class="node"><b>Outcome</b></div>
</div>

<div class="panel accent" style="margin-top:28px;">The reviewer reports only what it can verify against the <strong>current PR head and current evidence</strong>.</div>

---

<div class="eyebrow">07 · What to copy</div>

# You do not need MCTL to copy the pattern.

<div class="grid4">
<div class="panel"><span class="n">01</span><h2>Start with one loop</h2><p>Choose one narrow path from intent to reviewed change.</p></div>
<div class="panel"><span class="n">02</span><h2>Make artifacts durable</h2><p>Criteria, approvals and evidence must survive chat history.</p></div>
<div class="panel"><span class="n">03</span><h2>One owner per phase</h2><p>Human, agent or automation — never two competing owners.</p></div>
<div class="panel"><span class="n">04</span><h2>Close the loop</h2><p>Done means the platform observed the result, not merely that code merged.</p></div>
</div>

---

<div class="eyebrow">08 · Closing</div>

# AI at the keyboard.  
# **Humans at the gates.**

<div class="lede">DevLoop turns agentic development into a delivery process that is <strong>reviewable, gated and observable.</strong></div>

<div class="mono muted" style="margin-top:38px;font-size:14px;">Dmitrii Mashkov · dmitriimashkov.com/approach · github.com/mctlhq</div>
