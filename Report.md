# Project Report
## Project 2 : Continuous Control

In this report, the model architecture and the steps to solve this particular project is explained. This architecture is able to solve the environment in around 257 steps as shown in the notebook.

## Project Overview

The goal of this project was to train an agent to control a double-jointed arm such that it would track a ball around. As described in the project: A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

## Learning Algorithm

Deep Deterministic Policy Gradient (DDPG) (the algorithm used in this project) builds on DPG but introduces an actor-critic architecture to deal with a large action space (continous or discrete).

DDPG is a policy gradient algorithm that uses a stochastic behavior policy for good exploration but estimates a deterministic target policy, which is much easier to learn. Policy gradient algorithms utilize a form of policy iteration: they evaluate the policy, and then follow the policy gradient to maximize performance. Since DDPG is off-policy and uses a deterministic target policy, this allows for the use of the Deterministic Policy Gradient theorem (which will be derived shortly). DDPG is an actor-critic algorithm as well; it primarily uses two neural networks, one for the actor and one for the critic. These networks compute action predictions for the current state and generate a temporal-difference (TD) error signal each time step. The input of the actor network is the current state, and the output is a single real value representing an action chosen from a continuous action space (whoa!). The critic’s output is simply the estimated Q-value of the current state and of the action given by the actor. The deterministic policy gradient theorem provides the update rule for the weights of the actor network. The critic network is updated from the gradients obtained from the TD error signal.

The Actor-Critic learning algorithm is used to represent the policy function independently of the value function. The policy function structure is known as the actor, and the value function structure is referred to as the critic. The actor produces an action given the current state of the environment, and the critic produces a TD (Temporal-Difference) error signal given the state and resultant reward. If the critic is estimating the action-value function Q(s,a), it will also need the output of the actor. The output of the critic drives learning in both the actor and the critic. In Deep Reinforcement Learning, neural networks can be used to represent the actor and critic structures.

## Network Architecture

2 Fully connected layers with RELU activation was used for both actor critic. Both in the critic and actor network a Batch Normalisation was used in the first hidden layer. Two hidden layers were used with units 128/128.

## Hyperparameters

Hyperparameters used were :

```
BUFFER_SIZE = int(1e5)  # replay buffer size
BATCH_SIZE = 128        # minibatch size
GAMMA = 0.99            # discount factor
TAU = 1e-3              # for soft update of target parameters
LR_ACTOR = 2e-4         # learning rate of the actor 
LR_CRITIC = 2e-4        # learning rate of the critic
WEIGHT_DECAY = 0        # L2 weight decay

```

## Training Plot

The agent was able to solve the environment by achieving score of 30.0 over 100 consecutive episodes after 257 episodes.
![ ](plot.jpg)

## Training Output

```
Episode 100	Average Score: 3.62
Episode 200	Average Score: 20.60
Episode 257	Average Score: 30.05
Environment solved in 257 episodes!	Average Score: 30.05
```

## Future Work 

Further experimnetation on the Network architecture can be done to improve the training time.
