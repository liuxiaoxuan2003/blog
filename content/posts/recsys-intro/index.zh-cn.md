---
title: "推荐系统入门：从协同过滤到深度学习"
slug: "recsys-intro"
description: "一篇推荐系统入门指南，梳理从经典协同过滤到深度学习推荐模型的演进脉络。"
date: 2026-05-14
image: cover.jpg
categories:
  - 推荐系统
tags:
  - RecSys
  - 协同过滤
  - 深度学习
  - 入门
---

## 什么是推荐系统？

推荐系统（Recommendation System）是信息过滤系统的一种，旨在预测用户对物品的"评分"或"偏好"，从而向用户推荐可能感兴趣的内容。

如今推荐系统无处不在：
- 电商平台的"猜你喜欢"
- 短视频的信息流推荐
- 音乐 App 的每日推荐歌单

---

## 经典方法：协同过滤

### User-based CF

核心思想：**相似的用户喜欢相似的物品**

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# 用户-物品评分矩阵
ratings = np.array([
    [5, 3, 0, 1],
    [4, 0, 0, 1],
    [1, 1, 0, 5],
    [0, 0, 5, 4],
])

# 计算用户间的余弦相似度
user_sim = cosine_similarity(ratings)
print(user_sim)
```

### Item-based CF

核心思想：**用户喜欢和他之前喜欢的物品相似的物品**

---

## 矩阵分解

将用户-物品交互矩阵分解为低秩矩阵：

$$R \approx P \cdot Q^T$$

其中 $P \in \mathbb{R}^{m \times k}$，$Q \in \mathbb{R}^{n \times k}$，$k$ 为隐因子维度。

---

## 深度学习时代

| 模型 | 年份 | 核心思想 |
|------|------|----------|
| DeepFM | 2017 | FM + DNN 并行结构 |
| DIN | 2018 | 注意力机制建模用户兴趣 |
| DIEN | 2019 | GRU 建模兴趣演化 |
| SIM | 2020 | 长序列用户行为建模 |

---

## 现代推荐系统架构

```
用户请求 → 召回（Recall）→ 粗排 → 精排（Rank）→ 重排 → 展示
```

每个阶段都有其独特的挑战和解决方案，后续文章会逐一深入。

---

## 总结

推荐系统是一个理论和工程高度结合的领域。从最简单的协同过滤，到如今的大模型加持，这个领域一直在快速演进。

> *Life is a Markov chain* —— 用户的下一次点击，只取决于当前状态。真的是这样吗？这正是我们需要探索的问题。

---

*下一篇：CTR 预估模型演进史*
