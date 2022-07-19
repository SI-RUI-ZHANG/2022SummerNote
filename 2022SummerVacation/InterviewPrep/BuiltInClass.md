# Frequently used built in class

## `Sets()`

> A Set is an unordered collection data type, highly optimized for checking whether a specific element is contained in the set. Based on **Hash Table**. Since sets are unordered, we cannot access item with index

```python
# same as {"a", "b", "c"}
myset = set(["a", "b", "c"])
print(myset)
# {'c', 'b', a} (unordered)
```

### Methods for Sets

#### `x in s`

check for presence of `x` in set `s`
`x in s`: O(1)

#### Adding elements

`set.add(e)`: $ O(1) $

```python
people = {"Jay", "Idrish", "Archi"}
people.add("Sirui")
```

#### Union

Sets can be merged using `union()` function or `|` operator
`s1.union(s2)`: $ O(len(s1) + len(s2)) $

```python
people = {"Jay", "Idrish", "Archil"}
vampires = {"Karan", "Arjun"}
dracula = {"Deepanshu", "Raju"}
 
# Union using union()
# function
population = people.union(vampires)
 
print("Union using union() function")
print(population)
 
# Union using "|"
# operator
population = people|dracula
```

#### Intersection

By `intersection()` or `&` operator
`s1.intersection(s2)`: $ O(len(s1) + len(s2)) $

```python
# Intersection using
# intersection() function
set3 = set1.intersection(set2)
 
print("Intersection using intersection() function")
print(set3)
 
# Intersection using
# "&" operator
set3 = set1 & set2
```

#### Difference

`s1 - s2:`: $ O(len(s1)) $
