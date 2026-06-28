# TASKS.md — tool-atlas

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Elyos

Each row below becomes one **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- **id** → stable `tool-atlas-<area>-NNN` (the table's ID column).
- **title** → the task title.
- **project** → `"tool-atlas"`.
- **type** → one of `code | research | writing | data | design-spec | maintenance`
  (entry authoring = `writing`; schema/guide = `design-spec`; SSG/CI = `code`; dataset = `data`;
  partner outreach/source verification = `research`; re-review = `maintenance`).
- **lane** → `donated` (this project has no funded tasks; if one were added it would require
  `fundedBudgetUsd`).
- **priority** → `high | medium | low` (the table's Size column is the *token estimate*, not
  priority; priority is set per task in the JSON).
- **domain** → array, e.g. `["education","practical-skills","open-reference","accessibility"]`.
- **riskTier** → `low` by default; `medium` for power-tool/injury-risk entries (Risk column).
- **urgent** → boolean (default `false`).
- **deliverable** → `pr | dataset | document | translation` (Deliverable column).
- **tokenEstimate** → `small | medium | large` (Size column).
- **status** → `open` for all (new backlog).
- **context / objective / acceptanceCriteria[] / output** → from the task detail.
- **resources[]** → links to schema, style guide, safety guide, source list.
- **requestor** → partner org (TO BE SECURED) — omitted/empty until confirmed.
- **verifiedNeed** → **`false`** on all tasks until an adopting partner is secured (honest).
- **outputLicense** → `CC-BY-4.0` for content/data, `MIT` for code.

Reviewer column: **Ed** = editorial reviewer (author ≠ reviewer); **Safety** = competent safety
reviewer (mandatory for medium-risk); **Maint** = maintainer.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-schema-001 | Define atlas entry JSON Schema (+ CI validation) | design-spec | medium | low | pr | — | Maint |
| tool-atlas-guide-002 | Write editorial style guide | design-spec | small | low | document | schema-001 | Maint |
| tool-atlas-guide-003 | Write safety guide + medium/high risk rubric | design-spec | medium | medium | document | schema-001 | Safety, Maint |
| tool-atlas-repo-004 | Scaffold repo (TS/ESM/pnpm, lint, validate, CI) | code | small | low | pr | — | Maint |
| tool-atlas-entry-005 | Reference entry: tape measure (low-risk exemplar) | writing | small | low | document | schema-001, guide-002 | Ed |

**Acceptance criteria — key tasks**

- **tool-atlas-schema-001**
  - JSON Schema covers all entry fields (name, aliases, category, purpose, when-to-use, technique
    steps, safety{riskTier,hazards,ppe,requiredCompetence,leadWithSafety}, commonMistakes,
    careAndMaintenance, related tools/tasks, media[{file,license,author,sourceUrl,provenanceNote}],
    sources[], license, version, lastReviewed, reviewers).
  - `media` requires a `license` field; schema is invalid without it.
  - Schema enforces that `riskTier:"medium"` requires a non-empty `safety.hazards` and `safety.ppe`.
  - AJV validation runs in CI and fails on any invalid entry.
- **tool-atlas-guide-003**
  - Defines the hazard-first format for medium-risk entries (hazards + PPE before technique).
  - Provides a written rubric for the low/medium/high line (incl. ladders, mains electrical, gas).
  - States refusal rules: no guard-defeat, illegal modification, or weapons content.
  - Reviewed and signed off by a safety reviewer.
- **tool-atlas-entry-005**
  - Original text; technique verified against ≥ 2 authoritative cited sources (not copied).
  - Diagram is original or verifiably CC-compatible with a complete provenance record.
  - Schema-valid; passes editorial review by someone other than the author.

**Definition of Done (M0):** schema + style guide + safety guide merged and CI-enforced; repo
scaffolding green (`pnpm build && pnpm test && pnpm lint`); one schema-valid, editorially reviewed
low-risk entry published. End-to-end authoring of a correct, safe, machine-readable entry is proven.

---

## Milestone M1 — Seed corpus & partner outreach

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-entry-101 | Seed entries: hammer, screwdriver set, level (batch) | writing | medium | low | document | schema-001, guide-002 | Ed |
| tool-atlas-entry-102 | Seed entries: hand saw, utility knife, chisel (batch) | writing | medium | low | document | guide-003 | Ed, Safety |
| tool-atlas-entry-103 | Seed entries: pliers, wrench (batch) | writing | small | low | document | schema-001 | Ed |
| tool-atlas-entry-104 | Seed entry: power drill (medium-risk exemplar) | writing | medium | medium | document | guide-003 | Safety, Ed |
| tool-atlas-data-105 | Glossary + cross-link graph (related tools ↔ tasks) | data | medium | low | dataset | entry-101..104 | Maint |
| tool-atlas-research-106 | Partner outreach packet + log first conversations | research | small | low | document | entry-005 | Steward |

**Acceptance criteria — key tasks**

- **tool-atlas-entry-104 (power drill, medium-risk)**
  - Entry leads with hazards and required PPE before technique (hazard-first).
  - `riskTier:"medium"`; safety section complete (hazards, PPE, required competence).
  - Reviewed and signed off by a safety reviewer; reviewer recorded in `reviewers[]`.
  - No content on defeating clutch/guard or unsafe modification.
- **tool-atlas-entry-102 (saw/knife/chisel batch)**
  - Each entry hazard-aware; sharp-tool safety and cut-direction guidance correct and reviewed.
  - Original media with provenance; schema-valid; citations to authoritative sources.
- **tool-atlas-research-106 (partner outreach)**
  - A reusable outreach packet describing the atlas, license, and adoption ask.
  - ≥ 1 outreach packet sent; ≥ 1 partner conversation logged with outcome/next step.
  - Honest status recorded; `verifiedNeed` flips to `true` only on written partner confirmation.

**Definition of Done (M1):** all 10 seed hand-tool entries published and schema-valid (drill via
the medium-risk safety path); glossary + initial cross-link graph merged; partner outreach started
with ≥ 1 logged conversation.

---

## Milestone M2 — Static-site explorer & dataset release

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-site-201 | Static-site generator: render entries (accessible, WCAG-AA aim) | code | large | low | pr | entry-101..104 | Maint |
| tool-atlas-site-202 | Browse: category nav + search + cross-link graph UI | code | medium | low | pr | site-201, data-105 | Maint |
| tool-atlas-data-203 | Publish versioned CC-BY dataset + provenance manifest | data | small | low | dataset | site-201 | Maint |
| tool-atlas-site-204 | Deploy live atlas (static hosting) + canonical attribution | code | small | low | pr | site-202 | Maint |

**Acceptance criteria — key tasks**

- **tool-atlas-site-201**
  - Renders every schema-valid entry; build fails if any entry is invalid.
  - Medium-risk entries render hazards/PPE first (driven by `safety.leadWithSafety`).
  - Accessibility checks pass (keyboard nav, alt text on diagrams, contrast — WCAG-AA target).
- **tool-atlas-data-203**
  - Full corpus exported as a single versioned dataset under CC-BY-4.0.
  - Per-asset provenance + license included; attribution string published.

**Definition of Done (M2):** live, accessible, searchable atlas reachable at a public URL; first
versioned CC-BY dataset published with provenance; cross-link navigation works.

---

## Milestone M3 — Safety-track hardening & power-tool expansion

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-guide-301 | Safety-review checklist + reviewer onboarding doc | design-spec | small | low | document | guide-003 | Safety, Maint |
| tool-atlas-code-302 | CI rule: medium-risk ⇒ safety section + recorded reviewer | code | small | medium | pr | schema-001, guide-301 | Maint |
| tool-atlas-entry-303 | Power-tool entries: circular saw, angle grinder, jigsaw (batch) | writing | large | medium | document | guide-301 | Safety, Ed |
| tool-atlas-entry-304 | Injury-risk entries: step ladder, extension cord/electrical basics (defer-to-pro where required) | writing | medium | medium | document | guide-301 | Safety, Ed |

**Acceptance criteria — key tasks**

- **tool-atlas-code-302**
  - CI fails any `riskTier:"medium"` entry lacking a completed safety section or a recorded safety
    reviewer.
- **tool-atlas-entry-303 (power tools)**
  - Each entry hazard-first with correct PPE and authoritative citations.
  - No guard-defeat/unsafe-modification content; safety reviewer sign-off recorded.
- **tool-atlas-entry-304 (electrical/ladder)**
  - Where law/safety requires a professional (e.g. mains/permanent wiring), entry defers to a
    qualified electrician rather than instructing high-stakes DIY.

**Definition of Done (M3):** safety checklist + onboarding documented; CI enforces the medium-risk
rule; ≥ 5 medium-risk entries shipped, each hazard-first and safety-reviewed.

---

## Milestone M4 — Category expansion & adoption

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-entry-401 | Garden/kitchen entries (batch ≥ 8, low-risk) | writing | large | low | document | guide-002 | Ed |
| tool-atlas-entry-402 | Textile/digital-dev entries (batch ≥ 7) | writing | medium | low | document | guide-002 | Ed |
| tool-atlas-research-403 | Confirm partner adoption + collect use report | research | small | low | document | site-204, research-106 | Steward |
| tool-atlas-maint-404 | Re-review cadence: refresh entries past lastReviewed window | maintenance | small | low | document | entry-005..304 | Ed, Safety |

**Acceptance criteria — key tasks**

- **tool-atlas-research-403 (adoption — the real outcome)**
  - ≥ 1 education/makerspace partner confirms adoption in writing.
  - A use report is collected (how it was used, beneficiary-usefulness feedback).
  - `verifiedNeed` updated to `true` on confirmation; ≥ 1 external dataset reuse documented.
- **tool-atlas-entry-401 / 402 (breadth)**
  - ≥ 15 new entries spanning ≥ 2 new categories; each schema-valid with original/licensed media.

**Definition of Done (M4):** ≥ 15 entries across ≥ 2 new categories published; ≥ 1 partner adoption
confirmed with use report; ≥ 1 documented external reuse of the CC-BY dataset; re-review cadence
running.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| tool-atlas-i18n-501 | Localization framework + first translated entries | code/translation | large | low | translation | Needs schema localization decision (Open Q6) |
| tool-atlas-contrib-502 | External contribution + review-scaling model | design-spec | medium | low | document | Opens UGC review burden (Open Q7) |
| tool-atlas-media-503 | Original-diagram pipeline + reusable SVG component kit | design-spec | medium | low | document | Speeds illustrated entries |
| tool-atlas-entry-504 | Specialty-trade tools (plumbing/automotive basics, defer-to-pro) | writing | large | medium | document | Mostly medium-risk; safety gate |
| tool-atlas-data-505 | Public API / structured export endpoint over the dataset | code | medium | low | dataset | Only if downstream demand emerges |
| tool-atlas-research-506 | Beneficiary survey instrument + outcome dashboard | research | small | low | document | Powers success-metric tracking |

---

## Example task JSON

```json
{
  "id": "tool-atlas-schema-001",
  "title": "Define atlas entry JSON Schema (+ CI validation)",
  "project": "tool-atlas",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["education", "practical-skills", "open-reference", "accessibility"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "pr",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "tool-atlas is an open CC-BY reference atlas of tools. Every entry must be uniformly machine-readable so it can power a static-site explorer, courses, and search. Safety must be enforceable as data, not styling, because power-tool/injury-risk entries are medium risk and must lead with hazards and PPE.",
  "objective": "Define and publish a versioned JSON Schema for an atlas entry, wired into CI via AJV, that captures all entry fields and enforces the safety and license invariants.",
  "acceptanceCriteria": [
    "Schema covers name, aliases, category, purpose, whenToUse, technique.steps, safety{riskTier,hazards,ppe,requiredCompetence,leadWithSafety}, commonMistakes, careAndMaintenance, relatedTools, relatedTasks, media, sources, license, version, lastReviewed, reviewers.",
    "Each media item requires a license field; the schema is invalid without it.",
    "riskTier='medium' requires non-empty safety.hazards and safety.ppe.",
    "AJV validation runs in CI and fails on any invalid entry.",
    "pnpm build && pnpm test && pnpm lint pass."
  ],
  "resources": [
    "C:\\code\\elyos\\governance\\proposals\\tool-atlas.md",
    "C:\\code\\elyos\\packages\\schema\\src\\schemas.ts",
    "C:\\code\\elyos\\planning\\projects\\tool-atlas\\PLAN.md"
  ],
  "output": "A merged PR adding the atlas entry JSON Schema, AJV-based validation script, and CI wiring, with the schema documented in the repo.",
  "requestor": "",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```
