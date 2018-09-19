# Deep Reinforcement Learning with Double Q-learning

## Table of contents
+ The Problem
+ The Solution
+ The Architecture
+ The Algorithm Pseudocode

## The Problem

Q-learning is one of the most popular reinforcement learning algorithms, but it's
known to sometimes learn unrealistically high action values because it includes a 
maximization step over estimated action values, which tends to prefer overestimated 
to underestimated values.

In previous work, overestimations have been attributed to insufficienlty flexable 
function approximation and noise. This paper unifies these views and shows that 
overestimations can occur when the action values are inaccurate, irrespective of the
source of approximation error. Overoptimistic value estimates are not necessarily a
problem in and of themselves. If all values would be uniformly higher then the relative
action preferences are preserved and we'd not expect the resulting policy to be any 
worse.

Optimism in the face of uncertainty is a well-known exploration technique. If, however,
the overestimations are not uniform and not concentrated at states about which we wish
to learn more, then they might negetivly affect the quality of the resulting policy

DQN is used to test whether overestimations occur in practice and at scale. This setting
is the best-case scenario for Q-learning, because the deep neural network provides
flexible function approximation with the potential for low asymptotic approximation
error, and the determinism of the environments prevents the harmful effects of noise.
Even is this comparatively favorable setting, DQN sometimes substantially overestimates the
values of the actions.

# The solution

In the reinforcement learning settings, the agent's sole purpose is to learn estimates
for the optimal value of each action, defined as expected sum of future rewards when
taking that action and following the optimal policy thereafter. Under a given policy
, the true value of action a in a state s is,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/45774418-27bcfa00-bc4d-11e8-8dd7-35bcf5cb904f.png"/>
</p>

An optimal policy is easily derived from the optimal values by selecting the highest
valued action in each state. Estimates for the optimal action values can be learned
using Q-learning. We can a parametrized value function Q(s, a: ) instead of tabular one
to solve really large and interesting problems. The standard Q-learning update for the
parameteres after taking and action in current state and observing the immediate reward
and the resulting state is,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/45774810-466fc080-bc4e-11e8-8600-83edb03c8c3c.png"/>
</p>

where alpha is a scalar step size and the target Y is defined as,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/45774859-6acb9d00-bc4e-11e8-9c17-b48050fe1f52.png"/>
</p>

Two important ingredients of the DQN algorithm  are the use of a target network, and
the use of experience replay. The target network, with parameters minused theta, is the
same as the onine network except that its parameters are copied every tao steps from the oblone
network, and kept fixed on all other steps. The target used by DQN is then,

<p align="center">
<img src ="https://user-images.githubusercontent.com/19307995/45775091-0e1cb200-bc4f-11e8-88c9-1ad04efcf389.png"/>
</p>

For experience replay, observed transitions are stored for some time and sampled uniformly f
from this memory bank to update  the network. For more details on the DQN, you can read the summary of the original paper.





