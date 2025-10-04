# Assignment 2: Neural Network Verification for Adult Census Income Classification


## Assignment Overview

This is an **individual assignment**. You are permitted to use generative AI tools to help write your code. Please **acknowledge the use of AI** wherever applicable.

The Adult Census Income dataset is a structured tabular dataset derived from the 1994 U.S. Census. Each record consists of demographic and employment-related attributes (e.g., age, education, occupation, marital status, hours worked). The prediction task is binary classification: determine whether an individual earns more than $50,000 annually.

Smayan has trained nine feedforward neural networks, each with fully connected layers, ReLU activations in the hidden layers, and a sigmoid output for binary classification. These models were trained using the Adam optimizer with binary cross-entropy loss. The nine models differ in depth (4, 6, or 8 layers) and width (100, 200, or 300 neurons per layer).

## Assignment Parts

### Part I: Formal Specification

Write five formal specifications for the Adult Income classification task. Each specification must be precise, using logical notation. These can be fairness, robustness, or functional correctness specifications.

### Part II: Formal Verification

For each of your five specifications, verify whether the property holds for the given neural networks using Marabou (github.com/NeuralNetworkVerification/Marabou).

### Part III: Limitations

Analyze the limitations of the formal verification approach by changing the architecture (both depth and nodes/layer) as well as specifications.

## Contents

- Formal specifications for neural network properties
- Marabou verification scripts and results
- Analysis of verification limitations

## Setup

### Prerequisites
- Python environment with required packages
- Marabou neural network verifier
- Access to the trained neural network models

### Installation
1. Install Marabou from: https://github.com/NeuralNetworkVerification/Marabou
2. Set up Python environment with necessary dependencies
3. Download the trained neural network models

### Usage
- Run verification scripts using Marabou
- Analyze results and generate reports
