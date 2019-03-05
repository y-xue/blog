---
layout: page
title: A Question about Federated learning
---

#### Estimating the distribution of a user's data in federated learning

Federated learning is a process of training where data owners (clients) collaboratively train a shared model without sharing their own data. A general process works as follows. 

1. A curator (server) sends the current model to clients.
2. Clients improve the model by training it on their own data.
3. Clients send back the updates.
4. The curator aggregates updates from clients and update the current model.
5. Repeat 1 - 4.

In general, clients improve the model by minimizing a shared loss function. Only the values of parameters (or gradients of parameters) of the model are shared with server. The private data stay on the clients' end. Many work have been done to ensure less information leakage of clients' data through shared parameters (or gradients). However, it is not clear of how much privacy a federated learning algorithm should guarantee and what properties of the clients' data the server can learn. 

Suppose a smart phone user donwloads an App that provides a service trained through federated learning. After the user agrees to participate in the training process, the developers of the App will take control. They may choose to optimize any function, including, but not limited to, the loss function of the service model, by collecting parameter estimates from the Apps on users' end. In this scenario, the server has a chance to learn the distirbution of a user's data by collecting the maximum likelihood estimates.

The server first proposes a particular distribution that a user's data may be drawn from. Then, instead of letting clients minimize a loss function, the server now let clients maximize the likelihood function of the parameters of the chosen distribution on their own data. For example, the server may assume that a user's data are drawn from a normal distribution \\( \mathcal{N} (\mu,\sigma^2) \\). The server sends a random guess \\( \mu_0 \\) to a client. The client maximizes the likelihood function \\( f(x_1,...,x_n\|\mu,\sigma) = (\frac{1}{\sqrt{2 \pi} \sigma})^n e^{-\sum_{i=1}^{n} \frac{(x_i - \mu)^2}{2 \sigma^2}} \\) on its own data \\( (x_1,x_2,...,x_n) \\) and sends the update of \\( \mu \\) back to server. In this example, the client can directly calculate the estimate \\( \hat{\mu} = \bar{\mathbf{x}} \\) and does not need \\( \mu_0 \\) as a starting point. 

In short, the server can collect parameters that reflect the distribution of a user's data through maximum likelihood estimation. This process does not break the rule of federated learning that users do not expose their private data to others. However, the server can learn the distribution of a user's data in the training process.

The question is, in practice, is there a  privacy standard in federated learning that specifies what kind of summaries (or parameters) a server can collect from users? In federated learning, is it allowed for the server to infer the distribution of a user’s data in any ways, explicitly through maximum likelihood estimation or maybe implicitly through shared parameters (or gradients) of a regular loss function?
