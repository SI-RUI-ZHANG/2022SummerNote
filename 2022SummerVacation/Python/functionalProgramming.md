# Functional Programming

## Pure Function

no side effect
same input $ \rightarrow $ same output

## `map()`, `filter()`, `zip`, `reduce()`

### `map()`

`map()` returns a map object (which is an iterator) of the results after applying the given function to each item of a given iterable (list, tuple etc.)

syntax

```python
map(fun, iter)
# fun: the function to which map passes each element of given iterable
# iter: a iterable which is to be mapped
# returns a list of the results after applying the given function to each item of a given iterable
```

```python
def times_two(item):
    return 2 * item


print(list(
    map(times_two, [1, 2, 3, 4])
    ))
# [2, 4, 6, 8]
```

### `filter()`

`filter()` filters the given sequence with the help of a function that tests each element in the sequence to be true or not

syntax

```python
filter(fun, iter)
# fun: function that tests if each element of a sequence true or not
# iter: ...
# returns an iterator that is already filtered
```

```python
def greater_than_ten(item):
    return item > 10


print(list(
    filter(greater_than_ten, [2, 3, 4, 11, 12])
    ))
# [11, 12]
```

### `zip()`

`zip` takes iterable or containers and returns a single iterator object, having mapped values from all the containers

syntax

```python
zip(*iterators)
# return a single iterator object
```

```python
my_list = ['a', 'b', 'c']
your_list = ['d', 'e', 'f']
print(list(
    zip(my_list, your_list)
    ))
# [('a', 'd'), ('b', 'e'), ('c', 'f')]
```

### `reduce()`

`reduce()` is used to apply a particular function passed in its argument to all of the list elements mentioned in the sequence passed along.

Working:

- first two elements of sequence are picked and the result is obtained
- apply the same function to the previously attained result and the number just succeeding the second element and the result is again stored
- process continues till no more elements are left in the container
- return the final result

```python
from functools import reduce

print(reduce(lambda a, b: a * b,
             [1, 2, 3, 4, 5]))
# 120
```

_I like_ `lambda`

## `lambda` Expression

Python `lambda` functions are anonymous function

syntax

```python
lambda arguments: expression
```

- the function can have **any number of arguments** but **only one expression**

```python
from functools import reduce

my_list = [1, 2, 3]

print(list(
    map(lambda x: x * 2, my_list)
    ))
# [2, 4, 6]
print(list(
    filter(lambda x: x>2, my_list)
    ))
# [3]
print(reduce(lambda x, y: x + y, my_list))
# 6
```

### `sort()`

```python
a = [(1, 2), (9, 3), (3, 7), (0, 1)]
a.sort(key=lambda x: x[1])
print(a)
# [(0, 1), (1, 2), (9, 3), (3, 7)] 
```

## List Comprehensions

`list comprehensions` are used for creating new lists form other iterables

syntax

```python
newList = [expression(element) for element in oldList if condition]
```

```python
name = 'sirui zhang'

my_list = ['|'+char+'|' for char in name]
print(my_list)
# ['|s|', '|i|', '|r|', '|u|', '|i|', '| |', '|z|', '|h|', '|a|', '|n|', '|g|']
numbers = [num for num in range(100)]
print(numbers)
# [0, 1, 2, 3, 4, 5, 6
even_numbers = [num for num in range(100) if num % 2 == 0]
print(even_numbers)
# [0, 2, 4, 6, 8, 10, ...
```

## `set` and `dictionary` comprehension

set: see list comprehension

dictionary:

```python
initial_dict = {
    'one': 1,
    'two': 2,
    'three': 3,
    'four': 4,
}

my_dict = {key + '|': value ** 2
           for key, value in initial_dict.items()
           if value % 2 == 0}
print(my_dict)
# {'two|': 4, 'four|': 16}
```

we can also write

```python
my_list = [1, 2, 3, 4]
my_dict = {num: num*2 for num in my_list}
```
