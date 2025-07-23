---
title: How could we measure the spatial inter-user interference using only the angular information ? 
summary: This question was answered during my PhD thesis!
date: 2025-07-07
type: docs
math: false
tags:
  - Intereference
  - mmWave communications
  - MIMO
  - Angular information
image:
  caption: ''
---

In wireless networks, the interference is a key parameter to investigate that could affect other parameters like SINR, throughput, etc. 

By definition, in multi-user communications, the inter-user interference reflects the non desired signal transmitted by the base station to serve another user. This could happens in different multiple access techniques like the frequency domain multiple access. And this metric will depend on the applied transmission technologies and radio ressource allocation techniques like MIMO, MIMO precoding, etc. 

For example, for multi-user transmission


In mmWave massive MIMO 

**Due to the importance of this metric, I aim in this article to present how we could measure** 

{{< math >}}
$$\gamma_{n} = \frac{ \left | \left (\mathbf x_{n} - \mathbf x_{n-1} \right )^T \left [\nabla F (\mathbf x_{n}) - \nabla F (\mathbf x_{n-1}) \right ] \right |}{\left \|\nabla F(\mathbf{x}_{n}) - \nabla F(\mathbf{x}_{n-1}) \right \|^2}$$
{{< /math >}}
