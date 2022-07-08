# Python basics II

## Conditional Logic

```python
if is_old_enough:
    print('you are old enough to drive!')
elif is_licenced:
    print('you can drive now!')
else:
    print('you cannot drive')
```

```python
if is_old_enough and is_licenced:
    print('you are old enough to drive!')
else:
    print('you cannot drive')
```

## Truthy vs Falsey

Falsey values:

- `[]`: empty lists
- `()`: empty tuples
- `{}`: empty dictionaries
- `set()`: empty sets
- `""`: empty strings
- `range(0)`: empty ranges
- `0`: integer 0
- `0.0`: float 0.0
- `0j`: complex 0j
- `None`
- `False`

Truthy values:

- Non-empty sequences or collections (lists, tuples, strings, dictionaries, sets)
- Numeric values that are not zero
- Constant: True

## Ternary Operator

syntax

```python
do_if_true condition do_if_false
```

```python
is_true = True

print('is true') if is_true else print('is false')
```

## Short Circuiting

$ \dots $

## Logical Operators

`and`,
`or`,
`>`,
`<`,
`>=`,
`<=`,
`==`,
`not`

```python
x = 3
print(1 < x <= 5)
# True
```

## `==` vs `is`

`==` checks for equality of value

```python
print(True == 1)
# True
```

`is` checks memory location

```python
arr_one = [1, 2, 3]
arr_two = [1, 2, 3]
print(arr_one == arr_two)
# True
print(arr_one is arr_two)
# False
```

## For loops

```python
for item in 'Zero to Mastery':
    print(item, end='')
# Zero to Mastery


for item in 'Zero to Mastery':
    print(item, end='')
print(item)
# Zero to Masteryy
```

## Iterable

list, dictionary, tuple, set, string
can be iterated

```python
user = {
    'name': 'Sirui',
    'age': 20,
    'hobby': 'coding'
}

for item in user:
    print(item)
#name
#age
#hobby

for item in user.values():
    print(item)
#Sirui
#20
#coding

for item in user.keys():
    print(item)
#name
#age
#hobby

for item in user.items():
    print(item)
#('name', 'Sirui')
#('age', 20)
#('hobby', 'coding')
```

## `rang()`

`rang()` returns the sequence of the given number between the given range

syntax

```python
range(stop)
range(start, stop[, step])
```

start from 0 by default

if you don't really care about the input, you can write in this way

```python
for _ in range(10)
    print('email')
```

## `enumerate()`

`enumerate()` method adds a counter to an iterable and returns it in a form of enumerating object

syntax

```python
enumerate(iterable, start=0)
```

example

```python
for i, char in enumerate('Hello'): print(i, char, end=' ')
#0 H 1 e 2 l 3 l 4 o
```

## while loop

```python
i = 0
while i < 10:
    print(i)
    i++
else:
    print('done with all the word')
```

`else` will not execute if there is a break statement triggered in the while loop

## `break`, `continue`, `pass`

`break`: used to terminate the loop or statement in which it is present.
`continue`: instead of terminating the loop, it forces the loop to execute the next iteration if the loop
`pass`: used as a placeholder for future code; when `pass` statement is executed, nothing happens, but you avoid getting an error when empty code is not allowed

## `def` function

```python
def say_hello():
    print('hello')

say_hello()
```

## arguments vs parameters

parameters are used when we define the function, arguments are used when we call the function

## Default Parameters and Keyword Arguments

### Default Arguments

```python
def say_hello(name='sirui', emoji='smile'):
    pass
```

### Keyword Arguments

```python
def say_hello(name, emoji):
    pass

say_hello(emoji='smile', name='sirui')
say_hello(name='sirui', emoji='smile')
say_hello('sirui', 'smile')
```

## return

```python
def sum(num1, num2):
    return num1 + num2
```

### inner function

```python
def sum(num1, num2):
    def another_func(num1, num2):
        return num1 + num2
    return another_func(num1, num2)
```

## Doctrings

```python
def test(message):
    """
    Info: this function tests and prints param message
    """
    print(message)
```

### `help()`

The `help()` function is used to display the documentation of modules, functions, classes, keywords, etc

```python
help(test)
# test(message)
#    Info: this function tests and prints param message
```

### `__doc__`

The docstring can be accessed using the `__doc__` method of the object or using the help function

```python
print(test.__doc__)
Info: this function tests and prints param message
```

## `*args` and `**kwargs`

### `*args` for Non-Keyword Arguments

This special syntax is used to pass a variable number of arguments to a function.

- `*` is used to indicates taking a number of arguments; by convention, it is used with `args`
- `*args` allows you to take in more arguments that formal arguments that you previously defined
- Using `*args`, the variable that we associate with the `*` becomes an iterable.

```python
def test(*args):
    print(args)


test('one', 'two', 'three', 'four')
# ('one', 'tow', 'three', 'four')
test(1, 2, 3, 4)
# (1, 2, 3, 4)
```

### `**kwargs` for keyworded, variable-length argument list

`**kwargs` allows us to pass through any number of keyword arguments

- keyword arguments is passed into the function with a name
- you can think of the `kwargs` as being a dictionary that maps each keyword to the value that we pass alongside it.

```python
def test(*args, **kwargs):
    print(kwargs)
    total = 0
    for item in kwargs.values():
        total += item
    return sum(args) + total


print(test(1, 2, 3, 4, five=5, six=6))
# {'five': 5, 'six': 6}
# 21
```

**Rule:** `params`, `*args`, `default parameters`, `**kwargs`
`default parameters:` like `name='sirui'`

## walrus operator `:=`

`:=` is used to assigns values to variables as part of a larger expression.

```python
if (n := len(a)) > 10:
    print(f"List is too long ({n} elements, expected <= 10)")
```

## `global` keyword

`global` allows a user to modify a variable outside of the current scope. It is used to create global variables from a non-global scope.

Rules for global keyword:

- variables that are only referenced inside a function are implicitly global
- we use `global` keyword to use a global variable inside a function

```python
total = 0


def count():
    global total
    total += 1


count()
count()
count()
count()

print(total)
# 4
```

## `nonlocal` keyword

`nonlocal` is used to reference a variable in the nearest scope.
`nonlocal` won't work on local or global variables and therefore must be reference variables in another scopes except in the global and local one.
The `nonlocal` keyword is used in nested functions to reference a variable in the parent function.

```python
def foo():
    name = 'sirui'
    def bar():
        nonlocal name
        name = 'sirui zhang'

    bar()
    print(name)

foo()
# sirui zhang
```
