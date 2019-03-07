---
layout: page
title: Federated learning and privacy
---

Federated learning is a process of training where data owners (clients) collaboratively train a shared model without sharing their own data. A general process works as follows. 

1. A curator (server) sends the current model to clients.
2. Clients improve the model by training it on their own data.
3. Clients send back the updates.
4. The curator aggregates updates from clients and updates the current model.
5. Repeat 1 - 4.

In general, clients improve the model by minimizing a shared loss function. Only the values of parameters (or gradients of parameters) of the model are shared with the server. The private data stay on the clients' end. Many works have been done to ensure low information leakage of clients' data through shared parameters (or gradients). However, it is not clear how much privacy a federated learning algorithm should guarantee and what properties of the clients' data the server can learn. 

Suppose a client provides a service trained through federated learning. After the client agrees to participate in the training process, the server starts the process. It may choose to optimize any function, including, but not limited to, the loss function of the service model, by collecting parameter estimates from the clients. 

Under the following scenario, the server has a chance to learn the distribution of client data by collecting the maximum likelihood estimates. The server would assume a particular distribution that client data may be drawn from. Then, instead of letting clients minimize a loss function, the server now let clients maximize the likelihood function of the parameters of the chosen distribution on their own data. For example, the server may assume that client data are drawn from a normal distribution. The server sends the current mean estimate to a client. The client maximizes the likelihood function on its own data and sends the update of the mean back to the server. 

In short, the server can collect parameters that reflect the distribution of client data through maximum likelihood estimation. This process does not break the rule of federated learning that clients do not expose their private data to others. However, the server can learn the distribution of the client data in the training process. To be clear, each client needs to agree to make updates with respect to the original loss function and the predefined likelihood function.

We wonder if there is a privacy standard in federated learning that specifies what kind of summaries (or parameters) a server can collect from clients? In federated learning, is it allowed for the server to infer the distribution of the client data by distribution fitting, explicitly through maximum likelihood estimation or maybe implicitly through shared parameters (or gradients) of a regular loss function?
