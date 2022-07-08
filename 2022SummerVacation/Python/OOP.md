# Object Oriented Programming

## Creating Objects

```python
class PlayerCharacter:
    def __init__(self, name):
        self.name = name

    @staticmethod
    def run():
        print('run')


player = PlayerCharacter('test')
player.attack = 50 
player.run()
print(player.name)
```

## attributes and methods

### attributes

```python
class PlayerCharacter:
    membership = True
    
    def __init__(self, name):
        self.name = name
```

membership is the `class attribute`
name is the `instance/object attribute`

### methods

```python
class PlayerCharacter:
    membership = True
    
    def __init__(self, name):
        self.name = name

    def shout(self):
        print(f'my name is {self.name}')
```

### `__init__`

the constructor, get called every time we create a new instance of the object

```python
class Player:
    __init__(self, name='anonymous'):
        self.name = name
```

### `@classmethod` `@staticmethod`

`@classmethod`

```python
class Calculator:
    @classmethod
    def add_things(cls, num1, num2):
        return num1 + num2


print(Calculator.add_things(1, 3))
```

`@staticmethod`

```python
class Calculator:
    @staticmethod
    def add_things(num1, num2):
        return num1 + num2


print(Calculator.add_things(1, 3))
```

## Encapsulation

## Abstraction

## Private vs Public Variables

there is no true private variables in python

```python
class Player:
    def __init__(self, name, age):
        self._name = name
        self._age = age
```

in python, by convention, we use `_` to indicate private variable

## Inheritance

```python
class User:
    @staticmethod
    def sign_in():
        print('logged in')


class Wizard(User):
    def __init__(self, name, power):
        self.name = name
        self.power = power

    def attack(self):
        print(f'attacking with power of {self.power}')


class Archer(User):
    def __init__(self, name, num_arrows):
        self.name = name
        self.num_arrows = num_arrows

    def attack(self):
        print(f'attacking with arrows:'
              f' arrows left-{self.num_arrows}')


wizard1 = Wizard('Merlin', 50)
archer1 = Archer('Robin', 100)
wizard1.sign_in()
wizard1.attack()
archer1.attack()
```

### `isinstance()`

The `isinstance()` function returns `True` if the specified object is of the specified type, otherwise `False`

## Polymorphism

## `super()`

```python
class User:
    def __init__(self, email):
        self.email = email


class Wizard(User):
    def __init__(self, email):
        super().__init__(email)
```

## Dunder Methods

```python
class Toy:

    def __init__(self, color, age):
        self.color = color
        self.age = age
        self.my_dict = {
            'name': 'yoyo',
            'has_pets': False
        }

    def __str__(self):
        return f'{self.color}'

    def __len__(self):
        return 5

    def __call__(self):
        return 'yess?'

    def __getitem__(self, i):
        return self.my_dict[i]


toy = Toy('red', 10)

print(str(toy))
# red
print(len(toy))
# 5
print(toy())
# yess?
print(toy['name'])
# yoyo
```

## Multiple Inheritance

```python
class Hybrid(Wizard, Archer):
    pass
```

not recommended

## `MRO` method resolution order

???
