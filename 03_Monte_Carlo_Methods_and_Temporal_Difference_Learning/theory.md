# 3. Monte Carlo Methods and Temporal Difference Learning

## Monte Carlo Methods: Overview

**Monte Carlo simulation** is a computational method that uses random number generation to solve problems that might be deterministic in principle. It emerged in 1949 alongside the first electronic computers and was initially applied to model complex physical processes in nuclear reactors.

Monte Carlo methods rely on:
- **Statistical modeling**
- **Random sampling**
- **Statistical analysis** of results

They are particularly useful when:
- Analytical solutions are too complex or unknown
- Simulations can replace expensive or time-consuming physical experiments

### Advantages
- No need for complex mathematical models
- Easy to implement
- Accuracy improves by increasing the number of simulations
- Easily extendable models

### Disadvantages
- Can be computationally expensive
- Results are always approximate and probabilistic

### Example: Estimating the Area of a Circle
To estimate the area:
1. Generate random points in a square surrounding the circle
2. Count how many land inside the circle
3. Use the ratio of inside/total to approximate the area (and even \( \pi \))

---

## Monte Carlo in Reinforcement Learning (RL)

In RL, Monte Carlo methods are used to **estimate value functions** based on complete episodes — no knowledge of environment dynamics is required.

- **Policy Evaluation**: Estimate the expected reward from states under a given policy
- **Policy Improvement**: Use returns from episodes to improve the policy

The agent must wait until the episode ends to update value estimates.

---

## Markov Chain Monte Carlo (MCMC)

**MCMC** methods simulate probability distributions using Markov chains. They are widely used when:
- Sampling from complex distributions
- Bayesian inference
- Data modeling in high-dimensional spaces

Key idea: Generate samples (chains) where each state depends only on the previous one (Markov property).

### Applications:
- Estimating rare events (importance sampling)
- Bayesian statistics
- Expectation Maximization (EM)

MCMC converges to a **stationary distribution**, and statistics are computed once the chain stabilizes.

---

## Monte Carlo Method Steps

1. **Problem formulation** – define a probabilistic model
2. **Random number generation** – simulate random variables
3. **Simulation** – execute random sampling
4. **Statistical estimation** – compute means, variances, confidence intervals
5. **Decision-making** – interpret statistical results

---

## Temporal Difference (TD) Learning

TD learning estimates value functions **step-by-step**, without waiting for the episode to end. It's a hybrid between Monte Carlo and dynamic programming.

### Core Idea:
Update the value function after each action using observed reward and the estimate of the next state.

### Usage:
Ideal for environments where you can't wait for episode termination and must update in real time.

---

## TD(0): The Simplest TD Method

Updates value \( V(S_t) \) using only the immediate reward and the estimate of the next state's value:

\[ V(S_t) \leftarrow V(S_t) + \alpha (R_{t+1} + \gamma V(S_{t+1}) - V(S_t)) \]

Where:
- \( \alpha \) – learning rate
- \( \gamma \) – discount factor

### Pros:
- Fast
- Doesn’t require full episode
- Works well in online/real-time learning

---

## TD(λ) and TD(?)

**TD(λ)** is a generalization of TD(0), where \( \lambda \) controls how many future steps are considered in the update.

- \( \lambda = 0 \) → TD(0)
- \( \lambda = 1 \) → Monte Carlo

Update rule includes **multiple future steps**:

\[ V(S_t) \leftarrow V(S_t) + \alpha \delta_t \lambda^t \]

Where \( \delta_t \) is the TD error.

---

## Eligibility Traces

**Eligibility traces** track recently visited states and actions, allowing credit assignment over multiple steps.

### Purpose:
- Speeds up learning
- Assigns value more accurately to past actions that led to delayed rewards

### Example:
If an agent performs several actions and only receives a reward later, eligibility traces help to propagate that reward backward to earlier steps.

They are especially powerful when used with TD(λ).

---

## Summary

| Method        | Update Timing       | Needs Full Episode | Uses Future Steps | Strengths |
|---------------|---------------------|---------------------|-------------------|-----------|
| Monte Carlo   | End of episode      | Yes                 | All steps         | Accurate long-term estimation |
| TD(0)         | Step-by-step        | No                  | 1 step            | Fast and online-capable       |
| TD(λ)         | Step-by-step + trace| No                  | Multiple steps    | Balanced accuracy and speed  |

**Monte Carlo** focuses on full trajectories.  
**TD methods** enable faster, more incremental updates.  
**Eligibility traces** improve credit assignment over time.

Together, these form the backbone of modern reinforcement learning, enabling agents to learn optimal policies in stochastic and uncertain environments.

