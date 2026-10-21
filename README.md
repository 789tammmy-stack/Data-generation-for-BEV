# Synthetic Data Generation for Battery-Electric Underground Mining Truck Energy Prediction
## Overview
This project generates 50,000 synthetic samples for energy consumption in battery-electric haul trucks operating in underground mining environments. A physics-based model is used to calculate net battery energy for haul segments from selected vehicle, road, and operating parameters. The synthetic dataset supports machine-learning model development and evaluation. 

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

> Replace `data_generation.py` with the actual filename if it differs. Exact installation commands and output filenames depend on the files included in this repository.

## Suggested repository structure

├── data_generator.py
├── README.md
├── requirements.txt
└── data/
    └── data_generation.csv

This is a suggested structure; adjust it to match the actual repository contents.

## The script:
1. Loads the motor speed, torque, and efficiency maps.
2. Validates and preprocesses the motor efficiency map.
3. Builds a two-dimensional efficiency interpolator.
4. Calculates vehicle resistance forces.
5. Calculates wheel and motor operating conditions.
6. Estimates motor and battery electrical energy.
7. Generates a reproducible synthetic dataset.
8. Exports the dataset to a CSV file.

## Model assumptions
- The vehicle travels at constant speed over each segment.
- Rolling resistance, aerodynamic drag, and road grade are included.
- Motor efficiency is obtained from the supplied efficiency map.
- Negative tractive force is treated as regenerative braking.
- Acceleration, auxiliary loads, battery state of charge, and regenerative
  braking limits are not explicitly modelled.

## Units
Mass                  : kg
Velocity              : m/s
Distance              : m
Wheel diameter        : m
Motor torque          : N m
Motor speed           : rad/s internally
Slope                 : percent grade
Power                 : W
Energy                : kWh
Efficiency map        : percent (0-100)

## Intended use
The generated data can be used for:
- Training and evaluating machine-learning models for energy prediction
- Comparing modelling approaches under consistent synthetic conditions
- Investigating the effects of selected operating parameters
- Reproducible academic experimentation
