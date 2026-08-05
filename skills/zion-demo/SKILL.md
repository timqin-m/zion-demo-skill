---
name: zion-demo
description: >-
  Run a live Zion plugin demo from the Git scaffold: clone plugin-templete,
  connect a Zion project, inventory schema/agents/actionflows, propose a
  data→pages→logic→experience structure plan, then build after confirmation
  with strong visual impact and UX. Use when starting a Zion demo, swapping
  projectExId, or the user mentions plugin-templete, Zion 演示脚手架, or
  现场演示 Zion plugin.
---

# Zion plugin demo

Scaffold: https://github.com/timqin-m/plugin-templete

Audience may be watching. Keep replies short and natural. Do not dump ops checklists unless asked.

Also load and follow the `zion-platform` skill / Zion MCP for any Zion work.

## Inputs

Required (ask only if missing):

- `projectExId` — Zion project external id

Optional:

- Demo requirements — what to build this session
- Brand / visual direction

If requirements are omitted, still connect + inventory, then ask what to demo.  
If visual direction is omitted, pick one clear direction that fits the domain — do not ship a generic gray admin look.

## Workflow

Copy and track:

```
Demo progress:
- [ ] 1. Clone scaffold
- [ ] 2. Connect Zion project
- [ ] 3. Inventory (tables / agents / AFs)
- [ ] 4. Structure plan → wait for OK
- [ ] 5. Build: data → pages → logic (+ visual/UX)
```

### 1. Clone scaffold

If not already in a clone of `plugin-templete`:

```bash
git clone https://github.com/timqin-m/plugin-templete.git
```

Work inside that clone (or the folder the user points at). Prefer a fresh clone per demo session when starting from scratch.

### 2. Connect Zion project

1. Confirm login (`whoami`); `login` if needed.
2. `project set-current --projectExId <id>`
3. `schema load` — read `typeSystem` exactly; route pre/post per `zion-platform`. Never guess.
4. Update `.zion-mcp/project-context.json` and `web/.env` (and `.env.example` values for this session) to the live `projectExId` / GraphQL / WS URLs.

### 3. Inventory

From the **live** schema only, briefly list:

- Tables (and notable relations)
- Agents
- Actionflows

Do not reuse names/ids from a previous demo.

### 4. Structure plan (stop here)

Do **not** write feature code yet. Propose a short plan:

1. **数据** — tables / fields / relations (reuse vs create)
2. **页面** — which pages, each page's job
3. **逻辑** — which Actionflows vs Agents, inputs/outputs
4. **体验** — visual direction (mood / palette / type), first-viewport impact, key UX flows (empty / loading / error / success), 2–3 intentional motions

If requirements were omitted, ask what to demo before proposing the plan.  
Wait for user confirmation before implementing.

### 5. Build after OK

Implement in order: **数据 → 页面 → 逻辑**. UI quality is part of “页面”, not a later polish pass.

**Visual / UX bar (required for demo pages):**

- First viewport should feel like a product, not a debug panel — clear hierarchy, atmosphere (gradient / texture / imagery when it fits), expressive typography (not default Inter/Roboto/Arial/system-only).
- One job per section; reduce clutter (no pill clusters, stat-strip spam, or decorative card walls).
- Define CSS variables for the chosen direction; avoid default AI looks (purple-on-white, cream+terracotta serif, broadsheet hairlines).
- Real UX: loading / empty / error / success states; obvious primary action; mobile-usable layout.
- Ship at least 2–3 intentional motions (entrance, state change, or feedback) — presence, not noise.
- Keep scaffold plumbing (Vite proxy, Apollo). Health page can stay for diagnostics; business routes should own the demo story.

Also:

- Verify each slice (runtime query / AF / agent / `npm run dev`).
- On blockers, say where it stuck (auth / schema / permissions / binding / runtime) — do not fake success.
- Do not invent schema paths or ids.
- Do not commit one-off demo business back into the template repo unless asked.

## Kickoff lines (for the human)

Full:

```text
用 zion-demo skill。连上 Zion 项目 {{PROJECT_EX_ID}}。

我们要做的是：
{{DEMO_REQUIREMENTS}}

先摸清现状，再按数据、页面、逻辑、体验出结构方案，我确认后再动手。页面要有视觉冲击感，UX 走通。
```

Spoken:

> 用 zion-demo，连这个 Zion 项目，摸清现状。我们要做 {{DEMO_REQUIREMENTS}}——先出结构方案，页面要好看有冲击，我点头后再做。
