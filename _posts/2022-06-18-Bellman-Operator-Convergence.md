---
layout: post
title: Contraction Property of Bellman Operator with contraction operator $\gamma < 1$
date: 2022-02-20 18:00:00
description: This blog post shows that the Bellman Operator used in value iteration is a contraction operator with contraction $\gamma<1$ and with respect to the $l_{\infty}$-norm.
tags: ReinforcementLearning
categories: rl-posts
---

In this blog, we show that $$||T(V_1) - T(V_2)||_{\infty} \leq \gamma ||V_1 - V_2||_{\infty}$$ where, $$\gamma \in [0,1)$$.

Consider state $$s \in S$$. The Bellman operator is defined as,

$$T(V_1(s)) = \max_{a \in A} \left(R(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a) V_1(s')\right)$$

$$T(V_2(s)) = \max_{a \in A} \left(R(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a) V_2(s')\right)$$

Let the optimal actions,

$$a_1^* = \underset{a \in A}{\operatorname{\argmax}} \left(R(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a) V_1(s')\right)$$

$$a_2^* = \underset{a \in A}{\operatorname{\argmax}} \left(R(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a) V_2(s')\right)$$

Now,

$$T(V_1) - T(V_2) = \left(R(s,a_1^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_1^*) V_1(s')\right) - \left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_2(s')\right)$$

Since,

$$\left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_2(s')\right) \geq \left(R(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a) V_2(s')\right) \;\; \forall a \in A $$

Therefore,

$$T(V_1(s)) - T(V_2(s)) \leq  \left(R(s,a_1^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_1^*) V_1(s')\right) - \left(R(s,a_1^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_1^*) V_2(s')\right) \;\; (\because a_1^* \in A)$$

$$ T(V_1(s)) - T(V_2(s)) \leq \gamma \sum_{s' \in S} P_{s,s'}(a_1^*) \left( V_1(s') - V_2(s')\right) \;\; (\because a_1^* \in A)$$

Now $$\forall s' \in S$$, $$V_1(s') - V_2(s) \leq \max_{s' \in S} |V_1(s') - V_2(s')| = ||V_1 - V_2||_{\infty}$$

$$ T(V_1(s)) - T(V_2(s)) \leq \gamma \sum_{s' \in S} P_{s,s'} ||V_1 - V_2||_{\infty}$$

$$T(V_1(s)) - T(V_2(s)) \leq \gamma ||V_1 - V_2||_{\infty}, \;\; \forall s \in S \;\; \left(\because \sum_{s' \in S} P_{s,s'} = 1\right) $$

Similarly,

$$T(V_2(s)) - T(V_1(s)) \leq \left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_1(s')\right) - \left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_2(s')\right) \;\; (\because a_1^* \in A)$$

$$T(V_2(s)) - T(V_1(s)) \leq \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) \left( V_1(s') - V_2(s')\right) \;\; (\because a_2^* \in A) $$

Similar arguments as done above will lead to,

$$ T(V_1(s)) - T(V_2(s)) \leq \gamma ||V_1 - V_2||_{\infty}, \;\; \forall s \in S $$

Since $$x \leq y$$ and $$-x \leq y, \; \; \implies |x| \leq y$$. Hence we have,
$$|T(V_2(s)) - T(V_1(s))| \leq \gamma ||V_1 - V_2||_{\infty} \;\; \forall s \in S$$

As the above expression is true for all $$s\in S$$. We have,

$$||T(V_1) - T(V_2)||_{\infty} \leq \gamma ||V_1 - V_2||_{\infty}$$
