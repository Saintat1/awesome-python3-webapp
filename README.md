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

## Day 2


# Python学习笔记


    def f(x):
        return x*x


    map(f, [1,2,3,4,5,6,7,8,9])




    [1, 4, 9, 16, 25, 36, 49, 64, 81]




    l=[]
    for n in [1,2,3,4,5,6,7,8,9]:
        l.append(f(n))
    print l

    [1, 4, 9, 16, 25, 36, 49, 64, 81]
    


    map(str,[1,2,3,4,5,6,7,8,9])




    ['1', '2', '3', '4', '5', '6', '7', '8', '9']




    def fn(x,y):
        return x*10+y
    reduce(fn,[1,3,5,7,9])




    13579




    def is_odd(n):
        return n%2==1
    filter(is_odd,[1,2,4,5,6,9,10,15])




    [1, 5, 9, 15]




    def is_sushu(n):
        return 
    

把lambda的函数分别作用在后面的函数中
map( lambda x : x + 1, [1, 2, 3] )

# e.g. choose prime number in 1 to 100


    list=range(1,101)
    for i in list:
        list=filter(lambda x: x%i !=0 or i==1 or x==i,list)
    print list

    [1, 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
    

思想：从小的开始去除,i=1时全部保留

sorted()用于排序
可以用于比较函数来实现自定义的排序,原函数事实上是两两比较 
(x,y)
  x>y return 1;
  x<y return -1;
  return 0;

## e.g.降序排序


    def reversed_cmp(x,y):
        if x>y:
            return -1
        if x<y:
            return 1
        return 0
    sorted([36,5,12,9,21],reversed_cmp)




    [36, 21, 12, 9, 5]



## or


    sorted([26,21,12,9,5],lambda x,y: y-x)




    [26, 21, 12, 9, 5]



# 返回函数 RETURN


    ##example:
    
    def lazy_sum(*args):
        def sum():
            ax=0
            for n in args:
                ax=ax+n
            return ax
        return sum

返回的是函数 用f()返回求和结果
f1=lazy_sum(1,3,5,7,9)
f2=lazy_sum(1,3,5,7,9)
f1!=f2 but  f1()=f2()


    f=lazy_sum(1,3,5,7,9)
    f()




    25



## 闭包 closure
<a href=https://www.zhihu.com/question/34872127>https://www.zhihu.com/question/34872127</a>

返回函数不要引用任何循环变量， 或者后续会发生变化的变量

##匿名函数 lambda x: f(x)

#装饰器 decorator(在代码运行期间动态增加功能)

.__name__可以拿到函数的名字


    def now():
        print '2016-06-03'
    now()

    2016-06-03
    


    def log(func):
        def wrapper(*args,**kw):
            print 'call %s():' %func.__name__     #先打印日志
            return func(*args,**kw)               #再返回函数
        return wrapper


    @log     #相当于执行了语句now=log(now)
    def now():
        print '2016-06-03'


    now()

    call now():
    2016-06-03
    

log是一个装饰器，返回一个函数，原来的now()函数仍然存在，同名的now变量指向了新的函数，于是调用now()会执行新的函数

##Python中完整的decorator的写法:


    import functools
    
    def log(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('call %s():' % func.__name__)
            return func(*args, **kw)
        return wrapper

带参数的decorator:


    import functools
    
    def log(text):
        def decorator(func):
            @functools.wraps(func)
            def wrapper(*args, **kw):
                print('%s %s():' % (text,func.__name__))
                return func(*args, **kw)
            return wrapper
        return decorator

#Partial Function


    int('12345',base=8)




    5349




    import functools
    int2=functools.partial(int,base=2) #作用就是把一个函数的某些参数给固定住，返回一个新的函数

#模块


    import sys


    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    ' a test module '
    
    __author__ = 'Michael Liao'
    
    import sys
    
    def test():
        args = sys.argv
        if len(args)==1:
            print 'Hello, world!'
        elif len(args)==2:
            print 'Hello, %s!' % args[1]
        else:
            print 'Too many arguments!'
    
    if __name__=='__main__':
        test()

    Too many arguments!
    


    if __name__='__main__':
        test()


      File "<ipython-input-8-d3328f48b353>", line 1
        if __name__='__main__':
                   ^
    SyntaxError: invalid syntax
    



    from PIL import Image


    im=Image.open('test.png')
    print im.format, im.size, im.mode

    PNG (582, 322) RGBA
    


    im.thumbnail((200,100))
    im.save('thumb.jpg','JPEG')

# 06/04/2016 多重继承





