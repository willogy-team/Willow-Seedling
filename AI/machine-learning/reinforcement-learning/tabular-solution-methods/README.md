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

### The Agent-Environment Interface

The RL problem is meant to be a straightforward framing of the problem of learning from interaction to achieve a goal. 
- The learner and decision-maker is called the **agent**.
- The thing it iteracts with, comprising everything outside the agent, is called the **environment**.
- The agent selecting actions and the environment responding to those actions and presenting new situations to the agent.
- The environment gives rise to numerical rewards that the agent tries to maximize over time.

![](images/Figure3.1.png)

Specifically, the agent and environment interact at each of a sequence of discreate time steps, _t_ = 0, 1, 2, 3,...
- At each time step _t_,
  - The agent receives some representation of the environment's **state**, ![](http://latex.codecogs.com/svg.latex?S_t\in\mathcal{S}), where ![](http://latex.codecogs.com/svg.latex?\mathcal{S}) is the set of possible states.
  - Basic selects an **action**, ![](http://latex.codecogs.com/svg.latex?A_t\in\mathcal{A}(S_t)), where ![](http://latex.codecogs.com/svg.latex?\mathcal{A}(S_t)) is the set of actions avaible in state ![](http://latex.codecogs.com/svg.latex?S_t).
- One time step later,
  - The agent receives a numerical **reward**, ![](http://latex.codecogs.com/svg.latex?R_{t+1}\in\mathcal{R}\subset\mathbb{R}).
  - Finds itself in a new state, ![](http://latex.codecogs.com/svg.latex?S_{t+1}).

At each time step, a mapping implemented from states to probabilities of selecting each possible action by the agent what is called the agent's **policy**. It is denoted _&pi;<sub>t</sub>_ where _&pi;<sub>t</sub>_(_a_|_s_) is the probability that _A<sub>t</sub>_ = _a_ if _S<sub>t</sub>_ = _s_. RL methods specify how the agent changes its policy as a result of experience to maximize the total amount of reward it receives over the long run.

The boundary between agent and environment is not often the same as the physical boundary of a robot's or animal's body. It is determined once one has selected particular states, actions, and rewards, and thus has identified a specific decision-making task of interset.

The RL framework is a considerable abstraction of the problem of goal-directed learning from interaction. It proposes that whatever the details of the sensory, memory and control apparatus, and whatever objective one is trying to achieve, any problem of learning goal-directed behavior can be reduced to three signals passing back and forth between an agent and its environment:
- One signal a.k.a an action to represent the choices made by the agent.
- One signal a.k.a an state to represent the basis on which the choices are made.
- One signal a.k.a an reward to define the agent's goal.

### Goals and Rewards

At each time step, the **reward** is a simple number, ![](http://latex.codecogs.com/svg.latex?R_t\in\mathbb{R}). The agent's **goal** is to maximize the total amount of reward it receives by cumulate reward in the long run, do not immediate reward.

### Returns

The (expected) **return** is the sum of the rewards that received after time step _t_ is denoted _R<sub>t+1</sub>, R<sub>t+2</sub>, R<sub>t+3</sub>,..._:
![](http://latex.codecogs.com/svg.latex?G_t=R_{t+1}+R_{t+2}+R_{t+3}+...+R_T)

where ![](http://latex.codecogs.com/svg.latex?T) is a final time step.
- From starting to when the agent-environment interaction breaks naturally into subsequences, it is **episodes**.
- Each episode ends in a special state is **terminal state**.
- Tasks with episodes of this kind are called **episodic tasks**. In episodic tasks sometimes need to distinguish the set of all nonterminal states as ![](http://latex.codecogs.com/svg.latex?\mathcal{S}), from the set of all states plus the terminal state as ![](http://latex.codecogs.com/svg.latex?\mathcal{S}^{+})

In many cases the agent-enviromnment interaction does not break naturally into identifiable episodes, it goes on continually without limit. We call these **continuing tasks**.The final time step would be _T_ = &infin;, and the return, which is problematicly what we are trying to maximize, could itself easily be infinite. 

The agent tries to select actions so that the sum of the discounted rewards it receives over the future is maximized. In particular, it chooses _A<sub>t</sub>_ to maximize the expected **discounting return**:

![](https://latex.codecogs.com/svg.latex?G_t=R_{t+1}+{\gamma}R_{t+2}+{\gamma^2}R_{t+3}+...=\sum_{k=0}^{\infty}{\gamma}^{k}R_{t+k-1})

where &gamma; is a parameter, 0 &le; &gamma; &le; 1, called the **discount rate**.

The discount rate determines the present value of future rewards.
- If &gamma; < 1, the infinite sum has a finite value as long as the reward sequence {_R_<sub>k</sub>} is bounded.
- If &gamma; = 0, the agent is myopic in being concerned only with maximizing immediate rewards.
- If &gamma approachs 1, the objective takes future rewards into account more strongly, the agent becomes more farsighted.

### The Markov Property

The markov property is a property of environments and their state signals that is of particular interest. We treat the state as information is available to the agent. It is importantly given by some preprocessing system, but we focus fully on the decision-making issues rather than onstructing, changing, or learning the state signal. 

The state signal should be not be expected to inform the agent of everything about environment, or even everything that would be useful to it in making decisions.
Ideadlly, is a state signal that summarizes past sensations compactly, yet in such a way that all relevant information is retained. A state signal that succeeds in retaining all relevant information is said to be **Markov**.

Formally define the Markov property for the RL problem with a assumely finite number of states and reward values. Consider how a general environment might respond at time _t_ + 1 to the action taken at time _t_. In the most general, causal case this response may depend on everything that has happended earlier. In this case the dynamics can be defined only by specifying the complete probability distribution:

![](https://latex.codecogs.com/svg.latex?Pr\\{R_{t+1}=r,S_{t+1}=s'|S_0,A_0,R_1,...,S_{t-1},A_{t-1},R_t,S_t,A_t\\})

for all _r_, _s'_, and all possible values of the past events: _S<sub>0</sub>, A<sub>0</sub>, R<sub>1</sub>, ..., S<sub>t-1</sub>, A<sub>t-1</sub>, R<sub>t</sub>, S<sub>t</sub>, A<sub>t</sub>_. If the state signal has the **Markov property**, on the other hand, then the environment's respone at _t_ + 1 depends only on the state and action represetations at _t_, in which case the environment's dynamics can be defined by specifying only

![](https://latex.codecogs.com/svg.latex?p(s',r|s,a)=Pr\\{R_{t+1}=r,S_{t+1}=s'|S_t,A_t\\})

for all _r_, _s'_, _S_<sub>t</sub>, _A_<sub>t</sub>.

If an environment has the Markov property, then its one-step dynamics enable us to predict the next state and expected next reward given the current state and action. Even when the state signal is non-Markov it is still appropriate to think of the state in RL as an approximation to a Markov state.

### Markov Decision Processes

A RL task that satisfies the Markov property is called a **Markov decision process**, or MDP. If the state and action spaces are finite then it is called a **finite MDP** that are particularly important to the theory of RL.

A particular finite MDP is defined by its state and action sets and by the one-step dynamics of the environment. Given any state _s_ and action _a_, the probability of each possible pair of the next state and reward, _s'_, _r_, is denoted

![](https://latex.codecogs.com/svg.latex?p(s',r|s,a)=Pr\\{S_{t+1}=s',R_{t+1}=r|S_t=s,A_t=a\\})

Given the dynamics as specified by above, one can compute anything else one might want to know about the environment, such as:

| value | formula|
|:--|:--|
| the expected rewards for state-action pairs | ![](https://latex.codecogs.com/svg.latex?r(s,a)=\mathbb{E}\\[R_{t+1}\\|S_t=s,A_t=a\\]=\sum_{r\in\mathcal{R}}r\sum_{s'\in\mathcal{S}}p(s',r\\|s,a))|
| the state-transition probabilities | ![](https://latex.codecogs.com/svg.latex?p(s'\\|s,a)=Pr\\{S_{t+1}=s'\\|S_t=s,A_t=a\\}=\sum_{r\in\mathcal{R}}p(s',r\\|s,a))|
| the expected rewards for state-action-next_state triples | ![](https://latex.codecogs.com/svg.latex?r(s,a,s')=\mathbb{E}\\[R_{t+1}\\|S_t=s,A_t=a,S_{t+1}=s'\\]=\frac{\sum_{r\in\mathcal{R}}r{\space}p(s',r\\|s,a)}{p(s'\\|s,a)})|

### Value Functions
Almost all RL algorithms involve estimating **value functions** - functions of states (or of state-action pairs) that estimate _how good_ it is for the agent to be in a given state (or how good it is to perform a given action in a given state). Of course the rewards the agent can expect to receive in the future depend on what actions it will take. Accordingly, value functions are defined with respect to particular policies.

A policy ![](https://latex.codecogs.com/svg.latex?\pi), is a mapping from each state ![](https://latex.codecogs.com/svg.latex?s\in\mathcal{S}) and action ![](https://latex.codecogs.com/svg.latex?a\in\mathcal{A}(s)), to the probability ![](https://latex.codecogs.com/svg.latex?\pi(a|s)) of taking action ![](https://latex.codecogs.com/svg.latex?a) when in state ![](https://latex.codecogs.com/svg.latex?s). Informally the **value** of a state ![](https://latex.codecogs.com/svg.latex?s) under a policy ![](https://latex.codecogs.com/svg.latex?\pi), denoted ![](https://latex.codecogs.com/svg.latex?v_{\pi}(s)), is the expected return when starting in ![](https://latex.codecogs.com/svg.latex?s) and following ![](https://latex.codecogs.com/svg.latex?\pi) thereafter. For MDPs, we can define it formally as

![](https://latex.codecogs.com/svg.latex?v_{\pi}(s)=\mathbb{E}_{\pi}\\[G_t|S_t=s\\]=\mathbb{E}_{\pi}{\Bigg[}\sum_{k=0}^{\infty}{\gamma}^{k}R_{t+k+1}{\Bigg|}S_t=s{\Bigg]})

where ![](https://latex.codecogs.com/svg.latex?\mathbb{E}\\[\cdot\\]) denotes the expected value of a random variable given that agent folows policy ![](https://latex.codecogs.com/svg.latex?\pi), and ![](https://latex.codecogs.com/svg.latex?t) is any time step. Note that the value of the terminal state, if any, is always zero. The function ![](https://latex.codecogs.com/svg.latex?v_\pi) the **state-value function** for policy ![](https://latex.codecogs.com/svg.latex?\pi).

The value of taking action ![](https://latex.codecogs.com/svg.latex?a) in state ![](https://latex.codecogs.com/svg.latex?s) under a policy ![](https://latex.codecogs.com/svg.latex?\pi), denoted ![](https://latex.codecogs.com/svg.latex?q_\pi(s,a)), as the expected return starting from ![](https://latex.codecogs.com/svg.latex?s), taking the action ![](https://latex.codecogs.com/svg.latex?a), and thereafter following policy ![](https://latex.codecogs.com/svg.latex?\pi):

![](https://latex.codecogs.com/svg.latex?q_{\pi}(s)=\mathbb{E}_{\pi}\\[G_t|S_t=s,A_t=a\\]=\mathbb{E}_{\pi}{\Bigg[}\sum_{k=0}^{\infty}{\gamma}^{k}R_{t+k+1}{\Bigg|}S_t=s,A_t=a{\Bigg]})

where ![](https://latex.codecogs.com/svg.latex?q_{\pi}) is the **action-value function** for policy ![](https://latex.codecogs.com/svg.latex?\pi).

The value functions ![](https://latex.codecogs.com/svg.latex?v_{\pi}) and ![](https://latex.codecogs.com/svg.latex?q_{\pi}) can be estimated from experience. 

A fundamental property of value functions used throughout RL and dynamic programming is that they satisfy particular recursive relationships. For any policy ![](https://latex.codecogs.com/svg.latex?\pi) and any state ![](https://latex.codecogs.com/svg.latex?s), the following consistency condition holds between the value of ![](https://latex.codecogs.com/svg.latex?s) and the value of its possible successor states:

![](https://latex.codecogs.com/svg.latex?v_{\pi}(s)=\mathbb{E}_{\pi}{\\[}G_t|S_t=s{\\]}=\sum_{a}\pi(a|s)\sum_{s',r}p(s',r|s,a)\big[r+{\gamma}v_\pi(s')\big])

where it is implicit that the actions, ![](https://latex.codecogs.com/svg.latex?a), are taken from the set ![](https://latex.codecogs.com/svg.latex?\mathcal{A}(s)), the next states, ![](https://latex.codecogs.com/svg.latex?s'), are taken from the set ![](https://latex.codecogs.com/svg.latex?\mathcal{S}) (or from ![](https://latex.codecogs.com/svg.latex?\mathcal{S}^{+}), and the rewards, ![](https://latex.codecogs.com/svg.latex?r), are taken from the set ![](https://latex.codecogs.com/svg.latex?\mathcal{R}). It is really a sum over all values of the three variables, ![](https://latex.codecogs.com/svg.latex?a), ![](https://latex.codecogs.com/svg.latex?s'), and ![](https://latex.codecogs.com/svg.latex?r). For each triplet, we compute its probability, ![](https://latex.codecogs.com/svg.latex?\pi(a|s)p(s',r|s,a)), weight the quantity in brackets by that probability, then sum over all possibilities to get an expected value.

That equation is the **Bellman equation** for ![](https://latex.codecogs.com/svg.latex?v_\pi). It expresses a relationship between the value of a state and the values of its successor states. Think of looking ahead from one state to its possible successor states, as suggested by Figure a. Each open circle represents a state and each solid circle represents a state-action pair. Starting from state ![](https://latex.codecogs.com/svg.latex?s), the root node at the top, agent could take any of some set of actions. From each of these, the environment could respond with one of several next states, ![](https://latex.codecogs.com/svg.latex?s'), along with a reward, ![](https://latex.codecogs.com/svg.latex?r). The Bellman equation averages over all the possibilities, weighting each by its probability of occuring. It states that the value of the start state musl equal the (discounted) value of the expected next state, plus the reward expected along the way.
![](images/Figure3.4.png)

Figure: Backup diagrams for (a) ![](https://latex.codecogs.com/svg.latex?v_\pi) and (b) ![](https://latex.codecogs.com/svg.latex?q_\pi).

### Optimal Value Fuctions

Solving a RL task means, roughly, finding a policy that achieves a lot of reward over the long run. For finite MDPs, we can precisely define an optimal policy in the following way. Value functions define a partial ordering over policies. A policy ![](https://latex.codecogs.com/svg.latex?\pi) is defined to be better than or equal to a policy ![](https://latex.codecogs.com/svg.latex?\pi') if its expected return is greater than or equal to that of ![](https://latex.codecogs.com/svg.latex?\pi') for all states. In other words, ![](https://latex.codecogs.com/svg.latex?\pi\geq\pi') if and only if ![](https://latex.codecogs.com/svg.latex?v_\pi(s){\geq}v_{\pi'}(s)) for all ![](https://latex.codecogs.com/svg.latex?s\in\mathcal{S}). There is always at least one policy that is better than or equal to all other policies. This is an **optimal policy**.

Although there may be more than one, we denote all the optimal policies by ![](https://latex.codecogs.com/svg.latex?\pi_{*}). They share the same functions as below:
| The optimal function | Denotation and Definition | For all values |
|:--|:--|:--|
| The **optimal state-value function** | ![](https://latex.codecogs.com/svg.latex?v_{*}(s)=\max_{\pi}v_{\pi}(s))| ![](https://latex.codecogs.com/svg.latex?s\in\mathcal{S})|
| The **optimal action-value function** | ![](https://latex.codecogs.com/svg.latex?q_{*}(s,a)=\max_{\pi}q_{\pi}(s,a))| ![](https://latex.codecogs.com/svg.latex?s\in\mathcal{S}{\land}a\in\mathcal{A}(s))|

For the state-action pair ![](https://latex.codecogs.com/svg.latex?(s,a)), the optimal action-value function gives the expected return for taking action ![](https://latex.codecogs.com/svg.latex?a) in state ![](https://latex.codecogs.com/svg.latex?s) and thereafter following an optimal policy. Thus, we can write ![](https://latex.codecogs.com/svg.latex?q_*) in terms of ![](https://latex.codecogs.com/svg.latex?v_*) as follows:

![](https://latex.codecogs.com/svg.latex?q_*(s,a)=\mathbb{E}\\[R_{t+1}+{\gamma}v_*(S_{t+1})|S_t=s,A_t=a\\])

The Bellman optimality equation expresses the fact that the value of a state under an optimal policy must equal the expected return for the best action from that state:

![](https://latex.codecogs.com/svg.latex?\begin{multline}v_*(s)=\max_{a\in\mathcal{A}(s)}q_{\pi_*}(s,a)\\\\=\max_{a}\mathbb{E}\\[R_{t+1}+{\gamma}v_*(S_{t+1})|S_t=s,A_t=a\\]\\\\=\max_{a\in\mathcal{A}(s)}\sum_{s',r}p(s',r|s,a)\\[r+{\gamma}v_*(s')\\]\end{multline})

The Bellman optimality equation for ![](https://latex.codecogs.com/svg.latex?q_*) is:

![](https://latex.codecogs.com/svg.latex?\begin{multline}q_*(s,a)=\mathbb{E}\\[R_{t+1}+{\gamma}\max_{a'}(S_{t+1},a')|S_t=s,A_t=a\\]\\\\=\sum_{s',r}p(s',r|s,a)\\[r+{\gamma}\max_{a'}q_*(s',a')\\]\end{multline})

The backup diagrams in Figure below show graphically the spans of future states and actions considered in the Bellman optimality equations for ![](https://latex.codecogs.com/svg.latex?v_*) and ![](https://latex.codecogs.com/svg.latex?q_*). These are the same as the backup diagrams for ![](https://latex.codecogs.com/svg.latex?v_\pi) and ![](https://latex.codecogs.com/svg.latex?q_\pi) except that arcs have been added at the agent's choice points to represent that the maximum over that choice is taken rather than the expected value given some policy.

![](images/Figure3.7.png)

Figure: Backup diagrams for (a) ![](https://latex.codecogs.com/svg.latex?v_*) and (b) ![](https://latex.codecogs.com/svg.latex?q_*)

Once one has ![](https://latex.codecogs.com/svg.latex?v_*), it is relatively easy to determine an optimal policy. For each state ![](https://latex.codecogs.com/svg.latex?s), there will be one or more actions at which the maximum is obtained in the Bellman optimality equation. Any policy that assigns nonzero probability only to these actions is an optimal policy. You can think of this as a one-step search. If you have the optimal value function, ![](https://latex.codecogs.com/svg.latex?v_*), then the actions that appear best after a one-step search will be optimal actions **greedily**. Although, the policies select actions based only on their short-term consequences, the beauty of ![](https://latex.codecogs.com/svg.latex?v_*) is actually optimal in longterm sense because ![](https://latex.codecogs.com/svg.latex?v_*) already takes into account the reward consequences of all possible future behavior. By means of ![](https://latex.codecogs.com/svg.latex?v_*), the optimal expected long-term return is turned into a quantity that is locally and immediately avaible for each state. Hence, a one-step-ahead search yields the long-term optimal actions. 

Having ![](https://latex.codecogs.com/svg.latex?q_*) makes choosing optimal actions still easier. With ![](https://latex.codecogs.com/svg.latex?q_*), the agent does not even have to do a one-step-ahead search: for any state ![](https://latex.codecogs.com/svg.latex?s), it can simply find any action that maximizes ![](https://latex.codecogs.com/svg.latex?q_*(s,a)). The action-value function effectively caches the results of all one-step-ahead searches. It provides the optimal expected long-term return as a value that is locally and immediately available for each state-action pair. Hence, at the cost of representing a function of state-action pairs, instead of just of states, the optimal action-value function allows optimal actions to be selected without having to know anything about possible successor states and their values, that is, without having to know anything about the environment's dynamics.

### Optimality and Approximation

A critical aspect of the problem facing the agent is always the computational power available to it, in particular, the amount of computation it can perform in a single time step.

The memory avaible is also an important constraint. A large amount of memory is often required to build up approximations of value functions, policies, and models. In tasks with small, finite state sets, it is possible to form these approximations using arrays or tables with one entry for each state (or state-action pair). This we call the **tabular** case, the corresponding methods we call tabular methods. 

## Monte Carlo Methods

## Temporal-Difference Learning

## Eligibility Traces

## Planning and Learning with Tabular Methods

## References
