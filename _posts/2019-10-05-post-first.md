---
title: "테스트"
categories:
  - GAN
tags:
  - "잡담"
---

테스트입니다.

$$ \begin{align} C(G) & = \max_D V(G,D) = V(G,D^*_G) \\ 
&= \mathbb{E}_{x \sim p_{data}} \left[ \log D^*_G(x) \right] + \mathbb{E}_{z\sim p_z}\left[ \log(1-D^*_G(G(z))) \right] \\ 
&= \mathbb{E}_{x \sim p_{data}} \left[ \log D^*_G(x) \right] + \mathbb{E}_{x\sim p_g}\left[ \log(1-D^*_G(x)) \right] \\ 
&= \mathbb{E}_{x \sim p_{data}} \left[ \log \frac{p_{data}(x)}{p_{data}(x)+p_{g}(x)} \right] + \mathbb{E}_{x\sim p_g} \left[ \log \frac{p_{g}(x)}{p_{data}(x)+p_{g}(x)} \right] 
\end{align} $$
