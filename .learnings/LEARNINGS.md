# Learnings

Corrections, insights, and knowledge gaps captured during development.

**Categories**: correction | insight | knowledge_gap | best_practice
**Areas**: frontend | backend | infra | tests | docs | config
**Statuses**: pending | in_progress | resolved | wont_fix | promoted | promoted_to_skill

---

## [LRN-20260511-001] correction

**Logged**: 2026-05-11T00:00:00+08:00
**Priority**: medium
**Status**: promoted
**Area**: infra

### Summary
Fork harness bootstrap must include graphify when the source project's workflow is `harness + ce + graphify`.

### Detail
The first Third-Person fork harness only added `harness + ce` docs and memory files, but omitted the repo-local graphify setup script, Git hooks, Codex hook installer, ignore rules, and `graphify-out` rebuild workflow.

### Resolution
Promoted the rule into `AGENTS.md` and `docs/harness/third-person-builder.md`: future harness work must include graphify automation unless the user explicitly asks for a lightweight harness.
