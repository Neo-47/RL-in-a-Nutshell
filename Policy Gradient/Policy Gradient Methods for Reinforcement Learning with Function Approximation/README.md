# Policy Gradient Methods for Reinforcement Learning with Function Approximation

## Table of contents
+ The Problem
+ The Solution
+ The Theorem


## The Problem

As mentioned in the [summary](https://github.com/Neo-47/RL-in-a-Nutshell/tree/master/DQN%20/Human%20level%20control%20through%20deep%20RL) of DQN paper, value-function approach has worked well in 
many applications, but has several limitations. First, it's oriented toward finding
a deterministic policy, whereas the optimal policy is often stochastic, e.g. in the 
two player game of rock-paper-scissors, a deterministic policy is easily exploited,
whereas a uniform random policy is optimal. Second, an arbitrarily small change in the 
estimated value of an action can cause it to be, or not to be selected. Such discontinuous
changes have been identified as a key obstacle to establishing convergence assurances for 
algorithms following the value-function approach.

As mentioned in the problem section of DQN summary [here](https://github.com/Neo-47/RL-in-a-Nutshell/tree/master/DQN%20/Human%20level%20control%20through%20deep%20RL#the-problem), small updates to Q may significantly change the policy and therefore change the data distribution, i.e. an update that increases Q(st, at) often increases Q(st+1, at) for all a and hence also increases the target, possibly leading to oscillations or divergence of the policy. You can read more
to see how they treated this problem from the value-based methods perspective.

## The Solution

Policy gradient methods try to optimize the policy directly instead of working with 
value functions. In these methods, the agent sees some experience and from that
experience tries to figure out how to change the policy in the direction that makes
it better. In this approach, the policy is explicitly represented by its own function approximator,
independent of the value function, and is updated according to the gradient of expected 
reward with respect to the policy parameters.

Rather than approximating a value function and using that to compute a deterministic
policy, we approximate a stochastic policy directly using an independent function
approximator with its own parameters. The policy might be represented by a neural 
network whose input is a representation of the state, whose output is action selection
probabilities, and whose weights are the policy parameters.

Let *θ* denote the vector of policy parameters and *ρ* the performance of the corresponding
policy (e.g., the average reward per time step). Then, in the policy gradient approach, 
the policy parameters are update approximately proportional to the gradient:

<p align="center">
<img src = "https://user-images.githubusercontent.com/19307995/44950610-4731e580-ae4c-11e8-9b5c-8ada6e96ddd0.png">
</p>

where α is a positive-definite step size. If the above can be achieved, then *θ* can
usually be assured to converge to a locally optimal policy in the performance measure
*ρ*. Unlike the value-function approach, here small changes in *θ* can cause only small
changes in the policy and in the state-visitation distribution. This paper proves that
a version of policy iteration with general differentiable function approximation is
convergent to a locally optimal policy.

## The Theorem

The standard reinforcement learning framework is considered, in which a learning agent
interacts with a Markov decision process (MDP). The state, action, and reward at each
time t ∈ {0, 1, 2, ...} are denoted st ∈ *S*, at ∈ *A*, and rt ∈ *R* respectively.
The environment's dynamics are characterized by state transition probabilities, 

<p align="center">
<img src = "https://user-images.githubusercontent.com/19307995/44950981-d09ae500-ae57-11e8-90aa-76f6f5a2e1c8.png">
</p>

and expected reward,

<p align="center">
<img src = "https://user-images.githubusercontent.com/19307995/44950984-e01a2e00-ae57-11e8-9097-1d614d42440b.png">
</p>

The agent's decision making procedure at each time is characterized by a policy, 
π(s, a, *θ*) = *Pr*{at = a| st = s, *θ*}, ∀s ∈ *S*, a ∈ *A*, where *θ* ∈ R is a paremeter
vector with length L where L << |*S*|. We assume that π is differentiable with respect
to its parameters, i.e., that the gradient exists.














