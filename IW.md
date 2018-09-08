# Searching for Novelty

## 1. Width-based search
### Planning is PSPACE-complete -- hard to solve
+ how to explain why planners perform well?
+ benchmark between "easy" and "hard" domains?

#### our answer is **width**
+ hard problems:
	- with higher atomic width
		- solving a single problem becomes difficult
	- hard to serialize
		- multiple goals 


### 2. **Novelty**
#### Definition
+ the **novelty w(s) of a state s** is the size of the **smallest subset of atoms(facts)** in s that is true for the first time in the search. 

+ if w(s) = 1, it means that there is a single item that we havn't seen so far.
	- look the search tree and look the new state, if find a single item, then the novelty is 1

+ example : p,q,r
	- case 1
		- p is true, q is false ,then w({p,q}) = 1;
	- case 2
		- p is true, q is true, but p^q is false, then w({p,q}) = 2;

### 3. Iterated Width(IW)
#### Algorithm
+ IW(k) = breadth-first search that **prunes** newly generated states whose novelty(s) > k
	- for instance, if novelty(s) > k, just prunes it
+ a sequence of calls IW(k) for i =0,1,2,3... over problem P until problem solved or i exceeds # of variables in problem.


+ properties
	- IW(k) expands at most O(n^k) states, where n is the number of atoms.
		- for instance , F={c(a),move(a)}, the most states increases at a time is all these facts become true first
	- IW(k) sovles problems **optimally**
	- IW(k) is **complete**

+ IW performce quite good for goals which goals are single atoms

#### Serialized Iterated Width(SIW)
+ achieving atomic goals one at a time
+ SIW uses IW for both decomposing a problem into subproblems and for solving them
+ blind search ; no heuristicl
+ IW does not even know next goal to achieve

+ Blind SIW better than GBFS + h(add)\

#### Summary
+ <img src = "Summary so far">	P13


### 4. Classical Planning
+ state-of-the-art methods for satisficing planning rely on
	- h
	- Greedy best-first search(GBFS)
	- extensions

+ shortcoming of GBFS
	- pure greedy - stuck in local 

### 5. Best-First Width Search(BFWS
+ <img src="BFWS">

### 6. Models and Simulators
+ 






