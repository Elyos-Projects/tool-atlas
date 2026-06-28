# Proposal: tool-atlas (an open atlas of tools and how to use them)

**Proposer:** jdev1977 (drafted by Claude Code)
**Date:** 2026-06-28
**Domain(s):** education, practical-skills, open-reference, accessibility
**Lane:** donated
**Requestor / beneficiary:** learners without access to a mentor/shop class; makerspaces, schools, vocational programs  ·  **Verified need:** yes (practical know-how is unevenly distributed)

## Summary
A structured, openly-licensed reference atlas of tools — what each tool is, what it's for, when to
choose it, how to use it safely and well, common mistakes, and care/maintenance. Starts with hand
and household/workshop tools (and is extensible to garden, kitchen, textile, and digital/dev
tools). Each entry is original text + an openly-licensed or original diagram, machine-readable so
it can power apps, courses, and search.

## Why it qualifies as a good deed
- **Tangible public benefit:** democratizes the practical knowledge usually passed person-to-person.
- **Freely available:** CC-BY content; structured data (JSON/Markdown) anyone can build on.
- **Not primarily for-profit:** an open alternative to ad-laden, SEO-spam how-to sites.
- **No harm/misinformation:** safety-reviewed; technique verified against authoritative sources.
- **Executable by AI sessions:** one tool = one self-contained entry; near-unlimited fan-out.

## Scope / first tasks
- (small) Entry schema (name, category, purpose, when-to-use, technique steps, safety, care, related
  tools, media, sources) + a style/safety guide.
- (medium) 10 seed entries for the most common hand tools (hammer, screwdriver set, tape measure,
  hand saw, level, utility knife, pliers, wrench, drill, chisel).
- (small) Glossary + cross-link graph between related tools and tasks.
- (medium) Static site generator that renders the structured entries into a browsable atlas.

## Definition of shipped
A published, browsable atlas with a growing, peer-reviewed set of entries adopted by at least one
education/makerspace partner, with downloadable structured data under CC-BY.

## Risks / review needs
**Risk tier: low → medium for power tools and anything with injury risk** (saws, grinders,
electrical, ladders) — those entries require a safety reviewer and must lead with hazards/PPE.
**License gate:** original or openly-licensed media only; record provenance. No content that
encourages unsafe or illegal modification (e.g., disabling tool safety guards, weapons fabrication).
