# Reinforcement Learning - Tabular Solution Methods

## Index
- [Multi-arm Bandits](#multi-arm-bandits)
- [Finite Markov Decision Processes](#finite-markov-decision-processes)
- [Dynamic Programming](#dynamic-programming)
- [Monte Carlo Methods](#monte-carlo-methods)
- [Temporal-Difference Learning](#temporal-difference-learning)
- [Eligibility Traces](#eligibility-traces)
- [Planning and Learning with Tabular Methods](#planning-and-learning-with-tabular-methods)
- [References](#references)

## Multi-arm Bandits

Importantly, RL uses training information that _evaluates_ the actions taken rather than _instructs_ by giving correct actions. This is what creates the need for active exploration, for an explicit trial-and-error search for good behavior.

|Comparison | Evaluative Feedback | Instructive Feedback |
|---|---|---|
|Relationship with the action taken | Depends entirely on it | Independently of it |
| Usage | The basis of methods for function optimization, including evolutionary methods | The basis of supervised learning, as pattern classification, artificial neural networks and system identification|

Simpliestly, we use the _nonassociate_ setting does not invole learning to act in more than one situation, in which most prior work involving evaluative feedback has been done, and it avoid much of the complexity of the full RL problem. Studying this case will enable us to see most clearly how evaluatiive feedback differs from, and yet can be combined with, instructive feedback.

### An n-Armed bandit

You are faced repeatedly with a choice among *n* different actions. After each choice you receive a numerical reward chosen from a stationary probability distribution that depends on the action you selected. Your objective is to maximize the expected total reward over some time playing.

Each action has an expected or mean reward given that action is selected, called is _value_ of that action. Assumming that you do not know the action values with certainly , although you may have estimates.
| | Greedy action | Nongreedy action|
|---|---|---|
|Way to estimates of the action values | At any time step always choose one action has greatest estimated value | Choose another action|
|Strategy style | Exploiting | Exploring|
|Reward | Only higher in the short run | Can higher in the long run |

Any single action selection is imposible both to explore and to exloit, it ofter refers to to the conflict between exploration and exploitation. Therefore, we will care the simple ways to balance them.

### Action-Value Methods

We denote the true value of action *a* as *q(a)*, and the estimated value on _t_-th time step as *Q<sub>t</sub>(a)*.

The true value of an action is the mean reward received when that action is selected.

One naive way to estimate this is the _sample-average method_, by averaging the rewards received by _N<sub>t</sub>(a)_ times prior to _t_ before the action was selected.
  
![](http://latex.codecogs.com/svg.latex?Q_t(a)=\frac{R_1+R_2+...+R_{N_t(a)}}{N_t(a)})

If _N<sub>t</sub>(a)_ = 0 , we define default value as _Q<sub>1</sub>(a)_ = 0.\
If _N<sub>t</sub>(a)_ &#8594; &infin;, _Q_<sub>t</sub>(a) &#8594; _q(a)_ (by  the  law  of  large  numbers)

This _greedy_ action selection method can be written as

![](http://latex.codecogs.com/svg.latex?A_t=argmax_aQ_t(a))
  
## Finite Markov Decision Processes

## Dynamic Programming

## Monte Carlo Methods

## Temporal-Difference Learning

## Eligibility Traces

## Planning and Learning with Tabular Methods

## References
