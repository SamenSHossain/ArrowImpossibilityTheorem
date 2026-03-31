# Strategic Voting Dynamics Analysis: The Full Pipeline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python: 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)

This repository is a **voting system crash-test lab**. It utilizes synthetic population generation, hand-coded neural networks, Proximal Policy Optimization (PPO), and Evolutionary Game Theory (EGT) to analyze the robustness of different voting mechanisms against strategic manipulation. 

From validating Arrow's Impossibility Theorem to testing real-world 2020 Maine Congressional ballots, this pipeline provides a multi-objective analysis of how we choose our leaders.

## 🚀 The 10-Phase Pipeline

### 1. Foundation & Synthetic Generation
We generate a synthetic population of 10,000+ voters, each defined by a preference profile, a strategic inclination score, and a fairness-sensitivity parameter `λ`.
* **Systems Included:** Plurality, Borda Count, Instant Runoff (IRV), Condorcet, and Approval Voting.

### 2. Static Analysis
Baseline visualization of candidate rankings and system agreement. This phase serves as a "sanity check" to observe how different mechanisms interpret the same voter intent.

### 3. Strategic Neural Network Learning
A pure NumPy 2-layer MLP (hand-coded backpropagation) trains to find optimal ballot manipulation. 
* **The Goal:** Discover if a voter can profitably manipulate a ballot given their `λ` (fairness) constraint.

### 4. Arrow’s Impossibility Theorem Validation
We mathematically test all four of Arrow's conditions: Unrestricted Domain, Non-Dictatorship, Pareto Efficiency, and Independence of Irrelevant Alternatives (IIA).

### 5. Multi-Objective Optimization (Pareto Analysis)
We identify the "Pareto Frontier" between manipulation success and social welfare.
* **Key Discovery:** The "Sweet Spot" for fairness vs. utility is identified at `λ ≈ 0.292`.

### 6. Reinforcement Learning (PPO)
Using a custom OpenAI Gym environment, we train a PPO agent (Actor-Critic) to optimize voting strategies across 500 episodes. We observe how agents learn to "game" the system or converge toward honest voting.

### 7. Game-Theoretic Analysis
Calculation of **Nash Equilibrium Stability Scores (ESS)** and Population Entropy. This phase determines if a population's strategy will converge or remain in a state of chaotic flux.

### 8. Evolutionary Game Theory (EGT)
We simulate 300 generations of "replicator dynamics" where five strategies (Honest, Borda Manipulator, Bullet Voter, Condorcet Pusher, and PPO Agent) compete for dominance.

### 9. Real-World Validation
We move beyond theory by ingesting **10,000+ real Ranked Choice Voting (RCV) ballots** from the 2020 Maine Congressional District 2 election to see how these dynamics play out in the wild.

### 10. Cross-System Synthesis
The final comparison. We rank systems by their **Composite Vulnerability Score**, evaluating resistance to manipulation, social welfare preservation, and Arrow compliance.

---

## 📊 Key Findings

| Metric | Winner | Loser |
| :--- | :--- | :--- |
| **Strategic Robustness** | **IRV (Ranked Choice)** | **Borda Count** |
| **Manipulation Rate** | 15% | 37% |
| **EGT Dominance** | Diverse/Stable | Borda Manipulator (99.7%) |
| **Stability** | High | Low (Condorcet Cycles) |

* **IRV** is the most robust; sequential elimination naturally breaks most strategic attack vectors.
* **Borda Count** is highly vulnerable to "rank truncation" and bullet voting.
* **Condorcet** systems frequently fall into "Condorcet Paradox" cycles, preventing a stable strategy from emerging.

---

## 🛠 Installation

```bash
git clone [https://github.com/yourusername/voting-dynamics-analysis.git](https://github.com/yourusername/voting-dynamics-analysis.git)
cd voting-dynamics-analysis
pip install -r requirements.txt
```

## 💻 Usage

To run the full pipeline from voter generation to the final cross-system radar plots:

```bash
python main.py --run-all --voters 10000 --lambda_sweep
```

To run a specific phase (e.g., Evolutionary Game Theory):

```bash
python main.py --phase 8 --generations 300
```

---

## 🔬 Mathematical Context
The core of our fairness analysis relies on the parameter `λ`, where the voter's utility `U` is defined as:

$$U_{total} = (1 - \lambda)U_{self} + \lambda U_{social}$$

By sweeping `λ` from 0 (purely selfish) to 1 (fully altruistic), we map the boundaries of strategic voting.

---

**Disclaimer:** *This project is a simulation tool for academic and research purposes. While it uses real-world data, election outcomes are influenced by myriad factors beyond the scope of this mathematical model.*
