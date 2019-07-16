Here are my learning notes of Python Essential Training on Lynda
## Chapter 2: Language overview
1. Python anatomy

## Chapter 3: Types and Values
1. String
2. Numeric
3. Sequence
4. type() and id()

## Chapter 4: Conditionals

## Chapter 5: Operators
1. Arithmetic
2. Bitwise
3. Comparision
4. Operator precedence

## Chapter 6: Loops
1. while
2. for
in a sequence

## Chapter 7: Functions
1. function declaration
2. Generators
3. Decorators

## Chapter 8: Structured Data
1. Lists
List comprehension
2. Tuples
3. Dictionary
4. Sets
5. Mixed structures

## Chapter 9: Classes 
1. inheritance
## Chapter 10: Exceptions
1. what? exception is runtime error reporting mechanism and a convenient and useful way to report runtime errors. 
Python has a rich and complete system for handling excpetions.
Eg. x = int("haha") throws out ValueError; x = 5/0 throws out ZeroDIvisionError
2. template (try, except)
```python
try:
  x = 5/0
except ValueError:
  print("I caught a ValueError")
except:
  print(f"Unkown Error:{sys.exc_info()[1]}")
else:
  print('Good')
```
3. Generate your own excpetions (raise)
```python
if numargs < 1:
  raise TypeError(f'expected at least 1 argument, got{numargs}')
```

## Chapter 11: String Objects
1. common methods
2. format
3. split and join
## Chapter 12: File IO
1. open and close
2. text/binary file

## Chapter 13: Build-in Functions
1. numeric functions
2. string functions
3. container functions
4. object and class functions

## Chapter 14: Modules
1. standard modules
2. create a module
