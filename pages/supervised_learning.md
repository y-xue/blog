---
layout: page
title: Supervised Learning
---

Supervised learning is a machine learning task of learning a **function** that maps an input to an output based on example input-output pairs. 

It infers a function from **_labeled_** _training data_ consisting of a set of _training examples_.

Given input \\(x\\) and output \\(y\\), a supervised learning algorithm learns a function \\(f\\) such that \\(y = f(x)\\).

#### Algorithms of supervised learning

- Linear regression
  - \\( y = b + w_1 x_1 + ... + w_N x_N\\)
- Logistic regression
  - \\( y = \sigma(b + w_1 x_1 + ... + w_N x_N)\\)
  - \\( \sigma(x) = \frac{1}{1 + e^{-x}}\\)
- Decision tree
- Support vector machines
  - \\( W X + b \ge +1 \text{when } y = +1 \\)
  - \\( W X + b \le -1 \text{when } y = -1 \\)
- k-nearest neighbor algorithm
- Reinforcement learning
