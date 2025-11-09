# HypoxiaPerformancePredictor

## Overview

**HypoxiaPerformancePredictor** is a machine learning model designed to predict the decline in maximal power output ($\Delta \text{POWER}_{\text{max}}$) in hypoxic conditions using physiological variables collected at sea level. The model was developed and validated on a dataset of human subjects exposed to hypobaric hypoxia, with the aim of identifying individuals at risk of performance deterioration.

## Motivation
In hypoxic environments, performance can vary significantly between individuals. Traditional models such as linear regression have demonstrated limited predictive power. This project explores the potential of more sophisticated machine learning methods—particularly wide neural networks—to improve prediction accuracy.

## Methods

### Outcome Variable
- **$\Delta \text{POWER}_{\text{max}}$**: Change in maximal power output between sea level (SL) and high altitude at 12 hours (HA12h).

### Feature Selection
- We applied **RMRM (Repeated Measure Regression Modeling)** to select 8 initial predictors at sea level:
  - VO₂/HRₘₐₓ
  - VE/VCO₂ₘₐₓ
  - $\text{RER}_{\text{max}}$
  - $\text{RR}_{\text{max}}$
  - PETCO₂ₘₐₓ
  - HR (resting)
  - METS (resting)
  - VE/VCO₂ₘₐₓ (resting)

- Using **Relief** for feature selection, the two most relevant predictors were:
  - VO₂/HRₘₐₓ
  - VE/VCO₂ₘₐₓ (resting)

### Model Architecture
- **Model Type**: Wide Neural Network
- **Hyperparameters**:
  - Fully Connected Layers: 1
  - First Layer Size: 50 neurons
  - Activation Function: ReLU
  - Iteration Limit: 1000
  - Regularization Strength (Lambda): 0.01
  - Data Standardization: No

### Validation Method
- **Leave-One-Subject-Out (LOSO)** cross-validation

## Results

| Metric | Value  |
|--------|--------|
| RMSE   | 4.94   |
| $R^2$  | 0.85   |
| MSE    | 24.41  |
| MAE    | 4.35   |

The wide neural network outperformed traditional regression methods, confirming the advantage of deep learning models in handling physiological complexity.

## Predictive Model: Wide Neural Network
This repository contains the trained regression model `trainedModel10_NeuralNetwork.mat`, exported from MATLAB's Regression Learner App.

## File
- `trainedModel10_NeuralNetwork.mat`: Contains the trained wide neural network model.

##  How to Use in MATLAB
To use this model to make predictions on a new data table `T` (same format as training data), follow these steps:

```matlab
% Load the model
load('trainedModel10_NeuralNetwork.mat');

% Predict
yfit = trainedModel10_NeuralNetwork.predictFcn(T);

 ```
### Applications
This model demonstrates potential for:
- Identifying at-risk individuals in high-altitude environments
- Personalized training and acclimatization strategies for athletes
- Enhancing performance monitoring in medical and occupational settings

### Authors
- Valeria Páez and Maria Rodriguez Fernandez from Institute for Biological and Medical Engineering, Schools of Engineering, Medicine and Biological Sciences, Pontificia Universidad Católica de Chile, Santiago, Chile.
- David Andrade from Centro de Investigación en Fisiología y Medicina de Altura, Biomedical Department, Faculty of Health Sciences, Universidad de Antofagasta, Antofagasta, Chile

### License
This project is open-source and available under the MIT License.

