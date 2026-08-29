# Indonesia Tax Microsimulation Model

A Python-based personal income tax (PIT) microsimulation model for Indonesia, developed as an applied tax policy project during the Master of International Development Policy (MIDP) program at Duke University.

## Overview

This repository contains an Indonesia-specific adaptation of a tax microsimulation framework used for tax policy analysis.

The model translates Indonesian personal income tax rules into a computational framework that can be used to:

* reproduce a baseline personal income tax system;
* simulate alternative tax policy parameters;
* estimate changes in individual income tax liabilities;
* estimate selected final income taxes;
* project tax liabilities across simulation years; and
* support distributional and policy analysis.

The current Indonesia implementation focuses on **Personal Income Tax (PIT)**.

## Current Model Status

The following module is currently active:

* **Personal Income Tax (PIT): Active**

The following modules are retained in the underlying framework but are not currently implemented as part of the Indonesia model:

* Corporate Income Tax (CIT)
* VAT/GST
* Behavioral elasticity
* Tax incentive / tax expenditure analysis

Some legacy configuration and supporting files from the underlying framework are therefore intentionally retained because parts of the backend expect these dependencies to be available even when the corresponding modules are inactive.

## Indonesia-Specific Components

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

## Lightweight Simulation Test

`app2_gui2.py` is used as a lightweight simulation runner.

It allows the PIT model to be tested without launching the full microsimulation application, which is useful when working with large administrative microdata.

A local test of the reconstructed repository successfully ran the Indonesia PIT model for simulation years **2021 through 2027**.

To run the test:

```bash
python app2_gui2.py
```

## Data Requirements

The model was developed using individual-level tax microdata and calibrated sample weights.

The underlying administrative microdata are **not included in this public repository**.

The local model expects the following files:

```text
taxcalc/pit_sample_2021_with_final_tax.csv
taxcalc/pit21_sample_2021_with_final_tax_weights_calibrated.csv
```

These files are explicitly excluded through `.gitignore`.

Users wishing to adapt the model will need to provide input data with variables consistent with the definitions contained in:

```text
taxcalc/records_variables_pit_indo.json
```

A synthetic or public sample dataset may be added in a future version to demonstrate the complete workflow without using restricted administrative data.

## Model Workflow

At a high level, the simulation follows the following process:

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

The model can calculate ordinary personal income tax as well as several categories of income subject to final taxation.

## Policy Reform Simulation

Alternative policy scenarios can be specified through JSON reform files.

For example:

```text
reform.json
```

can be used to modify selected tax parameters and compare reform results with the baseline system.

## Repository Background

This project was developed as part of applied tax policy work during the MIDP program at Duke University.

The Indonesia model was built by adapting and extending an existing tax microsimulation training framework. The underlying framework contains components originally designed for multiple countries and tax types. This repository retains portions of that backend where they remain necessary for compatibility while separating the Indonesia-specific PIT configuration and calculation logic.

The objective of this repository is to document the Indonesia implementation, preserve a reproducible analytical workflow, and demonstrate the use of Python-based microsimulation for tax policy analysis.


## Upstream Framework and Attribution

This repository builds on a tax microsimulation training framework developed within the World Bank Revenue Academy ecosystem.

The Indonesia-specific implementation adapts and extends that framework with Indonesian PIT policy parameters, variable definitions, tax calculation functions, growth assumptions, data-preparation workflows, and simulation configuration.

Legacy multi-country and multi-tax components are retained where required for compatibility with the original backend. Their presence in this repository should not be interpreted as part of the Indonesia-specific implementation.

## Reproducibility and Confidentiality

The computational model and policy configuration can be shared publicly, but the administrative microdata used in the original analysis cannot be distributed through this repository.

For this reason:

* restricted microdata are excluded;
* calibrated weights derived for the working dataset are excluded;
* source code and policy configuration are retained; and
* data requirements are documented separately from the confidential input files.

This separation allows the analytical methodology to be documented without exposing taxpayer-level information.

## Technical Notes

The codebase is based on an older tax microsimulation framework and therefore includes some legacy dependencies and compatibility code.

The model currently runs with the required local inputs, although some dependencies may generate deprecation warnings in newer Python environments. Future repository cleanup may modernize these dependencies without changing the underlying tax calculation methodology.

## Disclaimer

This repository is shared for academic, analytical, and portfolio purposes.

The model, assumptions, simulations, and outputs should not be interpreted as official estimates, statistics, or policy positions of the Directorate General of Taxes, the Ministry of Finance of Indonesia, Duke University, the World Bank, or any other institution.

The repository author is responsible only for errors in the Indonesia-specific implementation. Any interpretation, application, or use of the model and its outputs by third parties is their own responsibility.
