# Search Algorithms

<img src="https://github.com/Fannibals/AI/blob/master/pics/StateModel.png" alt="alt text" width="600" height="250">

 

## Classical Planning
+ Basic State Model
    * directed graphs
+ search algo
    * Blind search vs. Heuristic (or informed) search
        - Blind search : Only use the basic ingredients for general search algorithms
            + DFS
            + BFS
            + Uniform cost (Dijkstra)
            + Iterative Deepening (ID)
        - Heuristic search: heuristic fucntions that estimate the distance to the goal
            + A*
            + IDA*
            + Hill Climbing
            + Best First
            + WA*
            + DFS B&B
            + LRTA*
    * Systematic search vs. Local search
        - Systematic search
            + consider a large number of search nodes simultaneously
            + keeps some history of visited nodes
            + BFS, DFS, IDS, Best-First, A*
        - Local search
            + work with one (or a few) candidate solutions (search nodes) at a time
        - can overlap
            + hill-climbing
    + when to use?
        * satisfying planning
            - Heuristic >> Blind
            - Systematic ≈  Local
        * optimal planning
            - Heuristic > Blind
            - has to be Systematic

## Terminology
+ **Search node n**
   - Contains a state reached by the search, plus information about how it was reached.
+ **Path cost g(n)**
   - The cost of the path reaching n
+ **Optimal cost g***
   - The cost of an optimal solution path. For a state s, g*(s) is the cost of a cheapest path reaching s.
+ **Node expansion**
   - Generating all successors of a node
+ **Search strategy**
   - Method for deciding which node is expanded next.
+ **Open list (Frontier)**
   - Set of all nodes that currently are candidates for expansion.
+ **Closed list (explored set)**
   - Set of all states that were already expanded. 
    * only used in graph search
        - not in tree search

## world states vs. search states
+ the **World state** includes all things related to this problem
+ the **Search state** keeps only the details needed for planning

## Progression vs. Regression
+ progression
    * forward
    * default in this course
    * search states = world states
+ regression
    * backward
    * search states = sub-goals we would need to achieve
        -  search states != world states
        -  search states = sets of world states, represented as conjuntive sub-goals

## Search States != Search Nodes
Search Nodes = Parent + Action + Cost + Search States =  Search states + info on “how we got there”


## Evaluation
* Guarantees
    - Completeness
        + can find a solution
    - Optimality
* Complexity
    - time: measured in generated states
    - space: measured in states
* factors
    - Branching factor b: how many successors does each state have?
    - Goal depth d: The number of actions required to reach the shallowest goal state

## Blind search
+ No additioanal work for the programmer

### Breadth-First Search
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/BFS.png" alt="alt text" width="700" height="400">
+ __low time complexity__
 - Variant: Uniform cost search (Dijkstra)
+ Strategy: expand a shallowest node first
+ Implementation: Fringe is a FIFO queue

+ **properties**
  - **Complete**: yes (s must be finite if a solution exists)
  - **Optimal**: yes only if costs are same
  - **Time complexity**:  <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;O(b^{d})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;O(b^{d})" title="O(b^{d})" /></a>
  - **Space complexity**:  <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;O(b^{d})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;O(b^{d})" title="O(b^{d})" /></a>

### Depth-First Search
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/DFS.png" alt="alt text" width="700" height="400">
+ __low space complexity__
+ Strategy: expand a deepest node first
+ Implementation: Fringe is a LIFO stack

+ **properties**
  - **Complete**: 
   - NO, search branches may be infinitely long and there is no check for cycles along a branch
   - YES when the state space is finite and acyclic
  - **Optimal**: No, due to DFS is a way of "hoping to get lucky"
  - **Time complexity**: O(b^d)
  - **Space complexity**: O(b*d)

+ The embarrassing failure of depth-first search in infinite state spaces can be alleviated by supplying depth-first search with a predetermined depth limit l. That is, nodes at depth l are treated as if they have no successors. This approach is called **depth-limited search**. 

### Iterative deepening search 
### (preferrd blind search method in large state spaces with unknown solution depth)
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/Iterative.png" alt="alt text" width="600" height="200">
+ Starting from level 0, if the goal test is not true, move to the level 1 and do the DFS  
  if still not find the key, move to the level 2 and so on.
+ low complexity in both time and space
+ Uses depth-limited search as a sub-procedure
+ **properties**
  - **Complete**: yes when the branching factor is finite
   - the **branching factor** is the **number of children at each node**, the outdegree.
  - **Optimal**: yes when the path cost is a nondecreasing function of the depth of the node.
  - **Time complexity**: O(b^d)
   - the nodes on the bottom level(depth d) are generated once, those on the next-to-bottom level are generated twice, etc.
   - the worst case: N(IDS) = (d)b + (d-1)b^2 + (d-2)b^3 +...+ (1)b^d , which is in O(b^d)
  - **Space complexity**: O(b*d)

+ IDS is the preferred search method in large state spaces with unknown solution depth
+ Bi-directional search
  - will not be examed


## Heuristic search 启发式搜索
+ The objective of a heuristic is to produce a solution in a reasonable time frame that is good enough for solving the problem at hand
+ requires as additional input a heuristic function h
+ most common and overall most successful algorithms for classical planning
+ heuristic function  __estimate__ the distance (or __remaining cost__) to the goal
    * search prefer to explore states with small h
    * h-value
+ remaining cost `h*`
    * ∞ if impossible
    * _perfect heuristic_ h = h*  
+ **property of `h`** these propoerties make sure that A* is always optimistic
    * can be
        - safe
         - the heuristic value is infinite(there is no solution from that state)
        - goal-aware
         - h(s) = 0 for all goal staes s is in SG
        - admissible
            + An admissible heuristic is one that never overestimates the cost to reach the goal.
            + always optimistic, never over-estimate
        - consistent
            + required only for applications of A∗ to graph search.
            + h diff <= action cost
            + h(n) ≤ c(n, a, n') + h(n') .
    * **relationships between properties**
        - `admissible -> goal-aware`
        - `admissible -> safe`
        - `consistent + goal aware -> admissible`
+ performance depends crucially on "how well `h` reflects `h*`"
    * the imformedness of `h`
    * the computational overhead of computing `h`
    * extreme cases
        - `h = h*`: perfectly informed
        - `h = 0`: No information at all
### Heuristic Function
+ <img src ="https://github.com/Fannibals/AI/blob/master/pics/Heuristic.png" height = 220, width = 730>
+ h: S -> Ro+ and {max}
 - map state S to a positive real value including the value 0 and infinite
+ h*: the star"*" means the optimal best value
 - perfect heuristic == h*
 - h+ is the heuristic function that is devised automatically
### systematic heuristic search
+ **Greedy Best-First Search**
    * __1/3 popular in satisﬁcing planning__
    * priority queue ordered by ascending __h(state(σ))__
        - priority queue
            + min heap
    * complete: YES for safe
    * optimal: NO
        - even for perfect heuristic, (e.g., `start --1000-->goal` and `start --0--> goal`,) nothing prevents it from choosing the bad one
            + different costs, but same `h`, 0.
+ Weighted A*
    * __1/3 popular in satisﬁcing planning__
    * priority queue ordered by ascending __g(state(σ)) + W*h(state(σ))__
    * For W > 1, weighted A* is **bounded suboptimal**: if h is admissible, then the solutions returned are at most a factor W more costly than the optimal ones.
    * |W|Weighted A* behaves like|
      | ---|---|
      |0| Uniform-cost search |
      |1|A*|
      |maximum| greedy best serach|
+ A*
    * __most popular in optimal planning,__ rarely used in satisﬁcing planning
    * combine best-first and dijktra
    * priority queue ordered by ascending __f-value = g(state(σ)) + h(state(σ))__
        - 如果g(n)为0，即只计算任意顶点n到目标的评估函数h(n)，而不计算起点到顶点n的距离，则算法转化为使用贪心策略的Best-First Search，速度最快，但可能得不出最优解；
        - 如果h(n)不高于实际到目标顶点的距离，则一定可以求出最优解，而且h(n)越小，需要计算的节点越多，算法效率越低，常见的评估函数有——欧几里得距离、曼哈顿距离、切比雪夫距离；
        - 如果h(n)为0，即只需求出起点到任意顶点n的最短路径g(n)，而不计算任何评估函数h(n)，则转化为单源最短路径问题，即Dijkstra算法，此时需要计算最多的定点；
    * re-open for smaller g
        - recall dijkstra
    * terminology
        - f-value : f(s) = g(s)+h(s)
        - generated nodes: nodes that are in the open list
        - expanded nodes: in closed list -- already have children
        - re-expanded nodes: already expanded but after comparing these nodes are more cheaper, so expand them again.
    * property
        - complete
            + yes for safe (even without duplication detection)
        - optimal
            + yes for admissible (even without duplication detection)
            + proof: https://docs.google.com/document/d/12upePheGQxXKQQ3laxtMeB8SxnaxkE-NUiQlwnaTpY4/edit
    * if `h = 0`
        - _A*_ becomes __uniform-cost__
    * Implementation
     - Popular method: 
       - whenever you have a plato(a set of state that have the same value)
       - break tie with smaller h-value
     - If h is admissible and consistent ⇒ A* never re-opens a state.
       - whenever A* finds a path to the state, you will guarantee that there is no cheaper one that can get in there.
     - Common, hard to spot bug: check duplicates at the wrong point.
+ IDA*, depth-ﬁrst branch-and-bound search, breadth-ﬁrst heuristic search ...

### local heuristic search
+ hill-climbing (本课程中 hill-climbing 一般指 steepest ascent hill-climbing)
    * local minima/maxima
        - not complete
            + when there are local maxima in the search space which are not solutions
        - not optimal
    * simple hill climbing vs. steepest ascent hill climbing
        - simple hill climbing chooses the __first closer__ node
        - steepest ascent hill climbing all successors are compared and the __closest__ to the solution is chosen
            + Steepest ascent hill climbing is similar to best-first search, which tries all possible extensions of the current path instead of only one.
                * steepest ascent hill-climbing vs. best-first
                    - hill-climbing __sorts the current__ node's children before adding them to the queue
                    - best-first search adds the current node's children to the queue, and then __sorts the entire__ queue
    * __不维护搜索树__ (_space complexity 与 `d` 无关?_)，只记录当前状态和目标函数值，不考虑与当前状态不相邻的状态
+ enforced hill-climbing
    * __1/3 popular in satisﬁcing planning__
    * makes sense only if h(s)>0
    * Breadth-ﬁrst search for state with strictly smaller h-value.
    * not optimal
    * not complete in general, yes under particular circumstance. Assuming `h` goal-aware
+ Beam search, tabu search, genetic algorithms, simulated annealing, ...

## Blind vs. Heuristic
+ blind
    * pros
        - no additional work for programmer
    * cons
        - rarely effective in practice
            + same expansion order regardless what the problem actually is (_blind_) 
+ heuristic
    * pros
        - typically more effective in practice
    * cons
        - need `h`
        

## Properties of Search Algorithms

<img src="https://github.com/Fannibals/AI/blob/master/pics/SearchSummary.png" width="600" height="300">

