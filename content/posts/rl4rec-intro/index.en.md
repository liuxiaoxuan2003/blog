---
title: "When RL Meets RecSys: An Introduction to RL4Rec"
slug: "rl4rec-intro"
description: "Exploring reinforcement learning applications in recommendation systems, from MDP modeling to policy optimization."
date: 2026-05-12
image: cover.jpg
categories:
  - Recommendation Systems
  - Reinforcement Learning
tags:
  - RL4Rec
  - Reinforcement Learning
  - MDP
  - Exploration
---

## Why Does RecSys Need Reinforcement Learning?

Traditional supervised learning paradigm in RecSys has several core issues:

1. **Myopic optimization**: Only optimizes immediate clicks/conversions, ignoring long-term user value
2. **Insufficient exploration**: Always recommends "safe" content, leading to homogeneous experiences
3. **Feedback loops**: Model only learns from displayed content feedback, creating filter bubbles

The RL framework naturally addresses these problems.

---

## Modeling Recommendation as MDP

$$\text{MDP} = (S, A, P, R, \gamma)$$

| Element | RecSys Mapping |
|---------|---------------|
| State $s$ | User behavior history, user profile |
| Action $a$ | Recommended items (list) |
| Reward $r$ | User feedback (click, purchase, dwell time) |
| Transition $P$ | User state transition (interest evolution) |
| Discount $\gamma$ | Long-term reward discount factor |

---

## Classic Approaches

### DQN-based Recommendation

```python
import torch
import torch.nn as nn

class DQNRecommender(nn.Module):
    def __init__(self, state_dim, num_items, hidden_dim=128):
        super().__init__()
        self.network = nn.Sequential(
            nn.Linear(state_dim, hidden_dim),
            nn.ReLU(),
            nn.Linear(hidden_dim, hidden_dim),
            nn.ReLU(),
            nn.Linear(hidden_dim, num_items)
        )
    
    def forward(self, state):
        # Q(s, a) for all items
        return self.network(state)
    
    def recommend(self, state, top_k=10):
        q_values = self.forward(state)
        _, indices = torch.topk(q_values, top_k)
        return indices
```

### Policy Gradient Methods

Directly learn the recommendation policy $\pi_\theta(a|s)$, optimized via REINFORCE or Actor-Critic:

$$\nabla_\theta J(\theta) = \mathbb{E}\left[\sum_t \nabla_\theta \log \pi_\theta(a_t|s_t) \cdot G_t\right]$$

---

## Exploration vs Exploitation

One of the most critical challenges in RL4Rec:

- **Exploitation**: Recommend content users are likely to enjoy (high short-term reward)
- **Exploration**: Try new content to discover latent interests (long-term value)

Common strategies:
- ε-greedy
- UCB (Upper Confidence Bound)
- Thompson Sampling
- Curiosity-driven exploration

---

## Challenges

1. **Offline evaluation**: How to evaluate RL policies without online A/B tests?
2. **Large action space**: Item catalogs are typically in millions
3. **Delayed rewards**: Users may convert long after the recommendation
4. **Safety constraints**: Can't severely harm UX for exploration

---

## Recommended Papers

- Zheng et al., "DRN: A Deep Reinforcement Learning Framework for News Recommendation" (WWW 2018)
- Chen et al., "Top-K Off-Policy Correction for a REINFORCE Recommender System" (WSDM 2019)
- Xin et al., "Self-Supervised Reinforcement Learning for Recommender Systems" (SIGIR 2020)

---

*This is just the tip of the iceberg. Future posts will dive into Offline RL and Model-based RL in recommendations.*
