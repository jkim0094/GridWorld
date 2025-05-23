# GridWorld

This repository contains code and experiments for a reinforcement learning project in a grid world environment.  
The project is structured in three stages:

---

## Project Stages

- **Stage 1**: Table-based Reinforcement Learning with a single agent  
- **Stage 2**: Deep Q-Learning (DQN) with a single agent  
- **Stage 3**: Multi-Agent Reinforcement Learning (MARL)

---

## Stage 1: Table-based Q-Learning Agent

This project implements a tabular Q-learning agent to solve a transport task in a grid world environment.  
The agent learns to pick up an item located at a random position (A) and deliver it to a fixed location (B) while minimizing the number of steps taken.

---

## 1. Environment Setup

- **Grid Size**: Default 5×5 (configurable)
- **Agent Start Position**: Randomized each episode
- **Item Location (A)**: Randomized per episode
- **Goal Location (B)**: Fixed at bottom-right corner (n, n)
- **State Space**: Agent position, item position, item possession
- **Action Space**: Move north, south, east, or west

---

## 2. Reward Design

- `-1`: Penalty per step (encourages shortest path)
- `+5 / -5`: Getting closer/farther from the item
- `+10 / -10`: Getting closer/farther from the goal while carrying the item
- `+50`: Successful delivery
- `-50`: Reaching the goal without the item

---

## 3. Q-Learning Summary

- **Q-table**: Initialized with zeros
- **Policy**: ε-greedy for exploration-exploitation balance
- **Learning Rate Decay (α)**: Gradually decreases over episodes
- **Exploration Rate Decay (ε)**: Decays toward a minimum threshold
- **Bellman Update Rule**:
  $$
  Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha [R_{t+1} + \gamma \max_{a'} Q(S_{t+1}, a') - Q(S_t, A_t)]
  $$

---

## 4. Training Procedure

- The agent is trained over 500 episodes.
- At each episode, the agent starts randomly and learns by updating Q-values step-by-step.
- Performance metrics include step count, total reward, Q-value change, and policy stability.

---

## 5. Visualizations

### 1. Steps and Total Rewards per Episode

The number of steps gradually decreases and rewards increase as the agent learns a more optimal policy.

![Steps and Total Rewards](images/stepNreward.png)

---

### 2. Q-value Convergence and Policy Stability

Q-values stabilize and the agent consistently selects optimal actions.

![Q-value Convergence and Policy Stability](images/Qvalue.png)

---

### 3. Learning Curve Stability (Reward Variance)

Early high variance indicates exploration, which stabilizes over time.

![Learning Curve Stability](images/learningcurv.png)

---

### 4. Exploration vs. Exploitation

Exploration is high in early episodes and gradually gives way to exploitation.

![Exploration vs Exploitation](images/exex.png)

---

### 5. GridWorld Simulation Snapshot

Agent (blue), item (green), and goal (yellow) shown at simulation start.

![GridWorld Simulation](images/Figure_1.png)

---

## 6. Conclusion

This project demonstrates the effectiveness of tabular Q-learning in solving a structured transport task in a discrete grid environment.

- **Improved efficiency**: The number of steps decreased over episodes while total reward increased.
- **Q-value convergence**: Q-values stabilized over time with learning rate decay.
- **Stable policy**: Actions became more consistent, indicating reliable learning.
- **Balanced exploration**: The decaying ε strategy allowed for early exploration and later exploitation.
- **Learning stability**: Reward variance decreased, showing more stable performance.

Q-learning, combined with effective reward shaping and decay strategies, enabled the agent to learn an efficient policy with no prior knowledge of the environment.

---

## 7. How to Run

```bash
# Set up virtual environment
uv venv .venv
source .venv/bin/activate

# Install dependencies
uv pip install -r requirements.txt

# Run the notebook
jupyter notebook stage1.ipynb
