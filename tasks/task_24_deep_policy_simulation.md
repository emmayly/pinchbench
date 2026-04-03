---
id: task_24_deep_policy_simulation
name: Deep Policy Simulation: Carbon Leakage & CBAM Effectiveness (Long)
category: research_and_simulation
grading_type: llm_judge
timeout_seconds: 2400
workspace_files:
  - path: "data_sources.json"
    content: |
      {
        "notes": "Fill this file with the URLs / citations you used, and any assumptions if sources were unavailable.",
        "sources": []
      }
  - path: "model_sim.py"
    content: |
      # Starter file (you may replace entirely).
      # Goal: implement a simple quantitative model + scenario simulation for carbon leakage and a border carbon adjustment.
      if __name__ == "__main__":
          print("TODO: implement simulation")
---

## Prompt

Act as a **Senior Quantitative Economist**. You must produce a research-style manuscript that combines:
1) a formal model (with equations), and  
2) a reproducible **Python calibration + simulation**.

This is an **iterative workflow** task intended to take ~30–40 minutes.

### Deliverables (must create all)
- `papers_review.md` — structured review of recent literature
- `paper.md` — full manuscript draft
- `model_sim.py` — runnable simulation script
- `results.csv` — scenario outputs produced by running `model_sim.py`
- `calibration_log.txt` — your calibration choices, parameter sources, and sensitivity notes
- Update `data_sources.json` with citations/URLs and notes on any approximations

---

## Phase 1 (Literature Synthesis, ~0–10 min)

Using browsing/search tools if available, identify and review **12–15 sources (prefer 2022–2026)** on:
- EU **CBAM/CBAM rollout** and expected impacts (policy + economic analysis)
- **carbon leakage** measurement / modeling (trade + emissions)
- comparisons of **EU vs UK** approaches (CBAM, ETS linkage, implicit carbon pricing, or alternative border measures)
- welfare/incidence and competitiveness impacts of carbon pricing + border measures

In `papers_review.md`, create a table with rows = papers and columns:
- Citation
- Research question
- Method (theory / empirical / CGE / IO / reduced-form)
- Data (if empirical) or calibration targets (if model-based)
- Key quantitative takeaway (1–2 bullets)
- Limitations
- **Agreement/Conflict**: what it aligns with or contradicts in other papers

If browsing is limited, use best-effort citations and clearly label them as “memory-based” in `data_sources.json`.

---

## Phase 2 (Model + Calibration + Baseline Simulation, ~10–22 min)

### 2.1 Formal model (include equations in `paper.md`)
Build a **two-region (Home H / Foreign F), two-good (Dirty D / Clean C)** model with trade.
Minimum required components:

- Preferences: CES over composites or Armington demand
- Production: sectoral production with emissions in Dirty sector
- Emissions:  
  - \(E_r = \gamma_r \cdot y_{D,r}\)
- Policy instruments:
  - carbon tax in Home: \(\tau_H\) applied to embodied emissions
  - a border carbon adjustment (CBAM/BCA) on imports of Dirty goods (or embodied emissions) at rate \(b\)
  - an output or investment subsidy for Clean sector: \(\sigma_H\)

**Leakage must be endogenous**: Foreign Dirty output (hence \(E_F\)) responds to Home policy via trade substitution / price effects.

### 2.2 Implement `model_sim.py`
Write a script that:
1. Defines parameters (at minimum): trade elasticity \(\epsilon\), emissions intensity \(\gamma_H,\gamma_F\), policy rates \(\tau_H, b, \sigma_H\)  
2. Implements a transparent equilibrium or reduced-form mapping from policy → outcomes.  
   - Full CGE is not required; a disciplined partial equilibrium / Armington-based structure is acceptable if you define it clearly.
3. Simulates **4 scenarios**:
   - A: Tax only
   - B: Tax + BCA
   - C: Subsidy only
   - D: Hybrid (Tax + Subsidy + optional BCA; specify which)
4. Outputs `results.csv` with at least:
   - scenario_name
   - Home emissions \(E_H\)
   - Foreign emissions \(E_F\)
   - Global emissions \(E_H + E_F\)
   - Leakage rate (define it explicitly; e.g., \(\Delta E_F / -\Delta E_H\))
   - A welfare proxy for Home and Foreign (e.g., EV approximation, real income, or utility change)
   - Any fiscal revenue / subsidy cost metric

### 2.3 Calibration requirements
- Calibrate \(\epsilon\) and \(\gamma\) using **best-available references** (papers, reports, or commonly used ranges).
- If you cannot find a precise estimate, choose a plausible range and justify.
- Record:
  - parameter values,
  - source or rationale,
  - and alternative values used for sensitivity
in `calibration_log.txt` and `data_sources.json`.

---

## Phase 3 (Robustness / “Red-Team” Audit, ~22–32 min)

Perform a structured self-critique in `paper.md` and `calibration_log.txt`:

1. List **3 fragile assumptions** (e.g., perfect competition, pass-through, fixed technology, no firm relocation, static setting).
2. Run a **low trade response** variant (e.g., cut \(\epsilon\) by 50%).
3. Re-run the script and append results (either extend `results.csv` with variant rows or produce `results_robustness.csv`).
4. Explain how and why the effectiveness of BCA changes (mechanism-level explanation).

---

## Phase 4 (Final Manuscript Draft, ~32–40 min)

Write `paper.md` as a professional draft with:
- Title, Abstract
- 1. Introduction
- 2. Policy Context (EU CBAM, UK comparison)
- 3. Literature Synthesis (structured, references to your table)
- 4. Model (equations + definitions)
- 5. Calibration & Data (parameter choices + sources)
- 6. Results (must cite values from `results.csv`)
- 7. Welfare Decomposition (include at least one explicit decomposition equation)
- 8. Geopolitical / competitiveness implications of CBAM rollout
- 9. Limitations & ethics/distributional considerations
- References

Target length: **~3,000–6,000 words** (quality > exact word count).

---

## Constraints
- Do not claim to have accessed proprietary datasets unless you actually did.
- If browsing is restricted, explicitly note limitations and use bounded sensitivity ranges.
- Your simulation must be runnable and produce the CSV file(s).

---

## Grading (LLM Judge, 100%)
Score 0.0–1.0 based on:
- All deliverables exist and are internally consistent
- Literature table is detailed and cross-compares papers
- Model is coherent with explicit equations and endogenous leakage
- `model_sim.py` runs and produces `results.csv`
- Calibration is transparent and justified
- Robustness audit is performed and discussed
- `paper.md` references quantitative results from the simulation
- Overall clarity, rigor, and plausibility (no fabricated “we ran X dataset” claims)