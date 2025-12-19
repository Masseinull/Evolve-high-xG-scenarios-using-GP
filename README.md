# Evolving High-xG Attacking Strategies in a Football Simulator Using Genetic Programming

This project explores the use of **Genetic Programming (GP)** to evolve interpretable attacking strategies in a football simulation environment.  
Instead of optimizing for goals scored, the system explicitly optimizes **Expected Goals (xG)**, a widely used metric in football analytics that measures the quality of scoring chances.

The goal is to investigate whether evolutionary methods can discover **human-readable decision rules** that consistently lead to higher-quality attacking opportunities.

---

## Overview

- **Method**: Genetic Programming (decision-tree policies)
- **Domain**: Football analytics & simulation
- **Environment**: Google Research Football (GRF)
- **Objective**: Maximize Expected Goals (xG) of final shots
- **Output**: Interpretable decision trees representing attacking tactics

Each GP individual represents a decision tree that controls the **ball-carrying attacker** in a constrained attacking scenario. The evolved strategies decide when to **move, pass, or shoot** based on spatial and tactical features.

---

## Simulation Environment

- **Environment**: `academy_3_vs_1_with_keeper` from Google Research Football
- **Scenario**:
  - 3 attackers vs 1 defender + goalkeeper
  - Fixed starting position near the opponent’s penalty area
  - Episode ends on shot, turnover, or time limit

This simplified setup allows efficient evaluation while still capturing meaningful attacking decisions.

---

## Observation & Feature Space

Each decision is based on a compact set of features derived from the raw environment state, including:

- Ball position (x, y)
- Player positions
- Distance to nearest defender
- Distance to nearest teammate
- Distance from center line
- Number of completed passes in the current possession

These features provide enough tactical context while keeping the decision trees interpretable.

---

## Action Space

The evolved policies can choose from a subset of football actions:

- Movement: up, down, left, right
- Passing: short pass, long pass, high pass
- Shooting
- No-op (idle)

Only the **ball carrier** is controlled by GP. Off-ball teammates follow scripted support behavior to keep the search space manageable.

---

## Genetic Programming Framework

### Genome Representation

Each individual is a **decision tree** composed of:

- **Internal nodes**: IF–THEN–ELSE conditions (feature > threshold)
- **Leaf nodes**: concrete actions (pass, shoot, move, etc.)

This structure produces policies that are:
- Interpretable
- Human-readable
- Easy to visualize and analyze

---

### Fitness Function: Expected Goals (xG)

The fitness of each individual is defined as the **mean xG of the final shot** across multiple simulation episodes.

The xG model considers:
- Shot distance to goal
- Shooting angle
- Defensive pressure

This encourages the evolution of strategies that:
- Avoid low-quality long shots
- Prefer close-range, high-probability chances
- Value positioning and patience over shot volume

---

### Evolutionary Operators

- **Selection**: Tournament selection with elitism
- **Crossover**: Subtree-level crossover (swapping tactical branches)
- **Mutation**: Gaussian noise applied to decision thresholds
- **Elitism**: Top-performing individuals preserved across generations

This setup balances exploration with stability and preserves interpretable structures.

---

## Results

- Mean xG improved significantly over generations
- Best individual achieved nearly **3× higher xG** compared to initial population
- Evolved strategies consistently:
  - Carried the ball into high-value shooting zones
  - Avoided speculative shots
  - Used passing selectively to improve position

The final decision trees remained compact and readable, allowing qualitative inspection of learned tactics.

---

## Visualization & Analysis

The project includes:
- Visualization of attack trajectories and shot locations
- Decision tree graphs showing tactical logic
- Analysis of pass counts, shot positions, and xG distribution

These tools help connect **quantitative performance** with **qualitative behavior**.

---

## Limitations

- Simplified 3v1 scenario does not capture full match complexity
- Defender behavior is predictable
- Off-ball teammate movement is scripted
- xG model is simplified and does not capture all real-world factors

As a result, strategies are **scenario-specific** and not directly transferable to full matches without extension.

---

## Future Work

Possible extensions include:
- Multi-objective fitness (xG, possession time, risk)
- Larger team scenarios
- Co-evolving attackers and defenders
- Richer xG models
- Evolving off-ball movement strategies

---

## Technologies Used

- Python
- Google Research Football
- Genetic Programming
- Decision Trees
- Data Analysis & Visualization
- NumPy, Matplotlib, Graphviz

---

## Author

**Mohammadhossein Arsalan**  
MSc Computer Science, McMaster University  

This project was completed as part of Evolutionary Computing course and reflects an interest in **interpretable machine learning**, **evolutionary computation**, and **sports analytics**.
