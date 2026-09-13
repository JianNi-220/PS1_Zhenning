# Intermediary Margin Rules, Farmer Earnings, and Product Access

Individual PS1 research proposal for COMSCI/ECON 206, Computational Microeconomics, Autumn 2026 Session 1. Author: Zhenning Wang. Instructor: Prof. Luyao Zhang.

This project asks how a platform's intermediary-margin rule changes farmer earnings and household product access in underserved markets. It compares a fixed margin with a margin chosen by the intermediary. The synthetic model links the rule to intermediary effort, retail price, completed purchases, farmer coordination costs, and farmer participation. Reputation enters as a demand multiplier so that later behavioral evidence can change the computational prediction.

The numerical results are synthetic illustrations. They are not estimates of real farmer income, household consumption, or rural inequality.

## Open the notebook

[Open the margin-rule notebook in Google Colab](https://colab.research.google.com/github/JianNi-220/PS1_Zhenning/blob/main/companion/notebooks/farmer_margin_rule_simulation.ipynb)

In Colab, choose **Runtime -> Restart session and run all**. No API key or private data are required.

## Reproduce locally

```bash
cd companion
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m unittest discover -s tests -v
python run_analysis.py
```

The last command recreates:

- `companion/outputs/baseline_results.csv`
- `companion/outputs/coordination_sensitivity.csv`
- `companion/outputs/coordination_sensitivity.png`

## Baseline model

Completed purchases are

`q(m,e,r) = 12 * r * e * max(0, 4 - m)`,

where `m` is the intermediary margin, `e` is effort, and `r` is a trust multiplier. Farmer and intermediary payoffs are

`pi_F = (w-c)q-K` and `pi_I = mq-30e^2`.

With `w=6`, `c=4`, `K=12`, and `r=1`, the fixed rule uses `m=1`; the chosen rule searches margins from 0 to 4 and effort from 0 to 1. The saved baseline gives:

| Rule | Margin | Effort | Completed purchases | Farmer net earnings | Intermediary profit |
|---|---:|---:|---:|---:|---:|
| Fixed | 1.00 | 0.60 | 21.60 | 31.20 | 10.80 |
| Chosen | 2.00 | 0.80 | 19.20 | 26.40 | 19.20 |

The comparison demonstrates a tradeoff in one calibration. Sensitivity analysis is necessary because the ranking can change with demand, trust, effort cost, and coordination cost.

## Repository map

- `main.tex`, `sections/`, `appendices/`, `references.bib`: ACM proposal source.
- `figures/`: editable Draw.io teaser and vector exports; these must match the farmer-margin proposal before submission.
- `companion/src/market_model.py`: reusable simulation functions.
- `companion/notebooks/farmer_margin_rule_simulation.ipynb`: Colab notebook.
- `companion/tests/`: checks for the reported baseline and model boundaries.
- `companion/outputs/`: saved outputs from a fresh local run.
- `companion/hf_space/`: placeholder for the matching Margin Rule Lab Space.

## Scope and reuse

The code and synthetic outputs are released for course research and education under the MIT License. The ACM class/style files and cited third-party materials retain their own terms. Do not treat the simulation as field evidence. Private peer-review reports and author responses should remain in the course-authorized review channel and should not be placed in this public repository.

## AI disclosure

OpenAI GPT-6 assisted with code drafting, debugging, documentation, and consistency checks on September 13, 2026 after the author selected the research question and supplied the course feedback. The author is responsible for checking every equation, output, citation, and claim.
