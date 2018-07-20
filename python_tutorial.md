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

