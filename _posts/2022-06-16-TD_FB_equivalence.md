---
layout: post
title: Equivalence of Forward and Backward view in TD($\lambda$) method
date: 2022-05-02 18:00:00
description: This blog post explains the equivalence of the forward view and the backward view in the Temporal Difference ($\lambda$) method. The same holds true for generalized advantage estimation.
tags: ReinforcementLearning
categories: rl-posts
authors:
  - name: Jayanth S
    url: "https://js2498.github.io"
    affiliations:
      name: IIT Dharwad
toc:
  - name: MC Estimate
  - name: TD Estimate
  - name: n-step TD estimate
  - name: TD(lambda) method
  - name: Equivalence of Forward and Backward View
---

To Do:

- MC Estimate
- TD Estimate
- n-step TD estimate
- TD($\lambda$) method
- SARSA algorithm
- Equivalence of FV and BV

The temporal difference (TD) error from eligibility trace update rule is,

$$ \Delta V_t^{TD}(s) = \alpha \delta_t e_t(s) $$

where, $$\delta_t = r_{t+1} + \gamma V(s_{t+1}) - V(s_t)$$ and $$e_t(s) = \gamma \lambda e_{t-1}(s) + I_{ss_t}$$ with $$I_{ss_t} = 1$$ if $$s=s_t$$ and $$0$$ otherwise.

Expanding $$e_t(s)$$ we obtain

$$e_t(s) = I_{ss_t} + \gamma \lambda e_{t-1}(s)$$
$$e_t(s) = I_{ss_t} + \gamma \lambda \left(\gamma \lambda e_{t-2}(s) + I_{ss_{t-1}}\right)$$
$$e_t(s) = I_{ss_t} + \gamma \lambda  I_{ss_{t-1}} + \gamma^2 \lambda^2 I_{ss_{t-2}} + \gamma^3 \lambda^3 I_{ss_{t-3}} + \dots$$
$$e_t(s) = \sum_{k=0}^t (\gamma \lambda)^{t-k} I_{ss_k}$$

The sum of TD errors over the trajectory in backward view for a state $s$ is,

$$\sum_{t=0}^{T-1} \Delta V_t^{TD}(s) = \sum_{t=0}^{T-1} \alpha \delta_t e_t(s) $$
$$\sum*{t=0}^{T-1} \Delta V_t^{TD}(s) = \sum*{t=0}^{T-1} \alpha \delta*t \left( \sum*{k=0}^{t} (\gamma \lambda)^{t-k} I\_{ss_k}\right)$$

Interchanging $$t$$ with $$k$$ and $$k$$ with $$t$$ on the RHS, we obtain

$$\sum_{t=0}^{T-1} \Delta V_t^{TD}(s) =  \sum_{k=0}^{T-1} \alpha \delta_t \left( \sum_{t=0}^{k} (\gamma \lambda)^{k-t} I_{ss_k}\right)$$

Expanding the RHS results in,

$$\sum_{t=0}^{T-1} \Delta V_t^{TD}(s) = \alpha \delta_0 (\gamma \lambda)^0 I_{ss_0} + \delta_1 ( \gamma \lambda I_{ss_0} + (\gamma \lambda)^0 I_{ss_1}) + $$
$$ + \delta*2 ( \gamma^2 \lambda^2 I*{ss*0} + \gamma \lambda I*{ss*1} + (\gamma \lambda)^0 I*{ss_2}) $$

$$ + \delta*3 ( \gamma^3 \lambda^3 I*{ss*0} + \gamma^2 \lambda^2 I*{ss*1} + \gamma \lambda I*{ss*2} + (\gamma \lambda)^0 I*{ss_3}) + \dots$$

$$ = \alpha \left( I*{ss_0} \sum*{k=0}^{T-1} (\gamma \lambda)^k \delta*k + I*{ss*1} \sum*{k=1}^{T-1} (\gamma \lambda)^{k-1} \delta_k + \dots \right)$$

$$ = \alpha \sum*{t=0}^{T-1} I*{ss*t} \left( \sum*{k=t}^{T-1} (\gamma \lambda)^{k-t} \delta_k \right)$$

Now, from the foward view the update rule is,

$$\Delta V_t^{\lambda}(s_t) = \alpha (L_t^{\lambda} - V_t(s_t)) $$

where, $$L_t^{\lambda}$$ is the weighted sum of n-step returns

Dividing the above equation by $\alpha$, we get

$$\frac{1}{\alpha} \Delta V_t^{\lambda}(s_t) = L_t^{\lambda} - V_t(s_t)$$
$$ = - V*t(s_t) + (1-\lambda) (R*{t+1} + \gamma V*t(s*{t+1})) + (1-\lambda)$$
