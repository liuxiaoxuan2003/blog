---
title: "Introduction to RecSys: From Collaborative Filtering to Deep Learning"
slug: "recsys-intro"
description: "A beginner's guide to recommendation systems, covering the evolution from classic collaborative filtering to deep learning models."
date: 2026-05-14
image: cover.jpg
categories:
  - Recommendation Systems
tags:
  - RecSys
  - Collaborative Filtering
  - Deep Learning
  - Getting Started
---

## What is a Recommendation System?

A Recommendation System is a type of information filtering system that predicts a user's "rating" or "preference" for items, recommending content they might be interested in.

Recommendation systems are everywhere today:
- E-commerce "You may also like"
- Short video feed recommendations
- Music app daily playlists

---

## Classic Approach: Collaborative Filtering

### User-based CF

Core idea: **Similar users like similar items**

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# User-item rating matrix
ratings = np.array([
    [5, 3, 0, 1],
    [4, 0, 0, 1],
    [1, 1, 0, 5],
    [0, 0, 5, 4],
])

# Compute cosine similarity between users
user_sim = cosine_similarity(ratings)
print(user_sim)
```

### Item-based CF

Core idea: **Users like items similar to what they've liked before**

---

## Matrix Factorization

Decompose the user-item interaction matrix into low-rank matrices:

$$R \approx P \cdot Q^T$$

Where $P \in \mathbb{R}^{m \times k}$, $Q \in \mathbb{R}^{n \times k}$, and $k$ is the latent factor dimension.

---

## The Deep Learning Era

| Model | Year | Core Idea |
|-------|------|-----------|
| DeepFM | 2017 | FM + DNN parallel structure |
| DIN | 2018 | Attention mechanism for user interest |
| DIEN | 2019 | GRU for interest evolution |
| SIM | 2020 | Long-sequence user behavior modeling |

---

## Modern RecSys Architecture

```
Request → Recall → Pre-ranking → Ranking → Re-ranking → Display
```

Each stage has unique challenges and solutions, which we'll explore in future posts.

---

## Summary

Recommendation systems are a field where theory and engineering are deeply intertwined. From simple collaborative filtering to today's LLM-powered approaches, this field continues to evolve rapidly.

> *Life is a Markov chain* — A user's next click only depends on their current state. But is that really true? That's exactly what we need to explore.

---

*Next up: The Evolution of CTR Prediction Models*
