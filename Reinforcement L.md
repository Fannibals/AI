## Reinforcement Learning
### introduction
+ still assume a Markov decision process(MDP)
	- A set fo state s -> S
	- A set of actions (per state) A
	- A model T(s,a,s')
	- A reward function R(s,a,s')
+ still looking for a policy pi(s)
+ New twist: don't know T or R
	- don't know which states are good or what the actions do 

### Offline(MDPs) vs. Online(RL)
+ offline: given the MDP you plan offline find out the optimal policy
+ online: know nothing, learn 

### Model-Based Learning
+ Learn an approximate model based on experiences
+ Solve for values as if the learned model were correct

+ Step 1: Learn empirical MDP model
+ Step 2: Solve the learned MDP

+ Example:
	- T(s,a,s')	: prob
	- R(s,a,s') : reward

## Passive Reinforcement Learning
### Simplified task: policy evaluation
+ input: given a fixed policy pi(s)
+ still don't know T and R
+ Goal: learn the state values

### Direct Evaluation
+ Goal: compute values for each state under pi
+ Idea: Average together observed sample values
	- Acting according to pi
	- Every time visit a state, write down what the sum of discounted rewards turned out to be
	- Average those samples
+ problem:
	- wastes info about state connections
	- Each state must be learned separately
	- long time to learn

### Temporal Difference Learning
+ Learn from every experience
	- Update V(s) each time we experience a T(s,a,s',r)
	- s' will contribute updates more often
+ Temporal difference learning of values

+ problems
	- TD value learning is a model-free approach to do policy evaluation, mimicking Bellman updates with running sample averages

## Active Reinforcement Learning
+ Full RL: optimal policies(like value iteration)
	- don't know T and R
	- **YOU Choose Actions now**
	- Goal: learn the optimal policy / values
+ learner make actions
+ Q-learning

### Exploration vs. Exploitation
+ How to Explore
	- e-greedy
	- exploration functions
		- f(u,n) = u + k/n

