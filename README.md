# Assignment 5 — ML Security and Abuse Pathways (DNSC 6330)

**Course:** DNSC 6330 Responsible Machine Learning  
**Type:** Individual Homework 05 (Applied)  
**Due:** April 30, 2026, 11:59 pm ET

This repository section contains the applied adversarial ML audit for Lecture 05, built on the same COMPAS modeling pipeline from Assignments 3 and 4.

---

## Dataset Source

ProPublica COMPAS two-year recidivism dataset:  
`https://raw.githubusercontent.com/propublica/compas-analysis/master/compas-scores-two-years.csv`

Filtered cohort and features follow the Assignment 3/4 preprocessing pipeline.

---

## How to Run

### Google Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/Assignment_5.ipynb)

### Local
```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
jupyter notebook Assignment_5.ipynb
```

---

## Notebook Parts (A–D)

- **Part A — PGD Evasion Audit:** Runs adversarial perturbations at `epsilon = {0.25, 0.5, 1.0, 2.0}` on LR and GBT, reports race-specific FPR and AIR, and identifies where AIR crosses below 0.80.
- **Part B — Poisoning Loop with Fairness Monitoring:** Runs targeted label-flip attacks (African-American and Caucasian variants), plots AUC and AIR degradation, and computes stealth zones where fairness degrades while AUC remains stable.
- **Part C — Membership Inference Depth:** Implements a shadow-model MI pipeline for LR/GBT, compares MI AUC with generalization gap, and evaluates LR regularization (`C`) as a privacy-utility tradeoff.
- **Part D — Reflection:** Summarizes the highest-risk finding, one proactive mitigation, one reactive mitigation, and potential disparate-impact side effects.

---

## Key Findings (populate with your run output)

- Evasion stress can widen race-conditioned error disparities as perturbation budget grows.
- Label-flip poisoning can move AIR outside governance bounds while top-line AUC drops minimally (stealth risk).
- Feature-PSI drift checks remain low under label-only poisoning, showing that covariate drift monitors alone are insufficient.
- Higher overfitting tends to increase MI exposure; stronger regularization can reduce MI risk but may trade off utility.

---

## Threat-Model Matrix (NIST AI 100-2 framing)

| Notebook Part | Attack Class | Stage | Typical Knowledge | Attacker Capability |
|---|---|---|---|---|
| Part A | Evasion (integrity) | Deployment-time | White/gray/black-box variants | Query model and perturb controllable numeric inputs |
| Part B | Data poisoning (integrity/availability) | Training-time | Insider or pipeline access | Relabel targeted records by subgroup |
| Part C | Membership inference (privacy) | Deployment-time | Black-box API access | Query confidence outputs and train shadow/meta models |
| Part D | Governance response | Ongoing monitoring | Risk office/model owner | Enforce controls and monitor fairness/security metrics |

---

## File Layout

```text
Responsible ML/
├── Assignment_3.ipynb
├── Assignment_4.ipynb
├── Assignment_5.ipynb
├── README.md
└── README_Assignment_5.md
```

---

## Responsible-Use Note

This work is for educational security auditing only. It should not be used to attack production systems. The COMPAS label (`two_year_recid`) measures re-arrest rather than true offending behavior and can encode historical enforcement bias. Any deployment decision requires legal, policy, and human-governance oversight.
