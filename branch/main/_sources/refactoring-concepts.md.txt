# Concepts in refactoring and modular code design


## Starting questions for the collaborative document

1. What does "modular code development" mean for you?
2. What best practices can you recommend to arrive at well structured,
   modular code in your favourite programming language?
3. What do you know now about programming that you wish somebody told you
   earlier?
4. Do you design a new code project on paper before coding? Discuss pros and
   cons.
5. Do you build your code top-down (starting from the big picture) or
   bottom-up (starting from components)? Discuss pros and cons.
6. Would you prefer your code to be 2x slower if it was easier to read and
   understand?


## Pure functions

- Pure functions have no notion of state: They take input values and return
  values
- **Given the same input, a pure function always returns the same value**
- Function calls can be optimized away
- Pure function == data

a) pure: no side effects
```python
def fahrenheit_to_celsius(temp_f):
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c

temp_c = fahrenheit_to_celsius(temp_f=100.0)
print(temp_c)
```

b) stateful: side effects
```python
f_to_c_offset = 32.0
f_to_c_factor = 0.555555555
temp_c = 0.0

def fahrenheit_to_celsius_bad(temp_f):
    global temp_c
    temp_c = (temp_f - f_to_c_offset) * f_to_c_factor

fahrenheit_to_celsius_bad(temp_f=100.0)
print(temp_c)
```

Pure functions are easier to:
- Test
- Understand
- Reuse
- Parallelize
- Simplify
- Optimize
- Compose


Mathematical functions are pure:
```{math}
f(x, y) = x - x^2 + x^3 + y^2 + xy
```

```{math}
(f \circ g)(x) = f(g(x))
```

Unix shell commands are stateless:
```shell
$ cat somefile | grep somestring | sort | uniq | ...
```


## But I/O and network and disk and databases are not pure!

- I/O is impure
- Keep I/O on the "outside" of your code
- Keep the "inside" of your code pure/stateless

:::{figure} img/good-vs-bad.svg
:alt: Image comparing code that is mostly impure to code where the impure parts are on the outside
:::


## From classes to functions

Object-oriented programming and functional programming **both have their place
and value**.

Here is an example of expressing the same thing in Python in 4 different ways.
Which one do you prefer?

1. As a **class**:
   ```{literalinclude} refactoring/using-class.py
   :language: python
   ```

2. As a **dataclass**:
   ```{literalinclude} refactoring/using-dataclass.py
   :language: python
   ```

3. As a **named tuple**:
   ```{literalinclude} refactoring/using-namedtuple.py
   :language: python
   ```

4. As a **dict**:
   ```{literalinclude} refactoring/using-dict.py
   :language: python
   ```


## How to design your code before writing it

- Document-driven development can be a nice approach:
  - Write the documentation/tutorial first
  - Write the code to make the documentation true
  - Refactor the code to make it clean and maintainable
- But also it's almost impossible to design everything correctly from the
  start -> make it easy to change -> keep it simple
