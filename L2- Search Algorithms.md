# Search Algorithms

## State Model &nbsp; _S(P)_
<img src="https://github.com/Fannibals/AI/blob/master/pics/StateModel.png" alt="alt text" width="700" height="300">

 

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
+ <img src="https://github.com/Fannibals/AI/blob/master/pics/DFS.png" alt="alt text" width="700" height="400">
+ __low time complexity__
 - Variant: Uniform cost search (Dijkstra)
+ Strategy: expand a shallowest node first
+ Implementation: Fringe is a FIFO queue

+ **properties**
  - Complete: yes (s must be finite if a solution exists)
  - Optimal: yes only if costs are same
  - Time complexity:  <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;O(b^{d})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;O(b^{d})" title="O(b^{d})" /></a>
  - Space complexity:  <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;O(b^{d})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;O(b^{d})" title="O(b^{d})" /></a>

+ DFS
    * __low space complexity__
    * Guarantees
        - complete when __acyclic__
            + if we record the visited nodes, can DFS be complete even if there is a cycle?
                * if there are infinite nodes, DFS might get unlucky and follow one route that can visit infinite nodes. However, BFS goes down by levels, which means it is able to find shortest path. That is why even recording visited nodes still cannot guarantee DFS be complete when there is infinite nodes.
        - not optimal
    * complexity, m is the max depth reached
        - space
            + O(b*m)
        - time
            + worst: O(b^m), infinite
            + best: O(b*l)
+ Iterative deepening search (preferrd blind search method in large state spaces with unknown solution depth)
    * low complexity in both time and space
    * Uses depth-limited search as a sub-procedure
    * Guarantees
        - complete
        - optimal
            + better than DFS
    * Complexity
        - space
            + O(b*d)
            + better than BrFS
        - time
            + O(b^d)
+ Bi-directional search
    * will not be examed

## Heuristic search 启发式搜索
+ requires as additional input a heuristic function h
+ most common and overall most successful algorithms for classical planning
+ heuristic function  __estimate__ the distance (or __remaining cost__) to the goal
    * search prefer to explore states with small h
    * h-value
+ remaining cost `h*`
    * ∞ if impossible
    * _perfect heuristic_ h = h*  
+ property of `h`
    * can be
        - safe
        - goal-aware
        - admissible
            + never over-estimate
        - consistent
            + h diff <= action cost
    * relationships between properties
        - `admissible -> goal-aware`
        - `admissible -> safe`
        - `consistent + goal aware -> admissible`
+ performance depends crucially on "how well `h` reflects `h*`"
    * the imformedness of `h`
    * the computational overhead of computing `h`
    * extreme cases
        - `h = h*`
        - `h = 0`

### systematic heuristic search
+ Greedy Best-First Search
    * __1/3 popular in satisﬁcing planning__
    * priority queue ordered by ascending __h(state(σ))__
        - priority queue
            + min heap
    * complete for safe
    * not optimal
        - even for perfect heuristic, (e.g., `start --1000-->goal` and `start --0--> goal`,) nothing prevents it from choosing the bad one
            + different costs, but same `h`, 0.
+ Weighted A*
    * __1/3 popular in satisﬁcing planning__
    * priority queue ordered by ascending __g(state(σ)) + W*h(state(σ))__
    * For W > 1, weighted A* is bounded suboptimal: if h is admissible, then the solutions returned are at most a factor W more costly than the optimal ones.
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
        - f-value
        - generated nodes
        - expanded nodes
        - re-expanded nodes
    * property
        - complete
            + yes for safe (even without duplication detection)
        - optimal
            + yes for admissible (even without duplication detection)
    * if `h = 0`
        - _A*_ becomes __uniform-cost__
    * If h is admissible and consistent, then A∗ never re-opens a state.
        - then can simplify the algorithm
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
![blind.vs.informed](./pics/blind.vs.informed.png)
