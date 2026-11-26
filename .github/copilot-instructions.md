<!-- AI Context Standard v0.10.0 - Adopted: 2026-07-27 -->
# AI Assistant Initialization Guide — interparticle-effects

**Purpose**: Initialize AI context for working in this repository

---

## What this repository is about

`interparticle-effects` is a research repository investigating concentration-dependent
interparticle scattering in SEC-SAXS, and its correction: the **soft-bounded LRF**
(first drafted as "Bounded Structure Factorization, BSF").

**Core idea**: Near the peak of the elution profile, the measured intensity contains
a structure factor contribution $B(q)$ proportional to $c^2$. The method uses a rank-2
decomposition $M = PC$ with $C = [c;\; c^2]$ to separate the true form factor $A(q)$
from the interparticle term $B(q)$, and weights the ratio $B/A$ per $q$ by $\tau^2/(\tau^2 + s_r^2)$,
with $\tau(q) = K\min\{1, 3L/(q\sigma)^2\}$ the bound that a hard core gives at every $q$.
The simulations, real-data runs and notebooks of the current work are in `molass-researcher`
(experiments 64-66); the paper outline and claims ledger are in `molass-papers/interparticle/OUTLINE.md`.

**Target paper**: Paper (b) in `molass-papers/interparticle/` —
"A bound, not a shape: correcting interparticle effects in SEC-SAXS with a concentration-squared term"
(first title: "Bounded Structure Factorization — Resolving Interparticle Effects in SEC-SAXS")

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
- `molass/LowRank/SoftBoundedLrf.py` — `soft_bounded_lrf`, `apply_soft_bounded_lrf`, `estimate_envelope_K` (the method of the paper)
- `molass/LowRank/BoundedLrf.py` — `estimate_KL`, `coerce_bounds`, `apply_bounded_lrf` (the earlier hard clip)
- `docs/BOUNDED_LRF_PLAN.md` — architecture design and `get_xr_matrices()` integration (original plan, with a status note)

---

## Relationship to other repositories

| Repository | Role |
|------------|------|
| `molass-library` | Implementation (`SoftBoundedLrf.py`; the earlier hard clip in `BoundedLrf.py`, `docs/BOUNDED_LRF_PLAN.md`) |
| `modeling-vs-model_free` | Foundational theory notebooks (interparticle_quadratic_verification, bounded_structure_factorization) |
| `molass-researcher` | Simulations and real-data runs (experiments 64-66), frozen results and notebooks |
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
- Bound (hard core, at every $q$): $|B/A| \leq K\min\{1,\, 3L/(q\sigma)^2\}$ with $\sigma = 2R$; the earlier hard-sphere envelope $|B(q)| \leq A(q) / (c_1 \cdot (qLR)^2)$ is its large-$q$ form

---

## Terminal conventions (Windows PowerShell)

Read [TERMINAL_CONVENTIONS.md v0.1.0](https://github.com/freesemt/ai-context-standard/blob/main/TERMINAL_CONVENTIONS.md) before committing or pushing from a terminal, and whenever a `git` / `gh` command prints a red `NativeCommandError` (usually not a failure).

## Notebook workflow

Read [NOTEBOOK_CONVENTIONS.md v0.2.6](https://github.com/freesemt/ai-context-standard/blob/main/NOTEBOOK_CONVENTIONS.md) before working with any notebook in this repo.  
Kernel preference: global Python (`py`). Do not create venvs.

---

## Response language

**Response language**: English
