---
title: "强化学习遇上推荐系统：RL4Rec 初探"
slug: "rl4rec-intro"
description: "探索强化学习在推荐系统中的应用，从 MDP 建模到策略优化。"
date: 2026-05-12
image: cover.jpg
categories:
  - 推荐系统
  - 强化学习
tags:
  - RL4Rec
  - 强化学习
  - MDP
  - 探索与利用
---

## 为什么推荐系统需要强化学习？

传统推荐系统的监督学习范式存在几个核心问题：

1. **短视问题**：只优化即时点击/转化，忽略长期用户价值
2. **探索不足**：总是推荐"安全"的内容，用户体验趋于同质化
3. **反馈循环**：模型只能学到已展示内容的反馈，形成信息茧房

强化学习的框架天然适合解决这些问题。

---

## 将推荐建模为 MDP

$$\text{MDP} = (S, A, P, R, \gamma)$$

| 元素 | 推荐系统中的对应 |
|------|------------------|
| State $s$ | 用户历史行为序列、用户画像 |
| Action $a$ | 推荐的物品（列表） |
| Reward $r$ | 用户反馈（点击、购买、停留时长） |
| Transition $P$ | 用户状态转移（兴趣演化） |
| Discount $\gamma$ | 长期收益折扣因子 |

---

## 经典方法

### DQN-based 推荐

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

### Policy Gradient 方法

直接学习推荐策略 $\pi_\theta(a|s)$，通过 REINFORCE 或 Actor-Critic 优化：

$$\nabla_\theta J(\theta) = \mathbb{E}\left[\sum_t \nabla_\theta \log \pi_\theta(a_t|s_t) \cdot G_t\right]$$

---

## 探索与利用（Exploration vs Exploitation）

这是 RL4Rec 中最关键的问题之一：

- **Exploitation**：推荐用户大概率喜欢的内容（短期收益高）
- **Exploration**：尝试推荐新内容，发现用户潜在兴趣（长期价值）

常见策略：
- ε-greedy
- UCB (Upper Confidence Bound)
- Thompson Sampling
- 基于好奇心的探索

---

## 挑战与思考

1. **离线评估困难**：无法在线 A/B test 时如何评估 RL 策略？
2. **大动作空间**：物品库通常百万级，如何高效探索？
3. **延迟奖励**：用户可能过了很久才产生转化
4. **安全约束**：不能为了探索而严重损害用户体验

---

## 推荐论文

- Zheng et al., "DRN: A Deep Reinforcement Learning Framework for News Recommendation" (WWW 2018)
- Chen et al., "Top-K Off-Policy Correction for a REINFORCE Recommender System" (WSDM 2019)
- Xin et al., "Self-Supervised Reinforcement Learning for Recommender Systems" (SIGIR 2020)

---

*这只是 RL4Rec 的冰山一角，后续会深入探讨 Offline RL、Model-based RL 在推荐中的应用。*
