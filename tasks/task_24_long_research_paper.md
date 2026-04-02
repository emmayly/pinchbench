---
id: task_24_long_research_paper
name: Economics Research Paper on Carbon Policy with Formal Model (Long)
category: research
grading_type: llm_judge
timeout_seconds: 1800
workspace_files: []
---

## Prompt

Write a **research-grade economics paper draft** in the workspace on a specific topic, with explicit **models and formulas**.

### Topic
**Carbon pricing vs. green subsidies under leakage and border carbon adjustments (BCA): welfare, emissions, and competitiveness.**

Your goal is to produce a paper-like draft that could plausibly be developed into a publishable submission.

### What to do

#### 1) Pick and analyze 10 papers
Select **10 research papers** relevant to:
- carbon taxes / cap-and-trade,
- carbon leakage,
- border carbon adjustments,
- green industrial policy / subsidies,
- trade and environmental policy,
- general equilibrium or partial equilibrium modeling of climate policy.

For each paper extract, at minimum:
- research question
- modeling approach (e.g., partial equilibrium, Armington, Melitz, IAM, reduced-form empirical)
- key equations or identifying assumptions (if empirical)
- main result(s)
- limitations
- what it implies for your proposed contribution

Create `papers_review.md` with a **table** for all 10 papers.

#### 2) Propose a novel contribution
Propose a clearly novel angle. It must include:
- a gap in prior literature,
- your hypothesis,
- what is new (mechanism, welfare decomposition, identification strategy, or policy comparison),
- what data or calibrated parameters would be needed.

Create `idea_pitch.md` (max ~1 page) describing the contribution succinctly.

#### 3) Write the full paper draft
Create `paper.md` with the following required sections and minimum content:

**Title + Abstract**
- Abstract must state: question, method, contribution, and *expected* findings.

**1. Introduction**
- Define the policy problem (leakage, competitiveness, global emissions)
- State contributions as bullet points

**2. Institutional / Policy Background**
- Briefly explain carbon pricing, subsidies, and BCAs

**3. Related Work**
- Organize the 10 papers into themes and discuss them (not just a list)

**4. Model (must include equations)**
Provide at least one formal model with explicit notation and formulas. Minimum required components:
- Two regions: Home (H) and Foreign (F)
- Two sectors: Clean (C) and Dirty (D)
- Representative household utility and budget constraint, e.g.
  - \(U = \sum_{t=0}^{\infty} \beta^t u(c_t)\) (if dynamic) or static \(u(c)\)
- Firms with production functions, e.g.
  - \(y_{s,r} = A_{s,r} \cdot k_{s,r}^{\alpha} \ell_{s,r}^{1-\alpha}\)
- Emissions intensity for dirty sector \(e_{D,r}\), total emissions \(E_r = e_{D,r} \cdot y_{D,r}\)
- Policies:
  - Carbon price \(\tau_r\) applied to emissions
  - Green subsidy \(\sigma_r\) applied to clean output or investment
  - Border carbon adjustment rate \(b\) on imports of dirty goods (or embodied emissions)
- Trade structure (choose one and specify): Armington CES demand or iceberg trade costs
- Define equilibrium and market clearing conditions

**5. Welfare and decomposition (must include equations)**
Include at least one explicit welfare measure and a decomposition conceptually separating:
- domestic surplus/welfare change
- terms-of-trade effect
- leakage effect / foreign emissions response
- fiscal recycling (use of carbon revenue)

Example acceptable formalism:
- Equivalent variation (EV) or compensating variation (CV)
- Social welfare \(W_r = u(c_r) - \phi E_r\) with damage parameter \(\phi\)

**6. Identification / Empirical or Calibration Plan**
Even if you do not run it, you must specify:
- what data sources you would use (e.g., MRIO tables, UN Comtrade, energy/emissions inventories)
- what parameters get calibrated/estimated and how
- an estimation strategy or calibration targets

**7. Policy Experiments**
Define at least 4 counterfactuals to compare:
1) carbon price only
2) subsidy only
3) carbon price + BCA
4) subsidy + BCA (or hybrid)

Explain expected qualitative results and mechanisms.

**8. Robustness / Ablations**
Include an ablation plan (minimum 5 items), e.g.:
- varying trade elasticity
- varying emissions intensity
- alternative revenue recycling
- alternative BCA design (embodied vs sectoral)
- partial vs full pass-through

**9. Limitations**
Be explicit about what the model abstracts away from.

**10. Ethics & Distributional Considerations**
Discuss distributional impacts across regions/income groups and political economy constraints.

**References**
At least 10 references corresponding to the reviewed papers.

### Constraints
- Do **not** claim you ran regressions/simulations.
- Be very clear about what is proposed vs established.
- Use consistent math formatting (LaTeX in markdown is fine).

## Expected runtime
This is a long task and should plausibly take ~30 minutes for a strong agent.

## Grading (LLM Judge only, 100%)

Score from **0.0 to 1.0** based on:
- Completeness of deliverables (`paper.md`, `papers_review.md`, `idea_pitch.md`)
- Depth and correctness of economic reasoning
- Presence and coherence of formal model + welfare formulas
- Concrete empirical/calibration plan
- Novelty and clarity of proposed contribution
- Writing quality and internal consistency
- No false claims of completed experiments
