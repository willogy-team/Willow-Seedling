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

### Optimistic Initial Values
All the above methods are dependent to some extent on the initial action-value estimates, _Q<sub>1</sub>(a)_. Statistically, these methods are _biased_ by their initial estimates.

In pratice, this kind of bias is usually not a problem, and can sometimes be very helpful. The downside is that the initial estimates become, in effect, a set of paremeters that must be picked by the user, if only to set them all to zero. The upside is that they provide an easy way to supply some prior knowledge about what level of rewards can be expected.

This optimism encourages action-value methods to explore. Initially, the optimistic method performs worse because it explores more, but eventually it performs better because its exploration decreases with time.
![](images/Figure2.2.png)

### Upper-Confidence-Bound Action Selection

Exploration is needed because the estimates of the action values are uncertain. The greedy actions are those that look best at present, but some of the other actions may really be better. &epsilon;-greedy action selection forces the non-greedy actions to be tried indiscriminately, with no preference for those that are nearly greedy or particularly uncertain. One effective way of doing this is to select actions as

![](https://latex.codecogs.com/svg.latex?A_t=argmax_a\Bigg[Q_t(a)+c\sqrt{\frac{lnt}{N_t(a)}}\Bigg])

where ln _t_ denotes the natural logarithm of _t_, and the number _c_ > 0 controls the degree of exploration. If _N<sub>t</sub>(a)_ = 0, then _a_ is considered to be a maximizing action.

![](images/Figure2.3.png)

The idea of this _upper confidence bound_ (_UCB_) action selection is that the square-root term is a measure of the uncertainty or variance in the estimate of _a_'s value. Each time _a_ is selected the uncertainty is presumably reduced; _N<sub>t</sub>(a)_ is incremented and, the term is descreased. Each time an action other _a_ is selected _t_ is increased, this term is increased too. The use of the natural logarithm means that the increase gets smaller over time, but is  unbounded; all actions will eventually be selected, but as time goes by it will be a longer wait.

In these more advanced settings there is currently no known practicalway of utilizing the idea of UCB action selection.

### Gradient Bandits
We consider learning a numerical _preference_ H<sub>t</sub>(a) for each action _a_. The larger the preference, the more often that action is taken, but it has no interpretation in terms of reward.

![](https://latex.codecogs.com/svg.latex?Pr\big\\{A_t=a\big\\}=\frac{e^{H_t(a)}}{\sum_{b=1}^ne^{H_t(b)}}=\pi_t(a))

The probability of taking action _a_ at time _t_, which are determined according to a soft-max distribution. Initially, all preferences are the same so that all actions have an equal probability of being selected.

There is a natural learning algorithm for this setting based on the idea of stochastic gradient ascent. On each step, after selecting the action _A<sub>t</sub>_ and receiving the reward _R<sub>t</sub>_, them are updated by:

![](https://latex.codecogs.com/svg.latex?H_{t+1}(A_t)=H_t(A_t)+\alpha(R_t-\bar{R}_t)(1-\pi_t(A_t))), and\
![](https://latex.codecogs.com/svg.latex?H_{t+1}(a)=H_t(a)-\alpha(R_t-\bar{R}_t)\pi_t(a),{\forall}a{\neq}A_t)

where _&alpha;_ > 0 is a step-size parameter, and ![](https://latex.codecogs.com/svg.latex?\bar{R})<sub>t</sub> &in; &reals; is the average of all the rewards up through and including time _t_, which can be computed incrementally above. The ![](https://latex.codecogs.com/svg.latex?\bar{R})<sub>t</sub> term serves as a baseline with which the reward is compared. If the reward is higher than the baselin, then the probability of taking _A<sub>t</sub>_ in the future is increased, and else below then probability is decreased. The non-selected actions move in the opposite direction.

One can gain a deeper insight into this algorithm by understanding it as a stochastic approximation to gradient ascent. Exactly, each preference _H<sub>t</sub>(a)_ would be incrementing proportional to the increment's effect on performance:

![](https://latex.codecogs.com/svg.latex?H_{t+1}(a)=H_t(a)-\alpha\frac{\partial\mathbb{E}\\[R_t\\]}{{\partial}H_t(a))

where the measure of performance here is the expected reward: 

![](https://latex.codecogs.com/svg.latex?\mathbb{E}\\[R_t\\]=\sum_{b}\pi_t(b)q(b))

Of course, it is impossible to implement gradient ascent exactly because by assumption we do not know the _q(b)_, but in fact the updates of the algorithm equally in expected value, making the algorithm an instance of stochastic gradient ascent.

### Associative Search
So far we have considered only nonassociative tasks, in which there is no need to associate different actions with different situations. However, in a general reinforcement learning task there is more than one situation, and the goal is to learn a policy: a mapping from situations to the actions that are best in those situations. To set the stage for the full problem, the simplest way in which nonassociative tasks extend to the associative setting.

### Summary

The simple ways of balanceing exploration and exploitation.
- The &epsilon;-greedy methods choose randomly a small fraction of the time.
- UCB methods choose deterministically, achieve explorationq by subtly favoring at each step the actions that have so far received fewer samples.
- Gradient-bandit algorithms estimate not action values, but action preferences, and favor the more preferred actions in a graded, probabilistic manner using a soft-max distribution.
- The simple expedient of initializing estimates optimistically causes even greedy methods to explore significantly.

![](images/Figure2.5.png)

Despite their simplicity can fairly be considered the state of the art. There are more sophisticated methods, but their complexity and assumptions make them impractical for the full RL problem that is our real focus. However, these methods are far from a fully satisfactory solution to the problem of balancing exploration and exploitation.

## Finite Markov Decision Processes 

## Dynamic Programming

## Monte Carlo Methods

## Temporal-Difference Learning

## Eligibility Traces

## Planning and Learning with Tabular Methods

## References
