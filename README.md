# Indonesia Tax Microsimulation Model

This repository contains a Python-based personal income tax microsimulation model for Indonesia. I developed the Indonesia-specific model in 2024 during my Master of International Development Policy studies at Duke University.

The starting point was a tax microsimulation training framework used by the World Bank Revenue Academy. I adapted its PIT component to Indonesian tax rules and to the structure of the administrative tax data I was working with.

For the Indonesia model, I coded the PIT rules and variable mappings, prepared the administrative data, calibrated the sample weights, and set the growth assumptions used in the simulations. I also added calculations for ordinary PIT and several categories of final income tax, and prepared reform scenarios for testing policy changes.

The model currently covers PIT only. CIT, VAT/GST, behavioral elasticity, and tax-incentive modules from the underlying framework are not active in the Indonesia configuration. Some supporting files for those modules remain because the older backend still expects parts of the original multi-country framework to be present.

I have tested the PIT model locally for simulation years 2021–2027. The taxpayer-level administrative data and calibrated working weights used in that testing are not included in this public repository.

## Key Indonesia files

The main Indonesia-specific tax model components are located in `taxcalc/`:

```text
taxcalc/
├── current_law_policy_pit_indo.json
├── function_names_pit_indo.json
├── functions_pit_indo.py
├── functions_pit_indo_marginal.py
├── pit_distribution_indo.json
├── records_variables_pit_indo.json
└── growfactors_pit_indo.csv
```

These files define the Indonesian PIT policy parameters, variable structure, tax calculation functions, marginal tax calculations, distributional analysis configuration, and growth assumptions used by the model.

## Testing the PIT model

I use `app2_gui2.py` as a lightweight simulation runner. It lets me check the PIT calculations without launching the full application, which is useful when working with the large administrative dataset.

To run it:

```bash
python app2_gui2.py
```

## Data needed to run the model

The model was developed using individual-level tax microdata and calibrated sample weights.

The underlying administrative microdata are **not included in this public repository**.

The local model expects the following files:

```text
taxcalc/pit_sample_2021_with_final_tax.csv
taxcalc/pit21_sample_2021_with_final_tax_weights_calibrated.csv
```

These files are explicitly excluded through `.gitignore`.

To use a different dataset, its variables need to be prepared and mapped consistently with the definitions in:

```text
taxcalc/records_variables_pit_indo.json
```

## Model Workflow

The simulation follows this sequence:

```text
Microdata
   ↓
Sample weights
   ↓
Growth factors
   ↓
Indonesia tax policy parameters
   ↓
PIT calculation functions
   ↓
Baseline / reform simulation
   ↓
Revenue and distributional outputs
```

## Policy Reform Simulation

I use JSON reform files to define alternative policy scenarios. For example, `reform.json` changes selected tax parameters so I can compare the reform results with the baseline.

## Upstream Framework and Attribution

The Indonesia model is based on a tax microsimulation training framework used by the World Bank Revenue Academy.

I retained parts of the original multi-country and multi-tax backend because some are still required by the framework even though the corresponding modules are not active in the Indonesia model. Files for other countries or tax types should therefore not be read as part of my Indonesia-specific implementation.

## Reproducibility and Confidentiality

The public repository includes the model code and tax-policy configuration, but not the taxpayer-level administrative data used in the original work.

The restricted microdata and calibrated working weights are excluded. The model configuration, growth factors, and variable definitions remain available so that the structure of the model can still be examined.

## Technical Notes

The code is based on an older version of the World Bank Revenue Academy tax microsimulation framework and includes some legacy dependencies. It runs with the required local inputs, although newer Python environments may produce deprecation warnings.

## Disclaimer

This repository is shared for academic, analytical, and portfolio purposes.

The model, assumptions, simulations, and outputs should not be interpreted as official estimates, statistics, or policy positions of the Directorate General of Taxes, the Ministry of Finance of Indonesia, Duke University, the World Bank, or any other institution.

The repository author is responsible only for errors in the Indonesia-specific implementation. Any interpretation, application, or use of the model and its outputs by third parties is their own responsibility.
