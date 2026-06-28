# PLAN.md — tool-atlas

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

**tool-atlas** is an open, structured reference atlas of tools — what each tool is, what it is
for, when to choose it, how to use it safely and well, the mistakes people commonly make, and how
to care for and maintain it. It begins with the most common hand, household, and workshop tools
and is deliberately extensible to garden, kitchen, textile, and digital/dev tooling.

The core insight: practical know-how is usually transmitted person-to-person (a parent, a shop
teacher, a mentor at a makerspace), which leaves people without that access at a disadvantage. The
open web's answer — ad-laden, SEO-spam how-to sites and unverified videos — is uneven, often
unsafe, and not reusable. tool-atlas produces **original CC-BY content with original or
openly-licensed diagrams**, stored as **machine-readable JSON/Markdown** so it can power a
static-site explorer, courses, apps, and search.

Every entry is self-contained, which makes the project an ideal fit for Elyos' donated lane:
**one tool = one bounded task** with near-unlimited fan-out. Overall risk is **low**, but entries
for power tools and anything with injury risk (saws, grinders, electrical work, ladders) are
**medium** risk and must lead with hazards/PPE and pass a safety reviewer before they ship.

The headline gates are (1) a **license/provenance gate** — original or verifiably
openly-licensed media only, with recorded provenance — and (2) a **safety gate** for
medium-risk entries. No content that teaches unsafe or illegal modification (e.g. disabling tool
safety guards, weapons fabrication).

## Problem & beneficiaries

**Who is helped.** People learning practical skills without access to a mentor or shop class:
self-taught makers and renters, first-time homeowners, students, and the staff/learners at
makerspaces, schools, and vocational programs who need clear, trustworthy, reusable reference
material.

**The need.** The proposal asserts the need as *verified: yes* on the grounds that practical
know-how is unevenly distributed. That is a reasonable, well-supported premise (it motivates shop
classes, makerspaces, and library tool-libraries everywhere). However, **a specific partner
organization that will adopt the atlas and confirm fitness-for-purpose is TO BE SECURED.** Until
an education/makerspace partner signs on, `verifiedNeed` on individual tasks is honestly set to
`false`, and the Definition of Shipped's "adopted by at least one partner" clause remains an open
dependency, not an assumption.

**Partner org.** TO BE SECURED — target profiles: a community makerspace network, a public
library tool-library program, a vocational/CTE program, or an open-education nonprofit. Early
outreach is itself a milestone task (see Roadmap M0/M1).

**Why not the existing web.** Existing how-to content is (a) not openly licensed, so it cannot be
remixed into courses or apps; (b) inconsistent on safety; and (c) optimized for ad revenue, not
learning. tool-atlas is the open, structured, safety-first alternative.

## Goals and non-goals

**Goals**
- Publish a browsable, openly-licensed (CC-BY) atlas of tools with consistent, high-quality
  entries.
- Make the content **machine-readable** (validated JSON + Markdown) so third parties can build on
  it.
- Establish a **safety-first** editorial standard: medium-risk entries lead with hazards and PPE
  and are reviewed by a competent safety reviewer.
- Make entries **bounded and forkable** so AI sessions in the donated lane can author them with
  high fan-out and consistent quality.
- Secure at least one education/makerspace partner who adopts the atlas and reports real use.

**Non-goals**
- Not a marketplace, price comparison, or affiliate/shopping site.
- Not a repair-manual or service-manual database for specific product models.
- Not a forum, Q&A site, or user-generated-content platform (at least through the first phases).
- Not a host for video. Diagrams and still imagery only, to keep provenance and accessibility
  tractable.
- Not a source of unsafe/illegal modification content (guard removal, weaponization, defeating
  safety interlocks) — explicitly refused.
- Not a substitute for professional or licensed work where law/safety requires it (e.g. mains
  electrical, gas); such entries point to qualified help rather than instructing high-stakes DIY.

## Success metrics (outcomes)

Outcome-based, beneficiary-centric. Vanity metrics (raw pageviews, star counts) are explicitly
**not** primary.

| Metric | Baseline (2026-06-28) | Target (first 2 phases) |
| --- | --- | --- |
| Peer-reviewed, published entries | 0 | 25+ (10 seed hand tools + 15 across categories) |
| Education/makerspace partners adopting the atlas | 0 | ≥ 1 with written adoption + use report |
| Beneficiary-reported usefulness (partner survey, "helped me do the task safely") | n/a | ≥ 80% of respondents agree |
| Medium-risk entries shipped with completed safety review | 0 | 100% of medium-risk entries (no exceptions) |
| Entries with recorded media provenance + valid license | n/a | 100% (hard gate) |
| Downstream reuse (forks, course/app integrations citing CC-BY) | 0 | ≥ 1 documented external reuse |
| Schema-valid machine-readable dataset published | none | 1 versioned CC-BY dataset release |

Note: the partner-adoption and beneficiary-usefulness metrics are the **true outcome measures**;
entry count and dataset release are necessary enablers, not the goal in themselves.

## Scope

**In scope**
- An entry schema (JSON Schema) capturing: name, aliases, category, purpose, when-to-use,
  technique steps, safety (hazards/PPE/required competence), common mistakes, care/maintenance,
  related tools, media (with license + provenance), and sources.
- A style guide + safety guide that define the editorial bar and the medium-risk hazard-first
  format.
- Seed content: 10 common hand tools, then expansion across hand/household/workshop and into
  garden/kitchen/textile/digital as capacity allows.
- A glossary and a cross-link graph (related tools ↔ tasks).
- A static-site generator that renders validated entries into a browsable, accessible atlas, plus
  a downloadable CC-BY dataset.
- Provenance records for every media asset.

**Out of scope (will NOT do)**
- Buying guides, prices, affiliate links, brand/model recommendations.
- Video hosting or production.
- User accounts, comments, or community-submitted entries (deferred beyond first phases).
- Step-by-step instructions for tasks that legally require a licensed professional.
- Any unsafe/illegal modification, bypass of safety devices, or weapons content.
- Medical/structural/electrical-code adjudication — entries defer to qualified authorities and
  local code.

## Solution approach & architecture

A **content-and-data project** with a thin software layer. The valuable artifact is the
structured, reviewed corpus; the static site is a renderer over it.

**Components**
1. **Schema package** — a versioned JSON Schema for an atlas entry, validated in CI (reuse the
   project's TypeScript/ESM + AJV conventions, mirroring `packages/schema`).
2. **Content corpus** — one file per entry. Source of truth is structured **JSON** (or Markdown
   with YAML front-matter compiled to JSON); prose fields are authored Markdown. Organized by
   category.
3. **Media + provenance store** — original SVG/PNG diagrams and any openly-licensed imagery, each
   paired with a provenance record (source, author, license, URL, retrieval date).
4. **Static-site generator (SSG)** — renders validated entries into an accessible, browsable site
   with category navigation, search, and the cross-link graph. Exports the full corpus as a
   downloadable CC-BY dataset.
5. **Editorial tooling** — lint/validate scripts (schema validation, link checking, license-field
   presence, "medium-risk requires safety section" rule) run in CI.

**Tech stack.** TypeScript, ESM, pnpm workspaces. AJV for schema validation. A lightweight,
well-supported SSG (e.g. Astro or Eleventy — decision deferred, see Open questions) chosen for
accessibility, static output, and low maintenance. Code MIT-licensed; content CC-BY-4.0.

**Data model (entry, abridged).**
```
id, name, aliases[], category, subcategory,
purpose, whenToUse, alternatives[],
technique: { steps[], tips[] },
safety: { riskTier, hazards[], ppe[], requiredCompetence, leadWithSafety:boolean },
commonMistakes[], careAndMaintenance,
relatedTools[], relatedTasks[],
media: [{ file, type, license, author, sourceUrl, provenanceNote }],
sources: [{ title, url, accessed, note }],
license, version, lastReviewed, reviewers[]
```

**Key decisions**
- **Structured-first, prose-inside.** Authoring targets the schema so every entry is uniformly
  machine-readable; prose lives in defined fields rather than free-form pages.
- **Safety as data, not styling.** `riskTier` and `safety.leadWithSafety` are data fields the SSG
  and CI enforce, so the hazard-first treatment for medium-risk tools cannot be skipped.
- **License field is mandatory** on every media asset; CI fails an entry that lacks it.
- **Bounded tasks.** Each entry is one task with a fixed template, enabling consistent fan-out.

## Data, licensing & compliance

**This section is a hard gate. Be conservative.**

- **Text content:** 100% original writing authored for this project. Technique is verified against
  authoritative sources (manufacturer safety guidance, OSHA/HSE-type public guidance, established
  trade references), which are **cited but not copied**. No paraphrase-laundering of copyrighted
  how-to text.
- **Media (diagrams/images):** **original artwork by default.** Any non-original asset must be
  verifiably under a license that permits reuse and derivatives compatible with CC-BY (e.g.
  CC0, CC-BY, CC-BY-SA only if isolated and clearly attributed, or public domain). **No
  "found on the web" images.** Every asset carries a provenance record: source, author, license,
  URL, retrieval date. CI rejects entries with media missing a license field.
- **Output license:** content released under **CC-BY-4.0**; code under **MIT**. Each published
  entry and the dataset release state the license explicitly with attribution requirements.
- **Attribution requirements:** CC-BY requires downstream users to credit tool-atlas; the site and
  dataset include the canonical attribution string and per-asset author credits.
- **Privacy / PII:** the project handles **no personal data**. No user accounts, no analytics that
  collect PII in the first phases. Contributors are credited by chosen handle only.
- **Provenance model:** a machine-readable provenance block per media asset and a `sources[]` list
  per entry; both are validated and published with the dataset so reuse is auditable.
- **Refusal compliance:** content that would teach defeating safety guards/interlocks, illegal
  modification, or weapons fabrication is refused and flagged per Elyos guardrails — regardless of
  how the request is framed.

## Quality, review & risk gates

**Risk tier.** Project baseline **low**; individual entries are **medium** when they cover power
tools or injury-risk activities (saws, grinders, electrical, ladders, anything with a
non-trivial harm path). The schema's `riskTier` field records this per entry. No entries are
expected to be `high` (which would require credentialed expert sign-off before merge); if a
proposed entry edges into high-stakes territory (e.g. mains electrical, gas, structural), it is
either reframed to "defer to a qualified professional" or escalated for expert review.

**Required review before "done":**
- **Every entry:** editorial review against the style guide (clarity, completeness, schema
  validity, citation quality, original-media check) by a maintainer/reviewer other than the author.
- **Medium-risk entries:** **additional safety review** by a reviewer competent in that tool/area,
  confirming the hazard-first ordering, correct PPE, accurate technique, and that no unsafe shortcut
  is implied. This review is mandatory and recorded in `reviewers[]`/`lastReviewed`.
- **License/provenance gate:** automated (CI) presence checks + human spot-verification of any
  non-original asset's license.

**Definition of Shipped (project).** Per the proposal: a published, browsable atlas with a
growing, peer-reviewed set of entries, **adopted by at least one education/makerspace partner**,
with downloadable structured data under CC-BY. Per Elyos' "delivered, not merged" bar, an entry is
*delivered* only when: acceptance criteria met + schema-valid + CI green + editorial (and safety,
if medium) review passed + published on the live atlas + reachable by the intended beneficiaries.

## Roadmap & milestones

**M0 — Foundation & cold-start (thin).**
Goal: make it possible to author one correct, safe, machine-readable entry end-to-end.
Exit criteria: entry JSON Schema published and CI-validated; style guide + safety guide merged;
**one** complete reference entry (a low-risk hand tool, e.g. tape measure) authored, reviewed, and
schema-valid; repo scaffolding (TS/ESM/pnpm, lint, validate) green.

**M1 — Seed corpus & partner outreach.**
Goal: a credible starter set + a real beneficiary.
Exit criteria: 10 seed hand-tool entries published (hammer, screwdriver set, tape measure, hand
saw, level, utility knife, pliers, wrench, drill, chisel) — **drill** routed through the
medium-risk safety path; glossary + initial cross-link graph in place; ≥ 1 partner outreach packet
sent and ≥ 1 partner conversation logged.

**M2 — Static-site explorer & dataset release.**
Goal: beneficiaries can actually browse and reuse it.
Exit criteria: SSG renders all entries into an accessible, searchable site (WCAG-AA aimed);
cross-link graph navigable; first versioned **CC-BY dataset** published with provenance; live URL.
Depends on M1 corpus and M0 schema.

**M3 — Safety-track hardening & power-tool expansion.**
Goal: prove the medium-risk pipeline at scale.
Exit criteria: safety-review checklist + reviewer onboarding documented; ≥ 5 medium-risk
(power-tool/injury-risk) entries shipped, each hazard-first and safety-reviewed; CI rule enforces
"medium-risk ⇒ safety section + recorded safety reviewer."

**M4 — Category expansion & adoption.**
Goal: breadth + confirmed real-world use.
Exit criteria: ≥ 15 additional entries spanning ≥ 2 new categories (garden/kitchen/textile/
digital); ≥ 1 partner adoption confirmed in writing with a use report; ≥ 1 documented external
reuse of the CC-BY dataset.

## Work breakdown

The itemized, schema-mapped backlog lives in **TASKS.md**. It is organized by the milestones above
(M0–M4), with a task table per milestone (ID, title, type, size, risk, deliverable, dependencies,
reviewer), acceptance criteria for the most important tasks, a per-milestone Definition of Done, a
backlog of sized-but-unscheduled work, and a complete example Task JSON for the first M0 task.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the schema, style/safety guides, release cadence, and the
  Definition of Shipped.
- **Editorial reviewers (rotation):** review entries for clarity, completeness, schema validity,
  citations, and original-media compliance. Author ≠ reviewer.
- **Safety reviewer(s):** competent in the relevant tool/area; mandatory gate for medium-risk
  entries. TO BE SECURED (may overlap with partner staff — e.g. a makerspace shop lead).
- **Steward (last-mile owner):** ensures published entries actually reach beneficiaries and that
  partner adoption/feedback is collected. TO BE SECURED.
- **Partner / requestor:** education/makerspace/library/vocational org. TO BE SECURED.
- **Expert reviewers (risk tiers):** on call if any entry escalates to high-stakes; not expected
  in normal flow, but the path exists.

## Dependencies & integrations

- **Elyos pieces:** Task JSON schema (`packages/schema`), CLI workspace-prep + PR flow (donated
  lane), governance/review process, the registry.
- **External tooling:** chosen SSG (Astro/Eleventy — TBD), AJV for validation, a diagram toolchain
  for original SVG/PNG artwork.
- **Datasets/sources:** authoritative public safety guidance (e.g. OSHA/HSE-style), manufacturer
  safety documentation, and established trade references — used for **verification and citation
  only**, never copied.
- **Partner dependency:** the Definition of Shipped's adoption clause depends on securing a
  partner — a true external dependency, tracked as such.
- **Media dependency:** availability of an artist/diagram pipeline for original artwork is on the
  critical path for entries that need illustration.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Unsafe/incomplete technique in a medium-risk entry causes injury | Low | High | Mandatory safety reviewer for medium-risk; hazard-first format enforced as data + CI; defer high-stakes tasks to professionals | Safety reviewer |
| Media with unclear/incompatible license slips in | Medium | High | Original-art default; CI requires license field; human spot-check of any non-original asset; record provenance | Maintainer |
| No partner secured → Definition of Shipped not met | Medium | High | Start outreach in M0/M1; treat as tracked dependency; set `verifiedNeed=false` until confirmed | Steward |
| Inconsistent quality across many fan-out authors | Medium | Medium | Strict schema + style/safety guides + template; reviewer-not-author rule; CI lint | Maintainer |
| Scope creep into buying guides / model-specific repair | Medium | Medium | Explicit non-goals; review rejects out-of-scope entries | Maintainer |
| Refusal-worthy content requested (guard removal, weapons) | Low | High | Guardrail refusal + flag; documented in style/safety guide | All authors/reviewers |
| Maintainer bandwidth / bus factor | Medium | Medium | Document everything; reviewer rotation; small, forkable tasks | Maintainer |
| Accessibility shortfall in the site | Medium | Medium | WCAG-AA target; accessibility check in SSG task acceptance | Maintainer |

## Security & privacy

- **Threat surface is small:** a static site + structured data, no user accounts, no server-side
  state, no PII collection.
- **Secrets:** none required for the donated lane content work; any CI/deploy tokens live in CI
  secrets only and are never written into entries, logs, receipts, or commits (per Elyos rules).
- **PII:** none collected or stored; contributors credited by handle only.
- **Abuse/misuse prevention:** the primary misuse vector is the content itself being steered toward
  harm (defeating safety devices, illegal modification, weapons). This is mitigated by the refusal
  guardrails, the safety-review gate, and explicit non-goals — enforced at authoring and review
  time, not just by policy text.
- **Supply chain:** keep the SSG/toolchain dependency set minimal and pinned; static output reduces
  runtime attack surface.

## Sustainability & maintenance

- **After delivery:** the maintainer + reviewer rotation keep entries current (`lastReviewed`
  drives a re-review cadence; safety guidance is re-checked against sources periodically).
- **Outcome tracking:** the steward collects partner adoption and beneficiary-usefulness feedback
  (the real success metrics) and feeds it back into the backlog.
- **Low operating cost:** static hosting + a versioned dataset keeps running costs near zero,
  supporting longevity independent of any single funder.
- **Forkability:** CC-BY content + MIT code + open schema mean the work survives even if the
  original maintainers step away.

## Open questions

1. **Partner:** which education/makerspace/library/vocational org adopts the atlas first?
   (Blocks the Definition of Shipped.)
2. **SSG choice:** Astro vs Eleventy vs other — decide on accessibility, build simplicity, and
   maintenance burden.
3. **Authoring format:** structured JSON directly, or Markdown-with-front-matter compiled to JSON?
4. **Safety reviewer sourcing:** recruit independently or via the partner's shop staff?
5. **Where exactly is the medium/high line** for borderline entries (e.g. ladders, mains
   electrical) — needs a written rubric in the safety guide.
6. **Localization:** is multi-language a future phase, and does the schema need to anticipate it
   now?
7. **Contribution model:** if/when external contributions open, what review scaling is needed?

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — the 5 good-deed criteria + risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — Task JSON schema (TASKS.md maps to it).
- `C:\code\elyos\governance\proposals\tool-atlas.md` — the project proposal.
- Creative Commons Attribution 4.0 (CC-BY-4.0) — content license.
- MIT License — code license.
