## Python Tutorial

## Unix Basics
### File/Directory Manipulation
+ some useful UNIX commands
```
[cs188-ta@nova ~]$ mkdir foo
[cs188-ta@nova ~]$ cd foo
[cs188-ta@nova ~]$ ls
```
+ some more
  * **_cp_** copies a file or files
  * **_rm_** removes (deletes) a file
  * **_mv_** moves a file (i.e., cut/paste instead of copy/paste)
  * **_man_** displays documentation for a command
  * **_pwd_** prints your current path
  * **_xterm_** opens a new terminal window
  * **_firefox_** opens a web browser
  * **_Press_** "Ctrl-c" to kill a running process
  * **_Append_** & to a command to run it in the background
  * **_fg_** brings a program running in the background to the foreground
  
  
## The Emacs text editor
+ commands
```
[cs188-ta@nova ~/python_basics]$ emacs helloWorld.py
```
+ useful commands
  * **C-x C-s** Save the current file
  * **C-x C-f** Open a file, or create a new file it if doesn't exist
  * **C-k** Cut a line, add it to the clipboard
  * **C-y** Paste the contents of the clipboard
  * **C-_** Undo
  * **C-g** Abort a half-entered command


## Python Basics

### Dir and Help
```
>>> s = 'abc' 

>>> dir(s)
['__add__', '__class__', '__contains__', '__delattr__', '__doc__', '__eq__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getslice__', '__gt__', '__hash__', '__init__','__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__','__repr__', '__rmod__', '__rmul__', '__setattr__', '__str__', 'capitalize', 'center', 'count', 'decode', 'encode', 'endswith', 'expandtabs', 'find', 'index', 'isalnum', 'isalpha', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'replace', 'rfind','rindex', 'rjust', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']

>>> help(s.find)

Help on built-in function find:

find(...)
    S.find(sub [,start [,end]]) -> int
    
    Return the lowest index in S where substring sub is found,
    such that sub is contained within s[start,end].  Optional
    arguments start and end are interpreted as in slice notation.
    
    Return -1 on failure.

>> s.find('b')
1
```

### Built-in Data Structures

### List
#### Lists of lists
```
>>> lstOfLsts = [['a','b','c'],[1,2,3],['one','two','three']] 
>>> lstOfLsts[1][2] 
3
>>> lstOfLsts[0].pop()
'c'
>>> lstOfLsts
[['a', 'b'],[1, 2, 3],['one', 'two', 'three']]
```

### Tuple
unlike list, you can change tuple's content once it is created
```
>>> pair = (3,5)
>>> pair[0]
3
>>> x,y = pair
>>> x
3
>>> y
5 
>>> pair[1] = 6
TypeError: object does not support item assignment
```

### Set
A _set_ is another data structure that serves as an unordered list with no duplicate items.
```
>>> shapes = ['circle','square','triangle','circle']
>>> setOfShapes = set(shapes)
>>> setOfShapes 
set(['circle','square','triangle']) 
>>> setOfShapes.add('polygon') 
>>> setOfShapes 
set(['circle','square','triangle','polygon']) 
>>> 'circle' in setOfShapes 
True 
>>> 'rhombus' in setOfShapes 
False 
```

### QuickSort
```
def quickSort(lst):
    if len(lst) <= 1: 
        return lst
    smaller = [x for x in lst[1:] if x < lst[0]]
    larger = [x for x in lst[1:] if x >= lst[0]]
    return quickSort(smaller) + [lst[0]] + quickSort(larger)

# Main Function
if __name__ == '__main__':    
    lst = [2,4,5,1]
    print (quickSort(lst))   
```

### Question 3
```
import shop

def shopSmart(orderList, fruitShops):
    """
        orderList: List of (fruit, numPound) tuples
        fruitShops: List of FruitShops
    """    
    
    minCost, argMin = None, None
    for shop in fruitShops:
        cost = shop.getPriceOfOrder(orderList)
        if minCost == None or cost < minCost:
            minCost, argMin = cost, shop
    return argMin
    
if __name__ == '__main__':
  orders = [('apples',1.0), ('oranges',3.0)]
  dir1 = {'apples': 2.0, 'oranges':1.0}
  shop1 =  shop.FruitShop('shop1',dir1)
  dir2 = {'apples': 1.0, 'oranges': 5.0}
  shop2 = shop.FruitShop('shop2',dir2)
  shops = [shop1, shop2]
  print "For orders: ", orders, "best shop is", shopSmart(orders, shops).getName()
  orders = [('apples',3.0)]
  print "For orders: ", orders, "best shop is", shopSmart(orders, shops).getName()
  ```

```
class FruitShop:

    def __init__(self, name, fruitPrices):
        """
            name: Name of the fruit shop
            
            fruitPrices: Dictionary with keys as fruit 
            strings and prices for values e.g. 
            {'apples':2.00, 'oranges': 1.50, 'pears': 1.75} 
        """
        self.fruitPrices = fruitPrices
        self.name = name
        print 'Welcome to %s fruit shop' % (name)
        
    def getCostPerPound(self, fruit):
        """
            fruit: Fruit string
        Returns cost of 'fruit', assuming 'fruit'
        is in our inventory or None otherwise
        """
        if fruit not in self.fruitPrices:
            print "Sorry we don't have %s" % (fruit)
            return None
        return self.fruitPrices[fruit]
        
    def getPriceOfOrder(self, orderList):
        """
            orderList: List of (fruit, numPounds) tuples
            
        Returns cost of orderList. If any of the fruit are  
        """ 
        totalCost = 0.0             
        for fruit, numPounds in orderList:
            costPerPound = self.getCostPerPound(fruit)
            if costPerPound != None:
                totalCost += numPounds * costPerPound
        return totalCost
    
    def getName(self):
        return self.name
    
    def __str__(self):
        return "<FruitShop: %s>" % self.getName()
```
