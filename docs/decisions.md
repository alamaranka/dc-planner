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

## 2026-05-22 — GPU type granularity

**Decision:** 4 buckets — heavy training, workhorse training, inference, legacy.

**Primary differentiator:** power draw and compute capability jointly; capex correlates strongly with both.

**Rationale:**
- Power drives carbon, the project's core objective.
- Compute class drives workload feasibility (a 70B model won't fit on T4).
- Capex amortized hourly enters the cost objective so the planner trades "buy more" vs "shift workloads" honestly.
- 4 buckets balances fidelity against MIP size; fewer collapses A100/H100 trade-offs, more outruns the data.

**Per-bucket parameters:** name, power_w, capex_eur, opex_eur_per_hour, memory_gb, compute_class.

**Open question:** Alibaba 2020 trace is V100/T4 heavy. For modern-fleet experiments, we'll calibrate buckets to public spec sheets (TDP, MSRP) and document the synthesis.