https://kate.io/blog/2017/08/22/weird-python-integers/

Python keeps its small integers in a table. (Tested in Python 3.6.1.)
```py
>>> a = 42
>>> b = 42
>>> a is b # True
>>> a = 316
>>> b = 316
>>> a is b # False
```

> We can use the Python built-in function `id` which returns a value you can think of as a memory address to investigate.
```py
>>> a = 128
>>> id(a) # 4504844960
```

> Python has a module called `ctypes` that can be misused to directly edit memory.
```py
>>> import ctypes
>>>
>>> def mutate_int(an_int, new_value):
...   ctypes.memmove(id(an_int) + 24, id(new_value) + 24, 8)
...
>>> a_number = 7
>>> another_number = 7
>>> mutate_int(a_number, 13)
>>> a_number
13
>>> another_number
13
```
