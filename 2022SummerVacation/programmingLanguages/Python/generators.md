# Generators

## `yield`

the `yield` statement suspends function's execution and sends a value back to the caller, but retains enough state to enable function to resume where it is left off.

```python
def squares(num):
    for item in range(num):
        yield item * item


for square in squares(10):
    print(square)
```

## Iterator

An iterator is an object that contains a countable of numbers
Iterator can be iterated upon, you can traverse through all the values
In python, iterator is an object implements the iterator protocol, which consist of `__iter__()` and `__next__()`

## Generator

A generator function is defined like a normal function, but whenever it needs to generate a value, it does so with the `yield` keyword rather than `return`
If the body of a `def` contains `yield`, the function automatically becomes a generator function

```python
def simpleGeneratorFunc():
    yield 1
    yield 2
    yield 3

# x is a generator object
x = simpleGeneratorFunc()

# Iterating over the generator object using next
print(x.next())
# 1
print(x.next())
# 2
print(x.next())
# 3
```

a `generator function` returns a `generator object` that is iterable

### generator object

Generator functions return a generator object.
Generator objects are used either by calling the `next()` method on the generator object or using the generator object in a `for ... in ...` loop

### examples

```python
def special_for(iterable):
    iterator = iter(iterable)
    while True:
        try:
            print(next(iterator))
        except StopIteration:
            break


special_for([1, 2, 3, 4, 5])
```

```python
class MyGen:
    current = 0

    def __init__(self, first, last):
        self.first = first
        self.last = last

    def __iter__(self):
        return self

    def __next__(self):
        if MyGen.current < self.last:
            num = MyGen.current
            MyGen.current += 1
            return num
        raise StopIteration


gen = MyGen(0, 100)
for i in gen:
    print(i)
```

### fibonacci number

```python
def fib(number):
    a = 0
    b = 1
    for i in range(number):
        yield a
        temp = a
        a = b
        b = temp + b
```

