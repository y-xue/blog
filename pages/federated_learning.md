---
layout: page
title: Federated learning
---

#### Estimating distribution of user's data in federated learning

Federated learning is a process of training where data owners (clients) collaboratively train a shared model without sharing their own data. A general process works as follows. 

1. A curator (server) send the current model to clients.
2. Clients improve the model by training it on their own data.
3. Clients send back the updates.
4. The curator aggregates updates from clients and update the current model.
5. Repeat 1 - 4.

In general, clients improve the model by minimizing a shared loss function. Only the parameters (or gradients of parameters) are sent to server. The private data stay on clients' end. Many work have been done to ensure less privacy leak of client data through shared parameters (or gradients). However, there is no standard of how much privacy should a federated learning algorithm guarantees.

Suppose a user donwloads an App that provides a service trained through federated learning. After the user agrees to participate in the training process, the developers of the App will take control. They can choose any loss function to optimize and gather parameter estimates from the App on users' end. In this scenario, the server has a chance to learn the distirbution of user's data by gathering the maximum likelihood estimate.

Instead of letting clients minimize a loss function, the server can choose a possible distribution that user's data are drawn from and let clients maximize the likelihood function for the parameters of this distribution on their own data. For example, the server assumes that a user's data are drawn from a normal distribution \\( \mathcal{N} (\mu,\sigma^2) \\). The server sends a random guess \\( \mu_0 \\) to a client. The client maximizes the likelihood function \\( (\frac{1}{\sqrt{2 \pi} \sigma})^n e^{-\sum_{i=1}^{n} \frac{(x_i - \mu)^2}{2 \sigma^2}} \\) on its own data \\( (x_1,x_2,...,x_n) \\) and sends back the updates of \\( \mu \\) to the server. In this example, the client can directly calculates the estimate of \\( \hat{\mu} = \bar{\mathbf{x}} \\) and does not need \\( \mu_0 \\). In short, the server can collect parameters that reflect the distribution of user's data though maximum likelihood estimate. This process does not break the rule of not collecting private data from users. However, the server learns the distribution of user's data.

The question is, in practice, is there a  privacy standard in federated learning that specifies what kind of summaries (or parameters) a server can collect from users? Is it allowed for the server to infer the distribution of user's data in any ways (explicitly through MLE or implicitly)?
