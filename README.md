# Symbolic Logic and Applications: Verification of Neural Networks

**Due:** 28th October 2025  
**Points:** 100  

This is an individual assignment. You are permitted to use generative AI tools to help write your code.  
Please acknowledge the use of AI wherever applicable.

---

## Table of Contents
- [Dataset](#dataset)
- [Part I: Formal Specifications](#part-i-formal-specifications)
  - [1. Counterfactual Fairness (Race)](#1-counterfactual-fairness-race)
  - [2. Local Robustness at Class Means](#2-local-robustness-at-class-means)
- [Part II: Formal Verification with Marabou](#part-ii-formal-verification-with-marabou)
- [Part III: More Properties](#part-iii-more-properties)

---

## Dataset

The **Adult Census Income** dataset is a structured tabular dataset derived from the 1994 U.S. Census.  
Each record consists of demographic and employment-related attributes (e.g., age, education, occupation, marital status, hours worked).

The prediction task is **binary classification**: determine whether an individual earns more than **$50,000** annually.

Smayan has trained **nine feedforward neural networks**, each with:

- Fully connected layers  
- ReLU activations in hidden layers  
- A sigmoid output for binary classification  

The models were trained using the **Adam optimizer** with **binary cross-entropy loss**.

They differ in architecture by:

| Depth | Width (neurons per layer) |
|--------|----------------------------|
| 4      | 100, 200, 300              |
| 6      | 100, 200, 300              |
| 8      | 100, 200, 300              |

---

## Part I: Formal Specifications

Let:

- $f : X \to [0, 1]$ be the network score  
- $\hat{y}(x) = 1[f(x) \ge 0.5]$ be the predicted label  

Inputs $x$ are constrained by feature-wise bounds and one-hot constraints for categorical features.

---

### 1. Counterfactual Fairness (Race)

Let `race(x)` denote the race one-hot subvector of $x$, and let `RaceVals` be the set of valid race encodings.  
For any $x \in X$, define $x'$ to be $x$ with `race(x)` replaced (all other coordinates unchanged).  
The model is **fair at** $x$ iff:

$$
\forall \text{race}(x) \in \text{RaceVals} : \hat{y}(x) = \hat{y}(x')
$$

**Verification target:** Search for a violation — i.e., determine satisfiability (SAT) of:

$$
\exists x \in X, \exists \text{race}(x) \in \text{RaceVals} : \hat{y}(x) \ne \hat{y}(x')
$$

subject to input bounds and one-hot constraints.

---

### 2. Local Robustness at Class Means

For $y \in \{0, 1\}$, let $\mu_y$ be the mean input (in normalized feature space) over the subset with label $y$.  
Fix $\epsilon > 0$ and the norm $\|\cdot\|_\infty$.  

Define the admissible $\epsilon$-ball:

$$
B_\infty(\mu_y, \epsilon) = \{ x : \|x - \mu_y\|_\infty \le \epsilon, \text{ continuous features within bounds, categoricals remain valid one-hot} \}
$$

The model is **robust at** $\mu_y$ iff:

$$
\forall x \in B_\infty(\mu_y, \epsilon) : \hat{y}(x) = \hat{y}(\mu_y)
$$

---

## Part II: Formal Verification with Marabou

Use **[Marabou](https://github.com/NeuralNetworkVerification/Marabou)** to check both properties for each of the nine models.  
Explain and illustrate how different models perform differently for each verification task.

You may include:

- The verification query formulation  
- Screenshots or logs of Marabou outputs  
- Comparisons across different architectures  

---

## Part III: More Properties

Propose **three other verifiable properties**.  
For each property:

1. State it formally.  
2. Encode it in Marabou.  
3. Test it on the provided neural networks.  

---

