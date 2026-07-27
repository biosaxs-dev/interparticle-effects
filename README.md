# interparticle-effects

Research repository investigating concentration-dependent interparticle scattering in SEC-SAXS data,
and the **Bounded Structure Factorization (BSF)** method for correcting it.

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

**Bounded Structure Factorization (BSF)** separates $A(q)$ from $B(q)$ using a rank-2
decomposition $M = PC$ with $C = [c;\; c^2]$, then constrains $B(q)$ within a
physics-motivated envelope derived from the hard-sphere structure factor.

---

## Relationship to other repositories

| Repository | Role |
|------------|------|
| `molass-library` | Implementation: `molass/LowRank/BoundedLrf.py`, `docs/BOUNDED_LRF_PLAN.md` |
| `modeling-vs-model_free` | Foundational notebooks: `interparticle_quadratic_verification.ipynb`, `bounded_structure_factorization.ipynb` |
| `molass-papers/interparticle/` | Paper (b): "Bounded Structure Factorization — Resolving Interparticle Effects in SEC-SAXS" |

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
- Implementation plan: `molass-library/docs/BOUNDED_LRF_PLAN.md`
- Library implementation: `molass-library/molass/LowRank/BoundedLrf.py`
