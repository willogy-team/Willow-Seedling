# Reinforcement Learning

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Dec 8th, 2020 |
| **Topic(s)** | AI |
| **Status**       | In Progress |

# Index
- [Introduction](#introduction)
- [Motivation](#motivation)
- [Tabular Solution Methods](#tabular-solution-methods)
- [Approximate Solution Methods](#approximate-solution-methods)
- [Frontiers](#frontiers)
- [References](#references)

## Introduction

Reinforcement learning (RL) is an area of machine learning concerned with how software agents ought to take actions in an environment in order to maximize the notion of cumulative reward. Reinforcement learning is one of three basic machine learning paradigms, alongside supervised learning and unsupervised learning.

### Paradigms comparison

|Paradigms | Reinforment learning | Supervised learning | Unsupervised learning |
|:----------| :----------|:----------|:----------|
|Learning method | Learning optimal stategy by trial and error | Learning to approximate reference answers| Learning underlying data structure|
|Need feedback| Do on agent's own actions | Do correct answers | No feedback required|
|Affect the input data |Agent can do| Do not | Do not |

### Notation

Directing to [Notation](notation/notation.md)

## Motivation

One of the challenges in RL is the trade-off between **exploration** and **exploitation**. The agent has to **exploit** what it already knows in order to obtain reward, but it also **explore** in order to make better action selections in the future. The dilemma is that neither exploration nor exploitation can be pursued exclusively without failing at the task.

All RL agents have explicit goals, can sense aspects of their environments, and can choose actions to influence their uncertain environment that even if all the details of complete agent can not yet filled in.


### Elements of RL

Four main subelements of a RL system: a **policy**, a **reward signal**, a **value function**, and optionally, a **model** of the environment.

- A **policy** defines the learning agent's way of behaving at a given time, that is a mapping from perceived states of the environment to actions to be taken when in those states. In general, policies may be stochastic.
- A **reward signal** defines the goal in a RL problem. On each time step, the environment sends to the agent a single number (a **reward**). The agent's sole objective is to maximize the total reward it receives over the long run. The reward what is the good or bad event for the agent.
- A **value function** defines what is good in the long run, differrently the reward signal indicates what is good in an immediate sense. It is the total amount of reward an agent can expect to accumulate over the future starting form one state.
- A **model** of the environment is someting that mimics the behavior of the environment. Models are used for **planning** to predict the resultant next state and next reward.

### History 

Two independent main threads of RL are **trial-and-error learning** and **optimal control**.
- **Trial-and-error learning** stated in the psychology of animal learning.
- **Optimal control** using value functions and dynamic programming.

## Tabular Solution Methods
The simplest forms in which the state and action spaces are small enough for the approximate action-value function to be represented as an array, or _table_. In this case, the methods can often find exact solutions, that is the optimal value function and the optimal policy.
Direct to [Tabular Solution Methods](tabular-solution-methods)

## Approximate Solution Methods
This contracts with the tabular solution methods, the approximate solution methods only find approximate solutions. But which in return can be applied effectively to much larger problems.
Direct to [Approximate Solution Methods](approximate-solution-methods)

## Frontiers
Direct to [Frontiers](frontiers)

## References
- Practical Reinforcement Learning course, [link](https://www.coursera.org/learn/practical-rl)
- "Reinforcement Learning: An Introduction", 2nd edition, by Richard S. Sutton and Andrew G. Barto. [pdf](https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf)
- "Hands-on Reinforcement Learning with Python", Sudharsan Ravichandiran. [link](https://librariestech.com/category/computer-science/hands-on-reinforcement-learning-with-python-master-reinforcement-and-deep-reinforcement-learning-using-openai-gym-and-tensorflow/)
