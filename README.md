# Running the γ-PGA modelling notebook

Everything needed is in this folder. **Keep the files together**: the notebook looks for
`iBB1018.xml` in the directory Jupyter is launched from.

## Install (once)

```bash
cd <this folder>
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

With Anaconda, `conda create -n pga python=3.11` followed by
`pip install -r requirements.txt` works just as well.

## Run

```bash
jupyter notebook iGEM_UdeS_gammaPGA_modelling.ipynb
```

Then *Kernel → Restart & Run All*. Allow about fifteen minutes: the notebook solves several
hundred FBA and FVA problems along the way.

As it runs it creates a `modeling_outputs/` folder and writes the 69 tables (CSV plus the
Escher JSON maps) that feed the Model page of the wiki. That is why they are not shipped
here — they are regenerated on every run.

## Contents

| File | What it is |
|---|---|
| `iGEM_UdeS_gammaPGA_modelling.ipynb` | the notebook, with every output from the last execution kept |
| `iBB1018.xml` | the genome-scale metabolic model of *B. subtilis*, the only external input |
| `requirements.txt` | the exact versions this was executed with (Python 3.11.15) |

## The four steps

| Step | What it does |
|---|---|
| **1. Model creation** | loads iBB1018, characterises it, then extends it with a γ-PGA synthesis and molecular-weight-control module, with the stoichiometry and mass balance verified |
| **2. Genetic engineering** | FBA / pFBA / FVA on the extended network; the four design iterations as a knockout screen, a capacity sweep and a molecular-weight dial |
| **3. Fermentation** | calibration on our own bioreactor growth curves, the five culture-medium iterations, the nitrogen and oxygen balances, and external validation against published fermentations the model was never fitted on |
| **4. Process** | the recovery handoff, the process train, the resource-constrained batch schedule and the decision-tool layer |

## Model source

`iBB1018.xml` comes from Blázquez, B. *et al.* (2023), *New Insights on Metabolic Features of
Bacillus subtilis Based on Multistrain Genome-Scale Metabolic Modeling*, International Journal
of Molecular Sciences 24(8):7091, https://doi.org/10.3390/ijms24087091 — open access under
CC BY 4.0. The notebook never modifies it on disk: it copies the model in memory and adds the
γ-PGA module to the copy.
