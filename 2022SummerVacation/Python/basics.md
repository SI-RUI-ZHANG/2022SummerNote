# Python Basics I

>Fundamental Data Types
>
>- int
>- float
>- bool
>- str
>- list
>- tuple
>- set
>- dict
>
>Class -> custom types
>
>Specialized Data Types

`type()`: return the type of argument

```python
print(type(6))
# <class 'int'>
print(type(2/4))
# <class 'float'>
```

## Numbers

```python
print(2 ** 3)
print(5 // 4)
print(5 % 4)
```

## Math Functions

`round(number, digits)`

```python
print(round(3.1))
# 3
```

## Variables

We usually use all capital letters to indicate a constant

```python
a, b, c = 1, 2, 3
```

## Strings

```python
username = 'super coder'
password = "super secret"

long_string = '''
WOW
o o
---
'''
```

## Type conversion

- `str()`
- `int()`
- `float()`
- $\dots$

## Escape sequence

```python
weather = "It\'s \"kind of\" sunny"
```

- `\t`: tab
- `\n`: new line

## Formatted string

```python
name = "Sirui"
age = 20

print(f'hi {name}, you are {age} years old')
```

## Sting index

```python
name ='sirui zhang'
print(name[0])
# s
```

`[start:end]` (inclusive, exclusive)
`[start:end:stepover]`
`[start:]` (from start to list end)
`[:5]` (start with 0 by default)
`[:]` (copy string)
`[::1]` (copy string)
`[-1]` (last index in the list)
`[::-1]` (reverse)

## Immutability

```python
name = 'sirui'
name[0] = '1'
# error
```

## Built-In functions + Methods

```python
quote = 'to be or not to be'
quote.upper()
# 'TO BE OR NOT TO BE'
quote.capitalize()
# 'To be or not to be'
quote.find('be')
# 3
quote.replace('be', 'me')
# 'to me or not to me'
```

## Booleans `bool`

`True, False`

```python
print(bool(1))
# True
print(bool(0))
# False
```

## Lists

```python
li = [1,2,3,4,5]
li2 = ['a', 'b', 'c']
li3 = [1, 'b', True]
```

### List Slicing

```python
amazon_cart = [
    'notebooks',
    'sunglasses',
    'toys',
    'grapes'
    ]

print(amazon_cart[2:])

# copy the list
cart_two = amazon_cart[:]
```

> lists are mutable

### List Methods

`len()`: return the list of a list

#### adding

- `list.append(object)`
- `list.insert(index, object)`
- `list.extend(iterable)`
  - adds the specified list elements (or any iterable) to the end of the current list

#### removing

- `list.pop()`
  - pops off whatever at the end of the list and return it
  - `list.pop(index)`
    - pops off whatever at the index
- `list.remove(element)`
  - remove the element in list
- `list.clear`
  - clear whatever is in the list

#### other methods

```python
basket = ['a', 'b', 'c', 'd', 'e']

print(basket.index('d')
# 3
# basket.index(element, start, end)
```

`in` keyword

```python
print('x' in basket)
# False
print('a' in basket)
# True
```

`count`

```python
basket = ['a', 'b', 'c', 'd', 'd', 'e']
print(basket.count('d'))
# 2
```

`sort()`
`sorted()`
`reverse()`

### Common List patterns

`range(start, end)`

```python
print(list(range(1, 100)))
# [1, 2, 3, 4, 5, 6, 7, 8, 9, ..., 99]
```

`join()`

```python
sentence = "!"
new_sentence = sentence.join(['hi', 'my', 'name', 'is', 'jojo'])
print(new_sentence)
# hi!my!name!is!jojo
# or '!'.join()
```

### list unpacking

```python
a, b, c, *other, d = ['a', 'b', 'c', 'd', 'e']
```

## Dictionary `dict`

```python
dictionary = {
    'a': [1,2,3],
    'b': 2,
    'c': True,
    'd': 'hello'
}

print(dictionary['b'])
# 2
```

### Dictionary Keys

> a key needs to be immutable, unique

### Dictionary Methods

- `dict.get(key)`: return associated value with `key` or none
  - `dict.get(key, defaultValue)`: return associated value with `key` or `defaultValue`
- `dict()`: create a dictionary
- `in`: check if a key presents in a dictionary

```python
user = {
    'basket': [1, 2, 3],
    'greet': 'hello',
    'age': 20
}
print('basket' in user)
# True
```

- `dict.keys()`
- `dict.values()`
- `dict.items()`
- `dict.clear()`
- `dict.copy()`
- `dict.pop(key)`: pop out item with key `key` and return its `value`
- `dict.popitem()`: randomly pop out a item
- `dict.update({key: value})`: update item with key `key` or add new item in dictionary

## Tuples

An unchangeable ordered collection

```python
my_tuple = (1,2,3,4,5)
```

> tuple can serve as a key in dictionary

### Tuple Methods

`count()`
`index()`

count, find index of element in a tuple

## Sets

unordered collection of unique values

```python
my_set = {1,2,3,4,5}
my_list = [1,1,1,2]
print(list(set(my_list)))
# (1,2)
```

> set does not support indexing

- `in`
- `set.add()`
- `set.copy()`

==more==

- `set.difference(anotherSet)`
- `set.discard(element)`
- `set.difference_update(anotherSet)`
- `set.intersecton(anotherSet)`
- `set.isdisjoint()`
- `set.issubset(anotherSet)`
- `issuperset(anotherSet)`
- `set.union(anotherSet)`
