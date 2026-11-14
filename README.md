# Equilibrium Analysis of PEN Toolbox and DNA Linkers with NUPACK

## Overview

These three Jupyter notebooks form a related set of NUPACK **test-tube analysis** examples for PEN toolbox DNA sequences and DNA linker systems. Given the specified temperature, salt conditions, and initial strand concentrations, they calculate equilibrium concentrations and base-pairing properties for selected complexes, then present the results in tables, CSV files, and plots.

NUPACK analyzes equilibrium properties over defined nucleic-acid ensembles using secondary-structure models. The `tube_analysis` jobs in these notebooks calculate equilibrium properties for specified test tubes, strand concentrations, and complex sets. The results are therefore **equilibrium predictions**; they do not directly simulate reaction rates or time-dependent behavior.

## Notebooks

| Notebook | Description |
|---|---|
| `nupack_analysis_pentoolbox.ipynb` | Analyzes several PEN toolbox reaction conditions (Reaction 1_1, 1_2, 2, and 3) using T1/T2/T3, alpha, beta, and Inh. It exports complex concentrations to CSV and plots the concentrations of selected abundant complexes. |
| `nupack_analysis_presentation.ipynb` | Adds P1/P2, Link1/Link2, and their templates to the PEN toolbox sequences. It analyzes a tube that includes complexes of up to four strands and plots equilibrium concentrations for two-strand complexes. |
| `nupack_analysis_oscillation.ipynb` | Compares three conditions using P1/P2 and Link1/Link2: all components, Linker1 only, and Linker2 only. It exports complex concentrations to CSV and plots selected results. Despite “oscillation” in the filename, the code contains no time steps or reaction-rate equations and does not simulate oscillation or time-dependent behavior. |

Together, the notebooks compare equilibrium complex formation across PEN toolbox reaction conditions and DNA systems with different linker combinations.

## Analysis conditions

Each notebook configures the NUPACK model as follows:

- Material: DNA (`material='dna'`)
- Temperature: 38.5 °C
- Sodium concentration: 0.050 M
- Magnesium concentration: 0.007 M
- Complex set: `SetSpec(max_size=2)` or `SetSpec(max_size=4)`
- Additional calculations: `compute=['mfe', 'pairs']`

The strand concentrations are defined in the notebooks. As the code comments indicate, these values should be adjusted to match the experimental conditions. Before interpreting results as representative of an experiment, check the values in each `concentration` dictionary, the temperature, ion conditions, and maximum complex size. For example, `max_size=4` includes complexes of up to four strands; larger complexes are excluded from that analysis set.

## Requirements

- Python and Jupyter Notebook
- The NUPACK Python module (the notebooks use `from nupack import *`)
- pandas (CSV export and tables)
- matplotlib (plots)

Set up an environment that can use the NUPACK Python module. Check the official NUPACK pages for current versions, terms of use, and installation instructions. Running NUPACK jobs may require an account and an active subscription.

## Running the notebooks

1. Start Jupyter in an environment where the NUPACK Python module, pandas, and matplotlib are available.
2. Open the notebook you want to run. Use the same environment for all three notebooks when comparing their results.
3. Review and, if needed, update the temperature, salt concentrations, and strand concentrations to match the experiment.
4. Run the cells from top to bottom.
5. Review the output tables and plots, along with the generated CSV files.

## Outputs

CSV files are written to the current working directory when the corresponding cells run.

- `nupack_analysis_pentoolbox.ipynb`: `1_2.csv`, `1_1.csv`, `2.csv`, and `3.csv`
- `nupack_analysis_presentation.ipynb`: no CSV export cell; plots are displayed in the notebook
- `nupack_analysis_oscillation.ipynb`: `gel_3.csv`, `gel_1.csv`, and `gel_2.csv`

The CSV files contain complex names and equilibrium concentrations in molar (M), sorted by concentration. The plots compare the equilibrium concentrations of selected complexes. Although `pairs` and `mfe` are requested as computed quantities, the notebooks do not export those results to CSV.

## Sequences and chemical modifications

Comments in the notebooks include chemical-modification notation used in PEN toolbox tables (for example, `*` and `3'P`). The sequence strings passed to NUPACK contain only A/C/G/T bases. As the notebook comments state, the modifications themselves are not represented in the input sequences. Their effects on binding or thermodynamic properties are therefore not automatically reflected in these calculations.

## Interpretation notes

- `tube_analysis` describes equilibrium concentrations and structural properties. Predicting reaction kinetics, enzyme-mediated reactions, or time-dependent oscillations requires a separate kinetic model or an appropriate reaction simulator.
- Test-tube analysis uses the strands, strand concentrations, and complex set specified in the notebook. Unspecified strands and complexes, including complexes larger than the selected `max_size`, are outside the analysis set.
- Concentrations and salt conditions affect the results. Compare the notebook values with the actual experimental conditions before using the results as experimental predictions.
- The sequence-based equilibrium analysis does not explicitly model chemical modifications, enzymes (such as nicking endonucleases), reaction rates, or fuel consumption in the PEN reaction mechanism.
- Results depend on the input sequences, physical model, concentrations, and `max_size` setting. Conclusions intended to describe an experiment require appropriate parameter settings and experimental validation.
