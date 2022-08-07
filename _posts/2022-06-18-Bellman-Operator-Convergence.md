---
layout: post
title: Contraction Property of Bellman Operator with contraction operator $\gamma < 1$
date: 2022-02-20 18:00:00
description: This blog post shows that the Bellman Operator used in value iteration is a contraction operator with contraction $\gamma<1$ and with respect to the $l_{\infty}$-norm.
tags: ReinforcementLearning
categories: rl-posts
---

A Markov Decision Process (MDP) framework is defined using the tuple $$(S, A, p, r)$$. The state space, $$S$$ and the action space $$A$$ is assumed to be discrete. The state transition probability $$p: S \times S \times A \to [0,1]$$ is the probability mass function (since state and action space are assumed to be discrete) and $$r:S \times A \to \mathbb{R}$$ is the reward function.

For the defined MDP settting we consider that the objective is to find a optimal policy $$\pi: S \to A$$ (stationary deterministic policy) such that the discounted reward is maximized, i.e.,

$$ \pi^* =  \argmax_{\pi} \mathbb{E}\left[\sum_{t=0}^T \gamma^t r(s_t, \pi(s_t))) \right]$$

where $$s_t$$ is the state at time instant $$t$$, $$a_t = \pi(s_t)$$ is the action taken at time instant $t$ follwing the policy $$\pi$$, $$\gamma \in (0,1]$$ is the discount factor and $$T$$ is the length of the episode.

For a given policy $$\pi$$, the state $$s \in S$$ is associated with a value and is given by,

$$V_{\pi}(s) = \mathbb{E} \left[\sum_{t=0}^T \gamma^t r(s_t, \pi(s_t)|s_0=s\right]$$

The state value $$V_{\pi}(s)$$ is the total discounted reward obtained by starting from state $$s$$ and then following the policy $$\pi$$ over the entire episode.

We can show that the state value $$V_{\pi}(s)$$ to be,

$$V_{\pi}(s) =  \mathbb{E}[r(s, \pi(s))] + \gamma \sum_{s' \in S} P_{s,s'}(\pi(s)) V_{\pi}(s)$$

where $$P_{s,s'}(\pi(s))$$ is the probability associated with the transition from state $$s$$ to $$s'$$ when action $$\pi(s)$$ is taken being in state $$s$$. It it interpreted as the expected sum of immediate reward and the discounted future reward with discount factor $$\gamma$$.

A optimal policy $$\pi^*$$ and the corrsponding optimal value $$V_{\pi^*}(s) \; \; \forall s \in S$$ can be obtained by a iterative algorithm called as value iteration. (We can also obtain it by policy iteration. Both value iterationa and policy iteration are dynamic programming algorithms.)

Briefly the algorithm corresponding to value iteration is given as follows:

* $$\textbf{Initalization}$$ : Initialize $$V_0(s) \text{ arbitrarily } \; \;  \forall s \in S.$$

* for $$t=1,2,\dots$$
  
  * $$V_t(s) = \max_a \left(r(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a)V_{t-1}(s')\right) \;\; \forall s \in S.$$
  
* Perform the above step until $$V_{t}(s) = V_{t-1}(s) = V^*(s),\;\; \forall s \in S$$ (Practically stop when $$|V_{t}(s) - V_{t-1}(s)| \leq \epsilon \;\; \forall s \in S$$ where $$\epsilon$$ is the tolerence level.

The policy evaluation and imporvement step in the value iteration can be represented as,

$$ T(V(s)) =  \max_a \left(r(s,a) + \gamma \sum_{s' \in S} P_{s,s'}(a)V(s')\right) \;\; \forall s \in S,$$

where $$T: \mathbb{R}^{|S|} \to \mathbb{R}^{|S|}$$ is called the Bellman Operator. Let $$\mathbf{V} = \{V(s) : s\in S\}$$ be the $$|S|$$-dimensional vector. Then we can show that $$\mathbf{V}^*$$ is unique (i.e., $$T(\mathbf{V}) \neq V \;\; \forall \; \mathbf{V} \neq \mathbf{V}^*$$). Hence, $$\mathbf{V}^*$$ is called the fixed point of operator $T$. This arises due to the fact that the Bellman operator $T$ has the contraction property.
In the below, we prove the contraction propety by showing that,

$$||T(V_1) - T(V_2)||_{\infty} \leq \gamma ||V_1 - V_2||_{\infty}$$

where, $$\gamma \in (0,1)$$ is the discount factor.

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

Now $$\forall s' \in S$$ we have,

$$V_1(s') - V_2(s) \leq \max_{s' \in S} |V_1(s') - V_2(s')| = ||V_1 - V_2||_{\infty}.$$

Hence,

$$ T(V_1(s)) - T(V_2(s)) \leq \gamma \sum_{s' \in S} P_{s,s'} ||V_1 - V_2||_{\infty}$$

$$T(V_1(s)) - T(V_2(s)) \leq \gamma ||V_1 - V_2||_{\infty}, \;\; \forall s \in S \;\; \left(\because \sum_{s' \in S} P_{s,s'} = 1\right) $$

Similarly,

$$T(V_2(s)) - T(V_1(s)) \leq \left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_1(s')\right) - \left(R(s,a_2^*) + \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) V_2(s')\right) \;\; (\because a_1^* \in A)$$

$$T(V_2(s)) - T(V_1(s)) \leq \gamma \sum_{s' \in S} P_{s,s'}(a_2^*) \left( V_1(s') - V_2(s')\right) \;\; (\because a_2^* \in A) $$

Similar arguments as done above will lead to,

$$ T(V_1(s)) - T(V_2(s)) \leq \gamma ||V_1 - V_2||_{\infty}, \;\; \forall s \in S $$

Since $$x \leq y$$ and $$-x \leq y$$ implies $$|x| \leq y$$. Hence we have,

$$|T(V_2(s)) - T(V_1(s))| \leq \gamma ||V_1 - V_2||_{\infty} \;\; \forall s \in S$$

As the above expression is true for all $$s\in S$$. We have,

$$||T(V_1) - T(V_2)||_{\infty} \leq \gamma ||V_1 - V_2||_{\infty}$$


# References:

* [Theory: Infinite horizon discounted MDP](https://adityam.github.io/stochastic-control/inf-mdp/discounted-mdp/)
* Reinforcement Learning Course (CS420) - IIT Dharwad
