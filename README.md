# awesome-python3-webapp
## Day 1
1.define function:
from xx(xx.py) import xx(a function in xx.py)

2.Type error
```
if not isinstance(x, (int, float)): 
   raise TypeError('bad operand type')
```

3.function can return several results.
```
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
```
In fact, what function return is a tuple.

4.number of parameter could be undefined.
```
def calc(numbers):
```






