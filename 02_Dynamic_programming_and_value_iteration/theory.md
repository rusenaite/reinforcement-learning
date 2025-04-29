# Dynamic Programming and Value Iteration: Policy Evaluation and Improvement

## 1. What is Dynamic Programming?

Dynamic programming (DP) is a programming method based on breaking a complex problem into smaller, interrelated subproblems and storing their solutions. It trades computational time for memory usage. This method is especially useful when divide-and-conquer strategies are not efficient enough.

Dynamic programming is an effective technique to solve optimization problems and is applicable particularly to problems requiring optimal solutions.

Richard Bellman, who introduced and described dynamic programming in 1952, explained the origin of the term in his autobiography:

> In the 1950s, mathematical research wasn't highly appreciated. Wilson, the Secretary of Defense, hated anything related to scientific research. If someone mentioned "mathematics" in front of him, he would become furious. I was working at the RAND Corporation, funded by the Air Force, which reported to Wilson. I needed a term that concealed my mathematical research. I chose "programming" instead of "planning" and added "dynamic" to imply a multistage process. This way, the name was neutral and acceptable even for Congress.

Problems solvable with dynamic programming often appear in competitive programming and olympiads.

Although dynamic programming might seem complex at first, it is more of a problem-solving strategy than a strict algorithm. Therefore, understanding comes best through solving examples.

---

## 2. Optimization Problems

An optimization problem involves finding the best solution among many possible ones, each with an associated value.

### Example: The Knapsack Problem

A thief breaks into a museum and finds `n` valuable artifacts. Each artifact has a value `v_k` and a weight `s_k`. The thief can carry a knapsack with a maximum weight limit `S`. Which artifacts should the thief take to maximize the total value without exceeding the weight limit?

This is an optimization problem because:
- There are multiple ways to select items.
- Each selection has a different total value.
- The goal is to maximize the total value.

Important distinctions:
- **Solution**: The set of items chosen.
- **Solution Value**: The sum of the values of chosen items.

Finding any valid solution is often easy. Finding the **optimal solution** is the hard part.

**Greedy algorithms** (choosing the locally best option at each step) are sometimes used but don’t always guarantee an optimal global solution. It's crucial to verify if a greedy approach will produce an optimal result for a given problem.


---

## 3. Dynamic Programming (DP)

Dynamic programming is an optimization technique suitable for problems that can be decomposed into smaller subproblems.

The core idea:
- Store the solutions to subproblems.
- Reuse those solutions to avoid redundant computation.

DP is heavily used in **Reinforcement Learning (RL)** for finding optimal paths and policies in environments modeled by states and actions.

---

## 4. Value Iteration

Value iteration is an algorithm used to find the optimal policy when the environment model (transition probabilities and rewards) is known.

### Steps:
1. **Initialize**: Set initial values (usually zeros) for all states.
2. **Update**: Iteratively update each state's value based on the expected rewards and transition probabilities.
3. **Converge**: Repeat until value changes become negligible.

### Update Formula:

\[ V(s) = \max_a \sum_{s', r} P(s' \mid s, a) \left( R(s, a, s') + \gamma V(s') \right) \]

Where:
- \( V(s) \): value of state \( s \)
- \( a \): action
- \( P(s' \mid s, a) \): probability of transitioning to \( s' \) given action \( a \)
- \( R(s, a, s') \): reward for the transition
- \( \gamma \): discount factor (importance of future rewards)

---

## 5. Policy Evaluation and Improvement

Policy iteration consists of two steps:

### 1. **Policy Evaluation**
- Calculate the value function \( V(s) \) for a given policy.

### 2. **Policy Improvement**
- Update the policy by choosing the best action based on the current value function.

This process repeats until the policy stabilizes (no further improvements can be made).

**Algorithm Steps:**
1. Evaluate the current policy.
2. Improve the policy.
3. Repeat until convergence.

---

## 6. Bellman Equation

The **Bellman equation** defines the optimal value function recursively:

\[ V^*(s) = \max_a \sum_{s'} P(s' \mid s, a) \left( R(s, a, s') + \gamma V^*(s') \right) \]

Where:
- \( V^*(s) \): optimal value of state \( s \)
- \( P(s' \mid s, a) \): transition probability
- \( R(s, a, s') \): immediate reward
- \( \gamma \): discount factor

The Bellman equation is the foundation for both **value iteration** and **policy iteration**.

---

# 📚 Fibonacci Sequence: A Mathematical Beauty

The **Fibonacci sequence** is a famous mathematical sequence with real-world applications in computer science, cryptography, and art.

Introduced by **Leonardo of Pisa (Fibonacci)** in his 1202 book *Liber Abaci*, he used the sequence to model rabbit population growth.

The sequence is simple:

\[ 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, \dots \]

Each number is the sum of the two preceding ones.

The Fibonacci sequence is closely related to the **Golden Ratio** and appears frequently in nature, architecture, and algorithms.

---

# 📖 Summary

- **Dynamic Programming** solves complex problems by solving and storing subproblems.
- **Value Iteration** and **Policy Iteration** are key reinforcement learning strategies.
- **Bellman Equation** underpins the value functions in decision-making.
- **Fibonacci Sequence** demonstrates recursive relationships with broad applications.

