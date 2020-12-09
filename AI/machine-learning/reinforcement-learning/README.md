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
- [Multiarm Bandits](#multiarm-bandits)
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

All RL agents have explicit goals, can sense aspects of their environments, and can choose actions to influence their uncertain environment. 

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

## Multiarm Bandits

### An n-Armed bandit

RL uses training information that **evaluates** the actions taken rather than **instructs** by giving correct actions. You are faced repeatedly with a choice among ![](https://latex.codecogs.com/svg.latex?n) different actions. The original form is one-armed bandit, except that is has ![](https://latex.codecogs.com/svg.latex?n) levers instead of one. Your objective is to maximize the expected total reward over some time playing.

### Action-Value Methods
We denote the true value of action ![](https://latex.codecogs.com/svg.latex?a) as ![](https://latex.codecogs.com/svg.latex?q(a)), and the estimated value on the ![](https://latex.codecogs.com/svg.latex?t)th time step ![](https://latex.codecogs.com/svg.latex?Q_t(a)).

## References
- Practical Reinforcement Learning course, [link](https://www.coursera.org/learn/practical-rl)
- "Reinforcement Learning: An Introduction", 2nd edition, by Richard S. Sutton and Andrew G. Barto. [pdf](https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf)
- "Hands-on Reinforcement Learning with Python", Sudharsan Ravichandiran. [link](https://librariestech.com/category/computer-science/hands-on-reinforcement-learning-with-python-master-reinforcement-and-deep-reinforcement-learning-using-openai-gym-and-tensorflow/)
