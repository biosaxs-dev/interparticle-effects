<!-- AI Context Standard v0.10.0 - Adopted: 2026-07-27 -->
# AI Assistant Initialization Guide — interparticle-effects

**Purpose**: Initialize AI context for working in this repository

---

## What this repository is about

`interparticle-effects` is a research repository investigating concentration-dependent
interparticle scattering in SEC-SAXS, and the **Bounded Structure Factorization (BSF)**
method for correcting it.

**Core idea**: Near the peak of the elution profile, the measured intensity contains
a structure factor contribution $B(q)$ proportional to $c^2$. BSF uses a rank-2
decomposition $M = PC$ with $C = [c;\; c^2]$ to separate the true form factor $A(q)$
from the interparticle term $B(q)$, then constrains $B(q)$ within a physics-motivated
envelope derived from the hard-sphere structure factor.

**Target paper**: Paper (b) in `molass-papers/interparticle/` —
"Bounded Structure Factorization — Resolving Interparticle Effects in SEC-SAXS"

---

## Key documents to read

1. **[README.md](README.md)** — Overview and repo relationships
2. **[explorations/](explorations/)** — Research notebooks (add as they are created)

**Foundational notebooks** (live in `modeling-vs-model_free`):
- `modeling-vs-model_free/explorations/interparticle_quadratic_verification.ipynb` —
  verifies that rank-2 $C=[c;\,c^2]$ separates $A(q)$ from $B(q)$
- `modeling-vs-model_free/explorations/bounded_structure_factorization.ipynb` —
  theory derivation, 4-strategy comparison (rank-1, full rank-2, synthesized LRF, bounded LRF),
  real data on SAMPLE3

**Implementation** (lives in `molass-library`):
- `molass/LowRank/BoundedLrf.py` — `estimate_KL`, `coerce_bounds`, `apply_bounded_lrf`
- `docs/BOUNDED_LRF_PLAN.md` — architecture design and `get_xr_matrices()` integration

---

## Relationship to other repositories

| Repository | Role |
|------------|------|
| `molass-library` | BSF implementation (`BoundedLrf.py`, `BoundedLrfPlan.md`) |
| `modeling-vs-model_free` | Foundational theory notebooks (interparticle_quadratic_verification, bounded_structure_factorization) |
| `molass-researcher` | Experimental data (real SEC-SAXS datasets for BSF testing) |
| `molass-papers/interparticle/` | Paper (b) draft text and figures |
| `molass-legacy` | Original implementation (`BoundedLRF/BoundedLrfSolver.py`, `Optimizer/StructureFactorBounds.py`) |

---

## Notation convention

Consistent with `modeling-vs-model_free`:

- $M = PC$ — data = spectral profiles × elution curves
- $A(q)$ — true form factor (monomer scattering profile)
- $B(q)$ — interparticle term ($= A(q) \cdot S_1(q)$)
- $S_1(q)$ — first-order structure factor coefficient
- $R = \sqrt{5/3} \cdot R_g$ — sphere-equivalent radius from Guinier $R_g$
- Envelope: $|B(q)| \leq A(q) / (c_1 \cdot (qLR)^2)$

---

## Notebook workflow

Read [NOTEBOOK_CONVENTIONS.md v0.2.6](https://github.com/freesemt/ai-context-standard/blob/main/NOTEBOOK_CONVENTIONS.md) before working with any notebook in this repo.  
Kernel preference: global Python (`py`). Do not create venvs.

---

## Response language

**Response language**: English
