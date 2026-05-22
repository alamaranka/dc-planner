# Decisions log

ADR-style: dated decisions, alternatives considered, rationale.

---

## 2026-05-22 — Scope: planning, not runtime scheduling

**Decision:** Build a planning-layer toolkit (strategic + tactical), not a runtime scheduler.

**Alternatives considered:**
- Runtime scheduler (Kubernetes plugin, Slurm extension)
- Hybrid (planner + thin runtime policy)

**Rationale:**
- Runtime scheduling space is crowded (GREEN, Themis, Gavel, K8s carbon-aware projects).
- Planning is OR-flavored (stochastic IP, decomposition) and less crowded.
- Directly aligns with OR-infra job postings (e.g., OpenAI Compute Optimization).
- Audience for planning lives in Python/Excel, not K8s internals.

**Consequences:** No runtime integration. Output is decisions/recommendations consumed by humans or downstream schedulers.