
#Notation for Reinforcement Learning

- Capital letters are used for random variables and major algorithm variables.
- Lower case letters are used for the values of random variables and for scalar functions.
- Bold and lowoers letters are required to be real-valued vectors.



| Notation | Meaning|
| :-- | :---------------------------------|
| ![s](s.md)| state |
| ![a](http://latex.codecogs.com/svg.latex?a)  | action |
| ![S](http://latex.codecogs.com/svg.latex?S)  | set of all nonterminal states|
| ![S^+](http://latex.codecogs.com/svg.latex?S^+)  | set of all states, including the terminal state|
| ![A(s)](http://latex.codecogs.com/svg.latex?A(s)) | set of actions possible in states|
| ![R](http://latex.codecogs.com/svg.latex?R) | set of possible rewardstdiscrete time step|
| | |
| ![t](http://latex.codecogs.com/svg.latex?t)| discrete time step|
| ![T](http://latex.codecogs.com/svg.latex?T) | final time step of an episode|
| ![S_t](http://latex.codecogs.com/svg.latex?S_t)| state at t |
| ![A_t](http://latex.codecogs.com/svg.latex?A_t) | action at t |
| ![R_t](http://latex.codecogs.com/svg.latex?R_t) | reward at t |
| ![G_t](http://latex.codecogs.com/svg.latex?G_t) | return (cumulative discounted reward) following t|
| ![](http://latex.codecogs.com/svg.latex?G_t^{(n)})| ![](http://latex.codecogs.com/svg.latex?n)-step return|
| ![](http://latex.codecogs.com/svg.latex?G_t^\lambda)| ![](http://latex.codecogs.com/svg.latex?\lambda)-return |
| | |
| ![](http://latex.codecogs.com/svg.latex?\pi)|policy, decision-making rule |
| ![](http://latex.codecogs.com/svg.latex?\pi(s))| action taken in states under ![](http://latex.codecogs.com/svg.latex?deterministic) policy ![](http://latex.codecogs.com/svg.latex?\pi)|
| ![](http://latex.codecogs.com/svg.latex?\pi(a{\mid}s)) | probability of taking action ![](http://latex.codecogs.com/svg.latex?a) in state ![](http://latex.codecogs.com/svg.latex?s) under ![](http://latex.codecogs.com/svg.latex?stochastic) policy ![](http://latex.codecogs.com/svg.latex?\pi) |
| ![](http://latex.codecogs.com/svg.latex?\pi(a{\mid}s)) | probability of transitioning to state ![](http://latex.codecogs.com/svg.latex?s'), with reward
| γ | discount-rate parameter |
(.updating)
