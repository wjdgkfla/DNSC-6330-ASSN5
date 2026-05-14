# Adversarial ML Security Audit — Evasion, Poisoning & Membership Inference (DNSC 6330, Assignment 5)

Conducted an end-to-end adversarial ML security audit on a COMPAS recidivism classifier, testing vulnerability to evasion attacks, data poisoning, and membership inference — with analysis of disparate racial impact across all attack vectors.

**Skills:** Python · pandas · scikit-learn · Adversarial ML · PGD Evasion · Data Poisoning · Membership Inference · Privacy-Utility Tradeoff

---

## What This Project Demonstrates

- **Evasion testing (PGD):** Perturbation sweeps at epsilon = {0.25, 0.5, 1.0, 2.0} on LR and GBT; race-specific FPR and AIR impact measured
- **Poisoning attacks:** Targeted label-flip attacks on racial subgroups; AUC and AIR degradation plotted; stealth zones identified
- **Membership inference:** Shadow-model MI pipeline for LR/GBT; MI AUC vs. generalization gap; regularization as privacy-utility tradeoff
- **Fairness-security intersection:** All attack vectors analyzed for disparate racial impact — showing security failures compound existing fairness gaps

---

## Key Findings

- Evasion stress widens racial error rate disparities
- Label-flip poisoning moves AIR out of bounds while minimizing AUC drop (stealthy attack vector)
- Feature-drift checks remain low under label-only poisoning
- Higher model overfitting increases membership inference exposure

---

## Dataset

ProPublica COMPAS Recidivism — same pipeline as Assignments 3 & 4

---

## Notebook

`Assignment_5.ipynb`

```bash
pip install pandas numpy matplotlib scikit-learn scipy
jupyter notebook Assignment_5.ipynb
```
