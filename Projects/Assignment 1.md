Options:
```
  -h, --help            show this help message and exit
  -n GAMES, --numGames=GAMES
                        the number of GAMES to play [Default: 1]
  -l LAYOUT_FILE, --layout=LAYOUT_FILE
                        the LAYOUT_FILE from which to load the map layout
                        [Default: mediumClassic]
  -p TYPE, --pacman=TYPE
                        the agent TYPE in the pacmanAgents module to use
                        [Default: KeyboardAgent]
  -t, --textGraphics    Display output as text only
  -q, --quietTextGraphics
                        Generate minimal output and no graphics
  -g TYPE, --ghosts=TYPE
                        the ghost agent TYPE in the ghostAgents module to use
                        [Default: RandomGhost]
  -k NUMGHOSTS, --numghosts=NUMGHOSTS
                        The maximum number of ghosts to use [Default: 4]
  -z ZOOM, --zoom=ZOOM  Zoom the size of the graphics window [Default: 1.0]
  -f, --fixRandomSeed   Fixes the random seed to always play the same game
  -r, --recordActions   Writes game histories to a file (named by the time
                        they were played)
  --replay=GAMETOREPLAY
                        A recorded game file (pickle) to replay
  -a AGENTARGS, --agentArgs=AGENTARGS
                        Comma separated values sent to agent. e.g.
                        "opt1=val1,opt2,opt3=val3"
  -x NUMTRAINING, --numTraining=NUMTRAINING
                        How many episodes are training (suppresses output)
                        [Default: 0]
  --frameTime=FRAMETIME
                        Time to delay between frames; <0 means keyboard
                        [Default: 0.1]
  -c, --catchExceptions
                        Turns on exception handling and timeouts during games
  --timeout=TIMEOUT     Maximum length of time an agent can spend computing in
                        a single game [Default: 30]
```                        
                        
  ### Question 1:
  A search ndoe must contain not only a state but also the information necessary to reconstruct
  the path which gets to that state.
  
  ### NOTES: 
    - All search functions need to return a list of actions
    - Stack, Queue and Priorityqueue data structure provided in util.py
    
    

## BFS expansion process:

```
frontier = Queue()
frontier.put(start) 
visited = {}    //creating a dictionary
visited[start] = True

while not frontier.empty():
  current = frontier.get()
  
  if current == goal:
    break
  
  for next in graph.neighbour(current):
    if next not in visited:
      frontier.put(next)
      visited[next] = True
```
      

## keep track of where we came from for every location that's visitied
```
frontier = Queue()
frontier.put(start)
came_from = {}
came_from[start] = None

while not frontier.empty():
   current = frontier.get()
   for next in graph.neighbors(current):
      if next not in came_from:
         frontier.put(next)
         came_from[next] = current
```

## Movement Cost
```
froniter = PriorityQueue()
frontier.put(start,0)
came_from = {}
cost_so_far = {}
came_from[start] = None
cost_so_far[start] = 0


while not frontier.empty():
  current = frontier.get()
  
  if current == goal:
    break
  
  for next in graph.neighbour(current):
    new_cost = cost_so_far[current] + graph.cost(current,next)
    if next not in cost_so_far or new_cost < cost_so_far[next]:
      cost_so_far[next] = new_cost
      priority = new_cost
      frontier.put(next,priority)
      came_from[next] = current
         
```   

## Heuristic search

A*
```
frontier = PriorityQueue()
frontier.put(start, 0)
came_from = {}
cost_so_far = {}
came_from[start] = None
cost_so_far[start] = 0

while not frontier.empty():
   current = frontier.get()

   if current == goal:
      break
   
   for next in graph.neighbors(current):
      new_cost = cost_so_far[current] + graph.cost(current, next)
      if next not in cost_so_far or new_cost < cost_so_far[next]:
         cost_so_far[next] = new_cost
         priority = new_cost + heuristic(goal, next)
         frontier.put(next, priority)
         came_from[next] = current
```  
  
  
  
  
  
  
  
  
  
