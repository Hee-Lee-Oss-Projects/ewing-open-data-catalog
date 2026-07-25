# ewing-open-data-catalog

> Open, license-clear index + datasheets of open Ewing Sarcoma datasets. Open-access/aggregate/de-identified data only; controlled-access out of scope.  ·  **Risk tier:** med  ·  **Status:** planning

Open Ewing sarcoma datasets exist, but they are scattered across repositories (NCBI GEO, the GDC / TARGET open tier, UCSC Treehouse, cBioPortal, ICGC/ARGO), published under inconsistent and often unstated terms, and described unevenly. A researcher who wants to reuse open Ewing data cannot easily answer the three questions that actually gate reuse: **(1) is this access tier truly open (not controlled-access dbGaP/EGA)? (2) does the license permit derivative reuse and redistribution of *metadata*? (3) is there re-identification risk** — a real concern because Ewing is a rare pediatric/AYA cancer where small cohorts and genomic data raise privacy stakes. The result is wasted effort, accidental misuse of controlled data, and under-reuse of data that families and clinicians consented to share for research.

**Definition of shipped:** Published catalog + datasheets adopted/cited by a research/advocacy partner.

This is a **Hee-Lee Oss** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Get started: https://github.com/HeeLeeOss/hee-lee-oss-downloads

## Plan
- [PLAN.md](./PLAN.md) — robust enterprise plan (vision, architecture, roadmap, risks; includes an applied-improvements appendix + review sign-off)
- [TASKS.md](./TASKS.md) — schema-mapped task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
hee-lee-oss browse
hee-lee-oss next --repo HeeLeeOss/ewing-open-data-catalog --no-fork
```

## Licensing & review
- Docs CC-BY-4.0; code MIT. No patient data.
- Risk tier **med** — deeds are *delivered, not merged*; a domain reviewer (and expert sign-off for any high-stakes content) must approve before merge.

> Planning stage; no adopting partner secured yet (`verifiedNeed: false` on delivery-dependent tasks).
