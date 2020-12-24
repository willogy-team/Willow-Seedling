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

Simpliestly, we use the _nonassociate_ setting does not involve learning to act in more than one situation, in which most prior work involving evaluative feedback has been done, and it avoid much of the complexity of the full RL problem. Studying this case will enable us to see most clearly how evaluatiive feedback differs from, and yet can be combined with, instructive feedback.

### An n-Armed bandit

You are faced repeatedly with a choice among *n* different actions. After each choice you receive a numerical reward chosen from a stationary probability distribution that depends on the action you selected. Your objective is to maximize the expected total reward over some time playing.

Each action has an expected or mean reward given that action is selected, called is _value_ of that action. Assumming that you do not know the action values with certainty , although you may have estimates.
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

The simplest action selection rule is to select the action with highest estimated action value, to select at step _t_ one of the greedy action, A<sup>\*</sup><sub>t</sub>, for which Q<sub>t</sub>(A<sup>\*</sup><sub>t</sub>) = max<sub>a</sub> Q<sub>t</sub>(a). This _greedy_ action selection method can be written as

![](http://latex.codecogs.com/svg.latex?A_t=argmax_aQ_t(a))

A simple alternative is to behave greedily most of the time, but every once in a while, with small probability &epsilon;, instead to select randomly from amongst all the actions with equal probability independently of the action-value estimates. The calling are _&epsilon;-greedy_ methods.

### Incremental Implementation
The estimate of the value of action _a_ is not really necessary to compute it again. Easily solving it out with incremental update formulas for computing averages with small, constant computation required to process each new reward. For some action, let _Q<sub>k</sub>_ denote the estimate for its _k_-th reward, that is, the average of its first _k - 1_ rewards.

![](http://latex.codecogs.com/svg.latex?Q_{k+1}=\frac{1}{k}\sum_{i=1}^{k}R_i=Q_k+\frac{1}{k}(R_k-Q_k)) 

The update rule is 

![](http://latex.codecogs.com/svg.latex?{NewEstimate}{\leftarrow}OldEstimate+StepSize(Target-OldEstimate))

In processing the _k_-th reward for action _a_, that method uses a step-size parameter of <sup>1</sup>&frasl;<sub>k</sub>. We denote it by the symbol _&alpha;_ or, more generally, by _&alpha;<sub>t</sub>(a)_.

![](http://latex.codecogs.com/svg.latex?Q_{k+1}=Q_k+\alpha(R_k-Q_k)) 

### Tracking a Nonstationary Problem
The step-size parameter _&alpha;_ &in; (0, 1]<sup>1</sup> is constant. The results in _Q<sub>k+1</sub>_ being a weighted average of past rewards and the initial estimate _Q<sub>1</sub>_:

![](http://latex.codecogs.com/svg.latex?Q_{k+1}=Q_k+\alpha(R_k-Q_k)=(1-\alpha)^kQ_1+\sum_{i=1}^k\alpha(1-\alpha)^{k-i}R_i)

We call this a weighted average because the sum of the weights is ![](http://latex.codecogs.com/svg.latex?(1-\alpha)^k+\sum_{i=1}^k\alpha(1-\alpha)^{k-i}=1). The weight decays exponentially according to the exponent on 1 - &alpha;, this is sometimes called an _exponential_, _recency-weighted average_.

Sometimes it is convenient to vary the step-size parameter from step to step. Let _&alpha;<sub>k</sub>(a)_ denote the step-size parameter used to process the reward received after the _k_-th selection of action _a_. The choice _&alpha;<sub>k</sub>(a) = <sup>1</sup>&frasl;<sub>k</sub>_ results in the sample-average method, which is guaranteed to converge to the true action values by the law of large numbers. But of course convergence is not guaranteed for all choices of the sequence _{&alpha;<sub>k</sub>(a)}_. Although these parameters meet the conditions often converge very slowly or need considerable tuning in order to obtain a satisfactory convergence rate. Therefore, they are often used in theoretical work, which are seldom used in applications and empirical research.

## Finite Markov Decision Processes 

## Dynamic Programming

## Monte Carlo Methods

## Temporal-Difference Learning

## Eligibility Traces

## Planning and Learning with Tabular Methods

## References
