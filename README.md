# Synthetic Data Generation for Battery-Electric Underground Mining Truck Energy Prediction
## Overview
This project generates a synthetic dataset for studying energy consumption in battery-electric haul trucks operating in underground mining environments. A physics-based model is used to calculate net battery energy for haul segments from selected vehicle, road, and operating parameters. The synthetic dataset supports machine-learning model development and evaluation. 
Generates 50,000 synthetic samples for battery-electric underground mining truck energy prediction using a physics-based model. Uniform sampling covers key parameters, including vehicle mass, speed, road grade, haul distance, rolling resistance, and aerodynamic properties. The dataset supports machine learning model development and evaluation.

## Dataset
- **Number of samples:** 50,000
- **Sampling strategy:** Uniform sampling across predefined input ranges
- **Inputs:** 11 pre-departure features describing vehicle, road, and operating conditions
- **Target:** Predicted net battery energy for a haul segment

The generator varies parameters such as vehicle mass, speed, road grade, travel distance, rolling resistance, aerodynamic drag coefficient, frontal area, and drivetrain ratio within specified ranges.

## Methodology
1. Define physically motivated ranges for the input parameters.
2. Generate combinations of input variables using uniform sampling.
3. Calculate energy consumption using the physics-based model.
4. Assemble the input features and calculated energy target into a dataset.
5. Save the generated data for subsequent machine-learning experiments.

The model uses the road grade to determine the gravitational component of the forces acting on the truck. The grade percentage is converted to an angle using `atan(grade / 100)` when calculating the grade-related component.

## Scope and assumptions
- The data are **synthetic**, not directly measured mine-operation data.
- The model represents haul segments using a simplified quasi-static approach; acceleration effects within a segment are not explicitly modelled.
- The dataset is intended for methodological development and controlled model comparisons.
- Real-world generalisation should be assessed separately using suitable independent operational data.
- Results depend on the parameter ranges and physical assumptions configured in the generator.

## Getting started
1. Clone or download this repository.
2. Review the generator script and confirm the configured parameter ranges and units.
3. Install the Python libraries imported by the script.
4. Run the generator using the command appropriate to the script filename, for example:
   python data_generator.py
5. Check the output location and confirm the generated dataset's columns, units, and target definition.

> Replace `data_generator.py` with the actual filename if it differs. Exact installation commands and output filenames depend on the files included in this repository.

## Suggested repository structure

├── data_generator.py
├── README.md
├── requirements.txt
└── data/
    └── generated_dataset.csv

This is a suggested structure; adjust it to match the actual repository contents.

## Intended use
The generated data can be used for:
- Training and evaluating machine-learning models for energy prediction
- Comparing modelling approaches under consistent synthetic conditions
- Investigating the effects of selected operating parameters
- Reproducible academic experimentation

## Limitations
Because the dataset is generated from a simplified physics-based model, it reflects the assumptions built into that model. It does not automatically capture all real underground mining conditions, including site-specific road geometry, transient acceleration, battery ageing, state-of-charge effects, regenerative-braking limits, or ventilation airflow effects unless these are explicitly implemented. The generated data should therefore not be interpreted as measured field performance.
