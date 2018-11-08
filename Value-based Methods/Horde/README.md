# Horde: A Scalable Real-time Architecture for Learning Knowledge from Unsupervised Sensorimotor Interaction
+ **Authors**: Richard Sutton, Joseph Modayil, Michael Delp, Thomas Degris, Patrick Pilarski, Adam White, Doina Precup
+ **Tags**: knowledge representation, robotics, reinforcement learning, off-policy, temporal difference learning, value function approximation
+ **Year**: 2011

## Table of contents
+ The Problem
+ Why learn value functions
+ General Value Functions

## The problem
How to learn, represent, and use knowledge of the world in a general sense remains a key open problem in AI. There are high-level representation languages based on first-order predicate logic and Bayes networks that are very expressive, but in these languages knowledge is difficult to learn and computationally expensive to use.

There are also low-level languages such as differential equations and state-transition matrices that can be learned from data without supervision, but these are much less expressive. There remains rooms for exploring alternate formats for knowledge that are expressive yet learnable from unsupervised sensorimotor data.


Horde is an architecture that consists of a large number of independant reinforcement learning sub-agents, or demons. Each demon is responsible for answering a single predictive or goal-oriented question about the world, thereby contributing in a factored, modular way to the system's overall knowledge. The questions are in the form of a value function, but each demon has its own policy, reward function, termination function, and terminal-reward function unrelated to those of the base problem. In this approach, the knowledge is represented as a large number of approximate value functions learned in parallel, each with its own policy, pseudo-reward function, pseudo-termination function, and pseudo-terminal-reward function.

## Why learn value functions

A distinctive, appealing feature of approximate value functions as a knowledge representation language is that they have an explicit semantics, a clear notion of truth grounded in sensorimotor interaction. A bit of knowledge expressed as an approximate value function is said to be true, or more precisely accurate, to the extent that its numerical values match those of the mathematically defined value function that it's approximating. 

A value function asks a question, what will the cumulative future reward be?. An approximate value function provides an answer to that question. The approximate value function is the knowledge, and its match to the value function, to the actual future reward, defines what it means for the knowledge to be accurate.

A problem may have both a reward function as known in the reinforcement learning framework, and also a terminal reward function z: S --> R, where z(s) is the terminal reward received if termination occurs upon arrival in state s. It's common to discount rewards by a factor of γ ∈ [0, 1] for each step of delay. One way to think about discounting is as a constant probability of termination, of 1 - γ, together with a terminal reward that is always zero.

More generally, we can consider there to be an arbitrary termination function, γ: S --> [0, 1], with 1 - γ(s) representing the probability of terminating upon arrival in state s, at which time a corresponding terminal reward z(s) would be registered. The overall return for the trajectory starting at time t, is then the sum of the per-step rewards received up until termination occurs, say at time T, plus the final terminal reward received in ST,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/48232278-c1856580-e3b9-11e8-8894-07a68e44d087.png"/>
</p>

The conventional action-value function Q is then defined as the expected return for a trajectory starting from the given state and action and selecting actions according to policy π until termination according to γ (thus determining the time of termination, T),

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/48232441-47a1ac00-e3ba-11e8-96e3-6beb73fb17ab.png"/>
</p>

The value function is the exact numerical answer to the precise, grounded question 'What would the return be from each state-action pair if policy π were followed?', and the approximate value function offers an approximate numerical answer. In this precise sense the value function provides a semantics for the knowledge represented by the AI agent's approximate value function.

## General Value Functions

The action-value function Q is equally dependant on ther reward and the terminal-reward functions, r and z. These functions could equally well have been considered inputs to the value function in the same way that π is. We might have defined a more general value function, which might be denoted,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/48233054-7c166780-e3bc-11e8-9099-3eb54bb6410d.png"/>
</p>

that would use returns from eqn(1) defined with arbitrary functiosn r and z acting as pseudo-reward function and pseudo-terminal reward function.









































