# tool-atlas

> An open, structured atlas of tools and how to use them safely.  ·  **Risk tier:** low-medium  ·  **Status:** proposed (planning)

A structured, openly-licensed reference atlas of tools — what each tool is, what it's for, when to
choose it, how to use it safely and well, common mistakes, and care/maintenance. Starts with hand
and household/workshop tools (and is extensible to garden, kitchen, textile, and digital/dev
tools). Each entry is original text + an openly-licensed or original diagram, machine-readable so
it can power apps, courses, and search.

**Definition of shipped:** A published atlas with peer-reviewed entries adopted by an education/makerspace partner; structured data under CC-BY.

This is an **Elyos** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Platform: https://github.com/jdev1977/elyos

## Planning
- [PROPOSAL.md](./PROPOSAL.md) — why this qualifies as a good deed (Good Deed Definition)
- [PLAN.md](./PLAN.md) — architecture, roadmap & milestones, risks
- [TASKS.md](./TASKS.md) — the full task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
elyos browse
elyos pull --task-file tasks/tool-atlas-schema-001.json --repo Elyos-Projects/tool-atlas
# do the work with your own agent, then:
elyos submit tool-atlas-schema-001 --repo Elyos-Projects/tool-atlas
```

## Licensing & review
- **Licensing:** Content + data: CC-BY-4.0. Tooling: MIT.
- **Review:** risk tier **low-medium** — deeds are *delivered, not merged*; a domain reviewer must sign off before merge.

> Status: this project is in **planning** and not yet ratified through Elyos governance; no adopting partner/requestor is secured yet (`verifiedNeed: false` on delivery-dependent tasks).
