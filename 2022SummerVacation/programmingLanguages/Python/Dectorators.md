# Decorators

## Higher order functions

function accepts another function or function returns another function

## Decorators

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print('===================')
        func(*args, **kwargs)
        print('===================')

    return wrapper


@my_decorator
def my_print(message):
    print(message)


my_print('test')
```

### measure performance

```python
from time import time


def performance(func):
    def wrapper(*args, **kwargs):
        t1 = time()
        result = func(*args, **kwargs)
        t2 = time()
        print(f'took {t2 - t1} ms')
        return result

    return wrapper


@performance
def long_time():
    for i in range(10000):
        for j in range(10000):
            pass


long_time()
# took 1.0664479732513428 ms
```

## From Geeks for Geeks

`decorators` allow us to wrap another function in order to extend the behavior of the wrapped function

In python, functions are **first class objects**

- a function is an instance of the Object type
- you can store the function in a variable
- you can pass the function as a parameter to another function
- you can return a function from a function
- you can store them in data structures such as hash tables, lists, ...

```python
@my_decorator
def hello():
    print("hello")

# is equivalent to

def hello():
    print("hello")

hello = my_decorator(hello)
```
