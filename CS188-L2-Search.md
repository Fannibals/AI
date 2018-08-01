# Search 

## 1. Planning agents
+ Ask "what if"
+ Decisions based on consequences of actions
+ Have a model 
+ Must formulate a goal test
+ CONSIDER HOW THE WORLD WOULD BE

+ Optimal vs. complete planning
+ Planning vs. replanning (short plan)


## 2. Search Problems
+ A search problem consists of:
  + A state space S
  + A successor function
    + actions
    + costs
  + A **start state** and a **goal test**
+ A solution is a sequence of actions which transforms the start state to a goal state.

## Example: Traveling in Romania
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/example1.png" alt="alt text" width="600" height="450">
+ State Space: cities
+ Successor function: roads, cost = distance
+ Start state: Arad
+ Goal test: Is state == Bucharest?
+ Solution


## 3. State Space
+ World state vs. search state
  - the **World state** includes all things related to this problem
  - the **Search state** keeps only the details needed for planning
  
+ problem: pathing
  - states: (x,y) location
  - actions: NSEW
  - successor: how to update location 
  - Goal test: is (x,y) = END
  
problem  |  pathing   | eat-all-dots 
-------  | :-------:  | ------------:
states   |   location  |   {(x,y), dot booleans}       
actions |   NSEW  |   NSEW
successor|  update location| update location and possibly a dot boolean
goal test|  is (x,y) =END|  dots all false
 
+ **State Space Size**
  - World State
    - Agent positions : 120
    - Food count : 30
    - Ghost positions: 12
    - Agent facing : NSEW
  - How many?
    - 120*(2^30)*(12^2)*4
    
    
+ Problem: eat all dots while keeping the ghosts perma-scared
  - agent position
  - dot booleans
  - power pellet booleans
  - remaining scared time

## State Space Graphs
+ a mathematical representation of a search problem
+ each state occur only once

## Search Trees
+ start state => root node
+ children => successors


## General Tree Search
+ important ideas
  - Fringe
  - Expansion
  - Exploration strategy
  
### Depth-First Search
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/DFS.png" alt="alt text" width="700" height="400">
+ Strategy: expand a deepest node first
+ Implementation: Fringe is a LIFO stack

+ **properties**
  - Complete: yes
  - Optimal: no
  - Time complexity: O(b^m)
  - Space complexity: O(b*m)
### Breadth-First Search
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/BFS.png" alt="alt text" width="700" height="400">
+ Strategy: expand a shallowest node first
+ Implementation: Fringe is a FIFO queue

+ **properties**
  - Complete: yes (s must be finite if a solution exists)
  - Optimal: yes only if costs are same
  - Time complexity: O(b^s)
  - Space complexity: O(b^s)

### BFS vs. DFS
+ BFS
  - 
+ DFS
  - 
  
### Iterative Deepening
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/Iterative.png" alt="alt text" width="600" height="200">
+ O(b * s) memory
+ O(b^s) running time 

### Uniform Cost Search
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/uniformcost.png" alt="alt text" width="600" height="450">
+ Strategy: expand a cheapest node first
+ Fringe is a priority queue 

+ **properties**
  - Complete: yes
  - Optimal: yes 
  - Time complexity: O(b^(C^*/e))
  - Space complexity: O(b^(C^*/e))
  
  C^*/e
