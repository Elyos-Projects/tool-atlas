# Competitive & Improvement Analysis — `tool-atlas`

> Analyst note · Scope correction up front. The tasking brief described `tool-atlas` as "an open,
> structured catalog of **open-source software tools + open datasets** for social good." The actual
> `PLAN.md`, `TASKS.md`, and proposal describe something different: an openly-licensed **reference
> atlas of physical tools** (hammers, saws, drills, chisels — hand/household/workshop, extensible to
> garden/kitchen/textile/digital) teaching *what a tool is, when to use it, how to use it safely, and
> how to maintain it*, as **original CC-BY content with original diagrams**. This is a
> content/education project, not a links-catalog of software. This analysis is grounded in the **real
> plan**. Where the brief named software-catalog competitors (awesome-lists, DPG Registry, Civic Tech
> Field Guide, AlternativeTo, libraries.io, OpenSustain.tech), I cover them but mark them **off-category**
> and substitute the true competitor set (iFixit, wikiHow, Instructables, Appropedia, OER/SkillsCommons,
> tool libraries/makerspaces, OSHA). The brief↔plan mismatch is itself the #1 correctness finding (§1).

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature for a draft: closed-enum `riskTier` with gas/mains/structural
auto-escalation, a license **allow-list enforced in schema**, mandatory human source-URL verification,
reviewer-≠-author, a ≥2-citation floor, a 10% re-audit sample, an honest `verifiedNeed=false` until a
partner signs, and a fallback "delivered" definition if no partner lands. Genuine strengths. Findings,
roughly worst-first:

1. **Identity / scope-framing mismatch (highest-order).** The project's name ("tool-atlas") and the
   ecosystem it sits in (Elyos good-deed catalog, Digital Public Goods) strongly connote *software/data*
   tooling, yet the content is *physical* tools. This already caused a tasking miscommunication. **Risk:**
   discoverability and positioning confusion, duplicated effort, and partner/funder mis-set expectations.
   **Fix:** a one-line positioning statement in the README and dataset metadata ("an atlas of *physical*
   tools and how to use them safely"); reserve the software-catalog concept as a *separate* Elyos repo
   (see §7). Decide deliberately rather than by accident.

2. **Scope is potentially infinite and lacks an *inclusion/curation rubric* (only a quality floor).**
   The plan has an excellent **per-entry quality floor** (schema-valid + ≥2 citations + signed checklist
   + audit sample) but **no documented criteria for *which* tools earn an entry, in what priority order,
   or when the corpus is "complete enough."** "10 seed hand tools, then garden/kitchen/textile/digital as
   capacity allows" is an open-ended growth path with no demand signal, no prioritization metric (e.g.
   tool-library checkout frequency, makerspace curriculum coverage, beneficiary requests), and no stopping
   rule. Awesome-lists and wikis sprawl for exactly this reason. **Fix:** add an *inclusion rubric* to the
   style guide — ranked by (a) ubiquity/beginner-frequency, (b) injury-risk salience, (c) partner-curriculum
   need, (d) gap vs existing open coverage — and cap each phase to a bounded set.

3. **Currency / linkrot is under-specified — and manifests differently than for a software catalog.**
   Because content is *original*, tools don't "die" or 404 the way software listings do. But two real
   decay vectors exist and the plan only gestures at them:
   - **Cited-source rot.** Every entry carries `sources[]` and (for medium/high) must cite manufacturer or
     OSHA/HSE guidance. Those URLs rot and version-bump (e.g. OSHA Pub 3080 vs the newer 3950 — see §2).
     There is a `lint`/link-check task mentioned, but **no defined re-check cadence, no archival
     snapshotting (e.g. Wayback/`archived_url` field), and no "source superseded" workflow.**
   - **Guidance staleness.** Safety best practice, PPE norms, and standards evolve. The schema has
     `lastReviewed`, and sustainability text says it "drives a re-review cadence" — but **no interval is
     defined** (6mo? 12mo? risk-tier-dependent?). Without a number, `lastReviewed` is decorative.
   - **Fix:** add `sources[].archivedUrl` + retrieval-date (retrieval date already present), a CI link-checker
     with a quarterly schedule, a risk-tiered re-review SLA (e.g. medium/high ≤12mo, low ≤24mo), and a
     "stale entry" badge surfaced in the SSG.

4. **Neutrality / vendor-promotion — well handled, with two residual leaks.** Non-goals explicitly bar
   buying guides, prices, affiliate links, and brand/model recommendations — strong. Residual risks: (a)
   the `alternatives[]` and "when to choose it" fields can drift into implicit product steering; (b) citing
   *specific manufacturers'* safety docs (the recommended evidence base) can read as endorsement. **Fix:**
   style-guide rule that `alternatives[]` names *tool classes, not brands*, and that manufacturer citations
   are evidence, not endorsement (prefer vendor-neutral OSHA/HSE where equivalent).

5. **Metadata / standards reuse is thin.** The schema is bespoke. It does not reference external
   vocabularies (schema.org `HowTo`/`HowToTool`, Wikidata QIDs for tools, GS1/UNSPSC categories) that
   would make the dataset interoperable and the cross-link graph anchorable to stable identifiers. **Fix:**
   add optional `wikidataId` and emit `schema.org/HowTo` JSON-LD from the SSG for free SEO + machine reuse.

6. **Dedup vs existing open corpora is unaddressed.** The plan positions against "ad-laden SEO how-to
   sites" but never against the *open* incumbents it most overlaps — wikiHow, iFixit, Appropedia, OER. A
   reader could reasonably ask "why not contribute to wikiHow?" The answer exists (license + structure +
   safety-as-data; see §4) but isn't stated. **Fix:** a short "why a new corpus" section citing the
   license/structure gap.

7. **Licensing of the listing/dataset — strong and a genuine moat.** CC-BY-4.0 content + MIT code, with a
   schema-enforced media license allow-list and per-asset provenance, is *more* reusable than every major
   open competitor (all CC-BY-**NC-SA** or proprietary; §2). This is correct and should be marketed, not
   buried. One gap: the plan should state how it will keep *contributed* media CC-BY-clean at scale (the
   `sourceVerified` gate covers it for now, but contributor terms/DCO-for-content aren't defined).

8. **Sustainability of curation / bus factor.** Owner is **TBD (hard M0 gate, target 2026-07-12)**, safety
   reviewer **TBD**, steward **TBD**, partner **TBD**. The plan is honest about this, but *four* unfilled
   critical roles is the dominant project risk — more so than any technical item. The fallback-delivered
   definition (ship the dataset even without a partner) is a good de-risking move.

9. **Minor:** WCAG-AA is "aimed," not gated in M2 acceptance (it's in risks, not exit criteria); the
   beneficiary-survey instrument (`research-506`) is a hard prerequisite for the headline outcome metric but
   is *backlogged/unscheduled*; "≥ N entries/week (target ≥3)" leaves N undefined in the M3 SLA.

---

## 2. Competitive landscape (researched, cited)

### True competitors (open practical-skills / tool know-how)

| Project | What it is | Strengths | Weaknesses vs tool-atlas |
| --- | --- | --- | --- |
| **iFixit** ([licensing](https://www.ifixit.com/Info/Licensing)) | 100k+ wiki repair guides, 13,500+ device models | Huge scale, strong community, original media, real-world trust | **CC BY-NC-SA 3.0** → *noncommercial + sharealike*, blocks commercial course/app reuse; **device-repair** focus, not tool-use pedagogy; prose, not structured schema |
| **wikiHow** ([CC announcement](https://creativecommons.org/2007/10/02/wikihow-reaches-25000-articles/)) | Largest general how-to wiki | Enormous breadth, "right to fork," CC-licensed | **CC BY-NC-SA** (same NC/SA limits); uneven safety quality; UGC drift; unstructured; not tool-centric |
| **Instructables** ([ToS](https://www.autodesk.com/company/legal-notices-trademarks/terms-of-service-autodesk360-web-services/instructables-terms-of-service-june-5-2013)) | Autodesk-owned project/how-to platform | Large, vibrant maker community | **Proprietary platform**, per-user license grants to Autodesk; ad/subscription; project-oriented, no neutral tool reference; not openly remixable as a dataset |
| **Appropedia** ([CC wiki](https://wiki.creativecommons.org/wiki/Appropedia)) | Sustainability/appropriate-tech wiki, MediaWiki | Open, **CC-BY-SA-4.0**, thousands of pages, active editors | **ShareAlike** (copyleft, less remix-friendly than CC-BY); sustainability/dev focus, not consumer tool pedagogy; prose wiki, not schema'd |
| **OER Commons / SkillsCommons** ([OER Commons](https://oercommons.org/), [SkillsCommons](https://support.skillscommons.org/about/open-educational-resources/)) | 30k+ OER items; SkillsCommons = CC-BY workforce-training OER | **CC-BY-4.0** (truly remixable), education-grade, vocational alignment | Aggregators of heterogeneous resources, not a *curated, uniform, structured tool atlas*; quality/format varies wildly per contributor |
| **OSHA Hand & Power Tools** ([Pub 3080](https://www.osha.gov/sites/default/files/publications/OSHA3080.pdf), [Pub 3950](https://www.osha.gov/sites/default/files/publications/OSHA3950.pdf), [hub](https://www.osha.gov/hand-power-tools)) | Authoritative US safety guidance | **Public domain**, authoritative — ideal *source* to cite | A regulator's safety doc, not a beginner-friendly, structured, illustrated atlas; not a competitor so much as a primary citation (and one prone to version drift — note 3080 vs 3950) |
| **Tool libraries / Library of Things / makerspaces** ([Local Tools](https://localtools.org/find/), [Denver Tool Library](https://denvertoollibrary.org/), [Shareable toolkit](https://www.shareable.net/library-of-things-toolkit/)) | Physical lending + in-person classes | Direct beneficiary access, hands-on teaching, **the natural partner channel** | Local, in-person, not a reusable open reference; *complement, not competitor* — these are tool-atlas's adoption partners |

### Off-category (named in brief; apply to a *software* catalog, not this project)

| Project | Relevance |
| --- | --- |
| **DPG Registry / DPGA** ([standard](https://github.com/DPGAlliance/DPG-Standard), [registry](https://github.com/DPGAlliance/publicgoods-candidates)) | A registry of *digital* public goods (open software/data/AI/content) — 222 entries, 9-indicator standard. tool-atlas isn't a competitor, but its CC-BY corpus **could be submitted as a DPG** (open content collection). See §7. |
| **Civic Tech Field Guide** ([civictech.guide](https://civictech.guide/)) | Catalog of *civic-tech* tools/orgs — off-category, but a model for "open-data catalog of tools." |
| **awesome-lists** ([sindresorhus/awesome](https://github.com/sindresorhus/awesome), [awesome-civic-tech](https://github.com/awesomelistsio/awesome-civic-tech)) | Curated link lists of *software*. Relevant only as a structural anti-pattern: link-rot-prone, unstructured, no quality floor — exactly what tool-atlas's original-content + schema model avoids. |

**Takeaway:** Every open competitor is either (a) license-encumbered for commercial/course reuse
(NC and/or SA), (b) unstructured prose, or (c) an aggregator without a uniform quality/safety bar.
**No incumbent is simultaneously CC-BY, schema-structured, safety-gated, and curated.** That intersection
is the opening.

---

## 3. Gaps tool-atlas can fill

1. **A truly remixable (CC-BY, no NC/SA) tool corpus** — the only one; unlocks paid courses, apps, and
   commercial training that iFixit/wikiHow/Appropedia licenses forbid.
2. **Structured, machine-readable know-how** — competitors are prose; a validated schema lets the same
   content power a site, an app, search, an LLM tool, and an MCP server (§7) from one source.
3. **Safety as enforced data, not editorial hope** — `riskTier` + `leadWithSafety` + CI gate + expert
   sign-off gives consistent hazard-first treatment that UGC wikis can't guarantee.
4. **Provenance-clean media at scale** — schema-enforced license allow-list + human source-URL verification
   beats the "found on the web" image problem endemic to how-to sites.
5. **Curated uniformity** — every entry hits the same floor, vs the quality variance of OER aggregators and
   open wikis.
6. **Beneficiary equity framing** — explicitly serves people *without* a mentor/shop class; tied to tool
   libraries and CTE programs as a delivery channel rather than ad traffic.

---

## 4. Differentiators to win

The honest, defensible pitch (vs the *real* incumbents):

1. **License moat — CC-BY-4.0 + MIT.** Researched and confirmed: iFixit and wikiHow are **CC BY-NC-SA**
   ([iFixit](https://www.ifixit.com/Info/Licensing); [wikiHow](https://creativecommons.org/2007/10/02/wikihow-reaches-25000-articles/)),
   Appropedia is **CC-BY-SA** ([CC](https://wiki.creativecommons.org/wiki/Appropedia)), Instructables is
   **proprietary**. tool-atlas is the *only* one a vocational program can legally fold into a paid course or
   an app maker can ship commercially. **Lead with this.**
2. **Structured > prose.** A schema'd corpus is a product surface (site + dataset + API + MCP) others can't
   match without re-authoring. Emit `schema.org/HowTo` JSON-LD for free interoperability.
3. **Safety-gated by design.** Enforced hazard-first + competent-reviewer sign-off + gas/mains/structural
   auto-escalation — a credibility and liability differentiator no UGC wiki can claim.
4. **Curation floor + reviewer-≠-author** — consistent quality across high fan-out, the opposite of
   awesome-list/wiki drift.
5. **Provenance-auditable** — every media asset and claim is traceable, making the dataset trustworthy for
   institutions (and DPG-eligible).

Against the *brief's* named set (DPG Registry, Civic Tech Field Guide): tool-atlas doesn't compete — it
*qualifies as a candidate entry* in those registries (open content collection), turning would-be
competitors into distribution channels.

---

## 5. Claude API leverage — and the hard limits

**Where Claude adds real leverage (donated-lane authoring + maintenance):**
- **Schema-conformant draft authoring** — generate entry scaffolds (purpose, when-to-use, technique steps,
  common mistakes, care) in the exact JSON shape, ready for human review (the bounded "one tool = one task"
  design is tailor-made for this).
- **Metadata extraction & normalization** — derive aliases, category/subcategory, and `relatedTools` edges;
  build the **cross-link graph** and glossary consistently across hundreds of entries.
- **Currency / linkrot triage** — fetch and check every `sources[].url`, flag dead/redirected links, detect
  **superseded source versions** (e.g. OSHA 3080→3950), and propose `archivedUrl` snapshots for human
  confirmation.
- **Consistency / style linting at fan-out** — enforce the style guide, reading level, and hazard-first
  ordering across many authors; flag drift for the 10% audit.
- **Categorization & dedup** — cluster proposed entries, detect near-duplicates, and map to Wikidata QIDs /
  schema.org types for the interoperability layer (§1.5).
- **Accessibility & localization scaffolding** — draft image alt-text and translation stubs (human-verified).

**Where Claude must NOT be the decider (hard human gates):**
- **Safety-technique correctness and risk-tier classification** — a *competent human safety reviewer* signs
  off medium/high entries; an LLM must never set or downgrade `riskTier` or approve PPE/technique.
- **Media license verification** — `sourceVerified:true` requires a *human* checking the source URL; no
  model assertion substitutes (license hallucination is a real, citable failure mode).
- **No fabricated tools, sources, or citations** — every cited source must be a real, retrievable document a
  human confirmed; the ≥2-citation floor is meaningless if citations are invented.
- **Curation/inclusion judgment** — *which* tools belong, and whether an entry meets the quality bar, is a
  maintainer call, not a generation call.
- **Neutrality calls** — whether phrasing crosses into vendor endorsement is human-judged.
- **Partner fitness / beneficiary usefulness** — outcome truth comes from the partner survey, not the model.

The plan's existing gates already encode most of this; the addition is to **write it into the agent
instructions** so donated-lane sessions know the bright lines before authoring.

---

## 6. Ten concrete optimizations

1. **Add an inclusion/curation rubric** (ranked: ubiquity, injury-risk, partner-curriculum need, open-coverage
   gap) and a per-phase entry cap — closes the infinite-scope gap (§1.2).
2. **Define a re-review cadence number** (e.g. medium/high ≤12mo, low ≤24mo) so `lastReviewed` is enforceable,
   plus a CI **quarterly link-checker** and a `sources[].archivedUrl` field for linkrot resilience (§1.3).
3. **Emit `schema.org/HowTo`/`HowToTool` JSON-LD** from the SSG and add optional `wikidataId` — free SEO,
   machine interoperability, stable cross-link anchors (§1.5).
4. **State the license moat everywhere** — README, dataset card, site footer: "CC-BY-4.0, commercial reuse
   permitted" — the single biggest differentiator vs NC/SA incumbents (§4.1).
5. **Style-guide neutrality rule:** `alternatives[]` names *tool classes not brands*; manufacturer cites are
   evidence not endorsement; prefer OSHA/HSE where equivalent (§1.4).
6. **Author a "datasheet for the atlas"** (provenance, license, coverage, review process, known gaps) shipped
   with each dataset release — ties to open-data-datasheets (§7) and makes it DPG-submittable.
7. **Pre-write the DPG Registry submission** as an M2/M4 task — converts a "competitor" registry into a
   distribution channel and a credibility signal (§7).
8. **Gate WCAG-AA in M2 exit criteria** (move it from "aimed"/risk into acceptance) and add an automated a11y
   check to the SSG task (§1.9).
9. **Schedule the beneficiary-survey instrument (`research-506`) into M1**, not the backlog — it's a hard
   prerequisite for the headline outcome metric (§1.9).
10. **Define a content-contribution provenance policy** (DCO-for-content / contributor license terms) now,
    before any external contribution opens, to keep the CC-BY corpus clean at scale (§1.7).

---

## 7. Parallel & perpendicular spin-offs

- **MCP server over the corpus** *(highest leverage)*. Because the atlas is schema'd CC-BY data, expose it as
  a Model Context Protocol server: any agent can answer "how do I use a chisel safely / what PPE for a
  grinder" from a provenance-backed, safety-reviewed source. One corpus → site + dataset + API + agent tool.
  Differentiator no prose wiki can replicate.
- **Structured tool registry / canonical IDs.** The `id` + alias + Wikidata layer can become a small
  *canonical identifier service* for physical tools (an "OpenAlex for hand tools"), which other Elyos
  repos and external apps reference.
- **open-data-datasheets (parallel).** The per-dataset "datasheet for the atlas" (§6.6) generalizes into a
  reusable Elyos pattern — datasheets-for-datasets applied to every Elyos corpus.
- **citizen-science-pipelines (perpendicular).** Crowd-sourced, provenance-verified tool photos/diagrams and
  field-tested technique feedback could feed the media pipeline (with the same human source-URL gate).
- **Shared Elyos good-deed-catalog infrastructure.** The schema-validation-in-CI, license allow-list,
  provenance block, safety/risk-tier gate, and reviewer-≠-author workflow are **reusable primitives** for
  *every* Elyos content project — extract them into shared tooling rather than re-implementing per repo.
- **Digital Public Goods candidacy.** Submit the CC-BY dataset + open schema + code to the
  [DPG Registry](https://github.com/DPGAlliance/publicgoods-candidates) — it plausibly meets the 9-indicator
  [DPG Standard](https://github.com/DPGAlliance/DPG-Standard) as an open content collection, yielding
  visibility and SDG alignment.
- **A *separate* software-for-social-good atlas.** The brief's mis-framing points to a real, distinct
  opportunity: a sibling Elyos repo that *is* a curated, CC-BY, schema'd catalog of open-source tools +
  open datasets for public-interest work (the niche DPG Registry, Civic Tech Field Guide, and awesome-lists
  only partially fill). Same engine, different corpus — but explicitly *not* this project.

---

## 8. Open questions

1. **Identity:** Should "tool-atlas" be renamed/repositioned to avoid the software-catalog confusion, and is
   the sibling software atlas (§7) a real Elyos backlog item?
2. **Inclusion rubric:** what is the demand signal that admits a tool and orders the long tail (tool-library
   checkout data? partner curricula? beneficiary requests)?
3. **Re-review cadence + linkrot:** concrete intervals and archival mechanism — what numbers, and who runs
   the quarterly link-check?
4. **Interoperability:** adopt schema.org `HowTo` + Wikidata IDs now, or defer? (Cheap now, expensive to
   retrofit.)
5. **Critical roles:** the four TBD roles (Owner, safety reviewer, steward, partner) — which is the binding
   constraint, and what's the recruiting plan if M0's 2026-07-12 owner deadline slips?
6. **Partner channel:** are tool libraries / makerspaces (the natural fit) being approached as *adoption
   partners* and as *safety-reviewer sources* simultaneously (the plan flags a CoI rule — good)?
7. **Contribution scaling:** when UGC opens, what content-provenance/DCO model keeps CC-BY clean?
8. **DPG submission:** submit at M2 (dataset) or wait for M4 (site + adoption)?

---

### Sources
- iFixit licensing (CC BY-NC-SA): https://www.ifixit.com/Info/Licensing
- wikiHow CC BY-NC-SA: https://creativecommons.org/2007/10/02/wikihow-reaches-25000-articles/
- Instructables ToS (Autodesk, proprietary): https://www.autodesk.com/company/legal-notices-trademarks/terms-of-service-autodesk360-web-services/instructables-terms-of-service-june-5-2013
- Appropedia CC-BY-SA: https://wiki.creativecommons.org/wiki/Appropedia
- OER Commons: https://oercommons.org/ · SkillsCommons (CC-BY): https://support.skillscommons.org/about/open-educational-resources/
- OSHA Pub 3080 / 3950 (public domain): https://www.osha.gov/sites/default/files/publications/OSHA3080.pdf · https://www.osha.gov/sites/default/files/publications/OSHA3950.pdf · https://www.osha.gov/hand-power-tools
- Tool libraries / Library of Things: https://localtools.org/find/ · https://denvertoollibrary.org/ · https://www.shareable.net/library-of-things-toolkit/
- DPG Standard / Registry: https://github.com/DPGAlliance/DPG-Standard · https://github.com/DPGAlliance/publicgoods-candidates
- Civic Tech Field Guide: https://civictech.guide/
- awesome-lists: https://github.com/sindresorhus/awesome · https://github.com/awesomelistsio/awesome-civic-tech
