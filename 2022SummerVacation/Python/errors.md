# Errors in Python

## Error Handling

```python
while True:
    try:
        age = int(input('what is your age?'))
        print(age)
    except ValueError:
        print('please enter a number')
    else:
        print('thank you')
        break
```

```python
try:
    pass
except TypeError as err:
    print(err)
```

```python
try:
    pass
except (TypeError, ZeroDivisionError) as err:
    print(err)
```

```python
try:
    pass
except (...):
    pass
finally:
    pass
```

`break` will break out of a loop but code inside `finally` will run
`continue` ...
