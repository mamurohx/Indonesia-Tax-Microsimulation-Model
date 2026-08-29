# Indonesia Tax Microsimulation Model

This repository contains a Python-based personal income tax microsimulation model for Indonesia. I developed the Indonesia-specific part of the model in 2024 during my Master of International Development Policy studies at Duke University.

The model is based on a tax microsimulation training framework used by the World Bank Revenue Academy. I adapted the PIT component to Indonesian tax rules and administrative tax data.

## What the model covers

The current Indonesia configuration covers Personal Income Tax (PIT). It calculates ordinary PIT and several types of income subject to final tax, and can be used to compare a baseline tax system with a reform scenario.

The model has been tested locally for simulation years 2021–2027.

CIT, VAT/GST, behavioral elasticity, and tax-incentive modules are not active in the Indonesia configuration. Some files related to those modules remain in the repository because the original backend still expects parts of the multi-country framework to be present.

## Indonesia-specific work

My work on the Indonesia model included coding Indonesian PIT rules, defining the variables used by the model, preparing administrative tax data, calibrating sample weights, setting growth assumptions, and preparing reform scenarios.

The main Indonesia-specific files are:

```text
taxcalc/
├── current_law_policy_pit_indo.json
├── function_names_pit_indo.json
├── functions_pit_indo.py
├── functions_pit_indo_marginal.py
├── pit_distribution_indo.json
├── records_variables_pit_indo.json
└── growfactors_pit_indo.csv
