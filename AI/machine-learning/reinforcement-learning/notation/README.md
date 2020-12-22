
# Notation for Reinforcement Learning

- Capital letters are used for random variables and major algorithm variables.
- Lower case letters are used for the values of random variables and for scalar functions.
- Bold and lowoers letters are required to be real-valued vectors.

| Notation | Meaning|
| :-- | :---------------------------------|
| ![s](http://latex.codecogs.com/svg.latex?s)| state |
| ![a](http://latex.codecogs.com/svg.latex?a)  | action |
| ![S](http://latex.codecogs.com/svg.latex?\mathcal{S})  | set of all nonterminal states|
| ![S^+](http://latex.codecogs.com/svg.latex?\mathcal{S}^+)  | set of all states, including the terminal state|
| ![A(s)](http://latex.codecogs.com/svg.latex?\mathcal{A}(s)) | set of actions possible in states|
| ![R](http://latex.codecogs.com/svg.latex?\mathcal{R}) | set of possible rewardstdiscrete time step|
| | |
| ![t](http://latex.codecogs.com/svg.latex?t)| discrete time step|
| ![T](http://latex.codecogs.com/svg.latex?T) | final time step of an episode|
| ![S_t](http://latex.codecogs.com/svg.latex?S_t)| state at ![](http://latex.codecogs.com/svg.latex?t) |
| ![A_t](http://latex.codecogs.com/svg.latex?A_t) | action at ![](http://latex.codecogs.com/svg.latex?t) |
| ![R_t](http://latex.codecogs.com/svg.latex?R_t) | reward at ![](http://latex.codecogs.com/svg.latex?t) |
| ![G_t](http://latex.codecogs.com/svg.latex?G_t) | return (cumulative discounted reward) following ![](http://latex.codecogs.com/svg.latex?t)|
| ![](http://latex.codecogs.com/svg.latex?G_t^{(n)})| ![](http://latex.codecogs.com/svg.latex?n)-step return|
| ![](http://latex.codecogs.com/svg.latex?G_t^\lambda)| ![](http://latex.codecogs.com/svg.latex?\lambda)-return |
| | |
| ![](http://latex.codecogs.com/svg.latex?\pi)|policy, decision-making rule |
| ![](http://latex.codecogs.com/svg.latex?\pi(s))| action taken in states under ![](http://latex.codecogs.com/svg.latex?deterministic) policy ![](http://latex.codecogs.com/svg.latex?\pi)|
| ![](http://latex.codecogs.com/svg.latex?\pi(a{\mid}s)) | probability of taking action ![](http://latex.codecogs.com/svg.latex?a) in state ![](http://latex.codecogs.com/svg.latex?s) under ![](http://latex.codecogs.com/svg.latex?stochastic) policy ![](http://latex.codecogs.com/svg.latex?\pi) |
| ![](http://latex.codecogs.com/svg.latex?p(s',r{\mid}s,a)) | probability of transitioning to state ![](http://latex.codecogs.com/svg.latex?s'), with reward ![](http://latex.codecogs.com/svg.latex?r), from ![](http://latex.codecogs.com/svg.latex?s,a)|
| ![](http://latex.codecogs.com/svg.latex?v_{\pi}(s)) | value of state ![](http://latex.codecogs.com/svg.latex?s) under policy ![](http://latex.codecogs.com/svg.latex?\pi) (expected return)|
| ![](http://latex.codecogs.com/svg.latex?v_{\ast}(s)) | value of state ![](http://latex.codecogs.com/svg.latex?s) under the optimal policy |
| ![](http://latex.codecogs.com/svg.latex?q_{\pi}(s,a)) | value of taking action ![](http://latex.codecogs.com/svg.latex?a) in state ![](http://latex.codecogs.com/svg.latex?s) under policy ![](http://latex.codecogs.com/svg.latex?\pi) |
| ![](http://latex.codecogs.com/svg.latex?q_{\ast}(s,a)) | value of taking action ![](http://latex.codecogs.com/svg.latex?a) in state ![](http://latex.codecogs.com/svg.latex?s) under the optimal policy |
| ![](http://latex.codecogs.com/svg.latex?V_t(s)) | estimate (a random variable) of ![](http://latex.codecogs.com/svg.latex?v_{\pi}(s)) or ![](http://latex.codecogs.com/svg.latex?v_{\ast}(s)) |
| ![](http://latex.codecogs.com/svg.latex?Q_t(s,a)) | estimate (a random variable) of ![](http://latex.codecogs.com/svg.latex?q_{\pi}(s,a)) or ![](http://latex.codecogs.com/svg.latex?q_{\ast}(s,a)) |
|||
| ![](http://latex.codecogs.com/svg.latex?{\hat{v}(s,\bold{w})) | approximate value of state ![](http://latex.codecogs.com/svg.latex?s) given ![](http://latex.codecogs.com/svg.latex?a) vector of weights ![](http://latex.codecogs.com/svg.latex?\bold{w})|
| ![](http://latex.codecogs.com/svg.latex?{\hat{q}(s,a,\bold{w})) | approximate value of state-action pair ![](http://latex.codecogs.com/svg.latex?s), ![](http://latex.codecogs.com/svg.latex?a) given weights ![](http://latex.codecogs.com/svg.latex?\bold{w})|
| ![](http://latex.codecogs.com/svg.latex?\bold{W},\bold{w}_t) | vector of (possibly learned) ![](http://latex.codecogs.com/svg.latex?weights) underlying an approximate value function |
| ![](http://latex.codecogs.com/svg.latex?\bold{x}(s)) | vector of features visible when in state ![](http://latex.codecogs.com/svg.latex?s) |
| ![](http://latex.codecogs.com/svg.latex?\bold{w}^{\top}\bold{x}) | inner product of vectors, ![](http://latex.codecogs.com/svg.latex?\bold{w}^{\top}\bold{x}=\sum_iw_ix_i); e.g., ![](http://latex.codecogs.com/svg.latex?\hat{v}(s,\bold{w})=\bold{w}^{\top}\bold{x}(s))| 
| ![](http://latex.codecogs.com/svg.latex?\delta_t) | temporal-difference error at ![](http://latex.codecogs.com/svg.latex?t) (a random variable, even though not upper case) |
| ![](http://latex.codecogs.com/svg.latex?E_t(s)) | eligibility trace for state ![](http://latex.codecogs.com/svg.latex?s) at ![](http://latex.codecogs.com/svg.latex?t) |
| ![](http://latex.codecogs.com/svg.latex?E_t{(s,a)}) | eligibility trace for a state-action pair |
| ![](http://latex.codecogs.com/svg.latex?\bold{e}_t) | eligibility trace vector at ![](http://latex.codecogs.com/svg.latex?t) |
|||
| ![](http://latex.codecogs.com/svg.latex?\gamma) | discount-rate parameter |
| ![](http://latex.codecogs.com/svg.latex?\varepsilon) | probability of random action in ![](http://latex.codecogs.com/svg.latex?\varepsilon)-greedy policy |
| ![](http://latex.codecogs.com/svg.latex?\alpha,\beta) | step-size parameters |
| ![](http://latex.codecogs.com/svg.latex?\lambda) | decay-rate parameter for eligibitity traces|
