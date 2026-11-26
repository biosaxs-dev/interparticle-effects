# interparticle-effects

Research repository investigating concentration-dependent interparticle scattering in SEC-SAXS data,
and its correction: the **soft-bounded LRF** (called "Bounded Structure Factorization, BSF" in the first drafts).

---

## What this repository is about

In SEC-SAXS, samples are typically dilute enough that interparticle effects are negligible.
However, near the peak of the elution profile, local concentration can be high enough
that the measured scattering intensity contains a contribution from the **structure factor** S(q,c):

$$I(q, c) = c \cdot P(q) \cdot S(q, c) \approx c \cdot A(q) + c^2 \cdot B(q)$$

where:
- $A(q) = P(q)$ — the true form factor (what we want)
- $B(q) = P(q) \cdot S_1(q)$ — the interparticle correction term
- $S_1(q) = S(q,c)/c$ — first-order structure factor coefficient

The **soft-bounded LRF** separates $A(q)$ from $B(q)$ using a rank-2
decomposition $M = PC$ with $C = [c;\; c^2]$, and weights the ratio $B/A$ per $q$ by
$\tau^2/(\tau^2 + s_r^2)$, where $\tau(q) = K\min\{1, 3L/(q\sigma)^2\}$ is a bound that a **hard core** gives at every $q$
(whatever the soft part of the interaction and the particle shape) and $s_r$ is the error of $B/A$: the plain quadratic
correction where the data are sharp (low $q$), no correction where they are not (high $q$), a smooth transition between.
The earlier hard clip of $B(q)$ at the hard-sphere envelope (the "Bounded LRF", `BoundedLrf.py`) is the hard-threshold form of the same bound.

> **Where the work is now (2026-11-26).** The simulations, the real-data runs, the robustness studies and the notebooks are in
> `molass-researcher/experiments/64_interparticle_methods`, `65_interparticle_decision` and `66_interaction_models`; the paper is
> `molass-papers/interparticle/` (outline, claims ledger and evidence map in `OUTLINE.md`); the method is in `molass-library`
> (`molass/LowRank/SoftBoundedLrf.py`, `decomposition.set_rank2_method('soft_bounded')`, unreleased). The notebooks in `explorations/` are the
> origin of the idea. Withdrawn: "the Bounded LRF is best" and a fitted hard-sphere structure-factor model as a recommended guard
> (experiments 64-66).

---

## Relationship to other repositories

| Repository | Role |
|------------|------|
| `molass-library` | Implementation: `molass/LowRank/SoftBoundedLrf.py` (soft-bounded LRF), `molass/LowRank/BoundedLrf.py` (hard clip), `docs/BOUNDED_LRF_PLAN.md` |
| `molass-researcher` | Simulations and real-data runs: experiments 64-66 |
| `modeling-vs-model_free` | Foundational notebooks: `interparticle_quadratic_verification.ipynb`, `bounded_structure_factorization.ipynb` |
| `molass-papers/interparticle/` | Paper (b): "A bound, not a shape: correcting interparticle effects in SEC-SAXS with a concentration-squared term" (first title: "Bounded Structure Factorization") |

---

## Repository structure

```
interparticle-effects/
├── .github/
│   └── copilot-instructions.md  ← AI context (this ecosystem)
├── README.md                    ← this file
└── explorations/                ← research notebooks
```

---

## Key references

- Foundational theory: `modeling-vs-model_free/explorations/bounded_structure_factorization.ipynb`
- Prerequisite verification: `modeling-vs-model_free/explorations/interparticle_quadratic_verification.ipynb`
- Implementation plan: `molass-library/docs/BOUNDED_LRF_PLAN.md` (original hard-clip plan, with a status note)
- Library implementation: `molass-library/molass/LowRank/SoftBoundedLrf.py` (soft-bounded LRF) and `BoundedLrf.py` (hard clip)
- Evidence and paper: `molass-researcher/experiments/66_interaction_models/README.md`, `molass-papers/interparticle/OUTLINE.md`
