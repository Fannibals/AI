### BaselineTeam.py
```
  def chooseAction(self, gameState):
    """
    Picks among the actions with the highest Q(s,a).
    """
    actions = gameState.getLegalActions(self.index)

    # You can profile your evaluation time by uncommenting these lines
    
    start = time.time()   // Python time time() 返回当前时间的时间戳（1970纪元后经过的浮点秒数）
    values = [self.evaluate(gameState, a) for a in actions] // evaluate => Counter()
    print 'eval time for agent %d: %.4f' % (self.index, time.time() - start) // 时间间隔

    maxValue = max(values)
    bestActions = [a for a, v in zip(actions, values) if v == maxValue]

    foodLeft = len(self.getFood(gameState).asList())

    if foodLeft <= 2:
      bestDist = 9999
      for action in actions:
        successor = self.getSuccessor(gameState, action)
        pos2 = successor.getAgentPosition(self.index)
        dist = self.getMazeDistance(self.start,pos2)
        if dist < bestDist:
          bestAction = action
          bestDist = dist
      return bestAction

    return random.choice(bestActions)   // randomly choose one
```
