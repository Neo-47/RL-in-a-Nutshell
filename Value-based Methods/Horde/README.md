# Horde: A Scalable Real-time Architecture for Learning Knowledge from Unsupervised Sensorimotor Interaction
+ **Authors**: Richard Sutton, Joseph Modayil, Michael Delp, Thomas Degris, Patrick Pilarski, Adam White, Doina Precup
+ **Tags**: knowledge representation, robotics, reinforcement learning, off-policy, temporal difference learning, value function approximation
+ **Year**: 2011

## Table of contents
+ The Problem
+ Why learn value functions
+ Contributions

## The problem
How to learn, represent, and use knowledge of the world in a general sense reamains a key open problem in AI. There are high-level representation languages based on first-order predicate logic and Bayes networks that are very expressive, but in these languages knowledge is difficult to learn and computationally expensive to use.

There are also low-level languages such as differential equations and state-transition matrices that can be learned from data without supervision, but these are much less expressive. There remains rooms for exploring alternate formats for knowledge that are expressive yet learnable from unsupervised sensorimotor data.


Horde is an architecture that consists of a large number of independant reinforcement learning sub-agents, or demons. Each demon is responsible for answering a single predictive or goal-oriented question about the world, thereby contributing in a factored, modular way to the system's overall knowledge. The questions are in the form of a value function, but each demon has its own policy, reward function, termination function, and terminal-reward function unrelated to those of the base problem. In this approach, the knowledge is represented as a large number of approximate value functions learned in parallel, each with its own policy, pseudo-reward function, pseudo-termination function, and pseudo-terminal-reward function.

