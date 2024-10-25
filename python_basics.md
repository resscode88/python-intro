## Python Classes:
A class is a blueprint for creating objects. It defines properties (attributes) and behaviors (methods) that the created objects (instances) will have.

Attributes: Variables that hold data about the object.
Methods: Functions defined inside a class that describe the behaviors of the object.
Basic Syntax for a Class:

```python
class Dog:
    # Class attribute (shared across all instances)
    species = 'Canine'

    # Initializer / Instance attributes (specific to each object)
    def __init__(self, name, age):
        self.name = name  # instance attribute
        self.age = age    # instance attribute

    # Method
    def bark(self):
        return f"{self.name} says woof!"
```

__init__(self, ...): This is the constructor method that is automatically called when a new object is created. It initializes the object's attributes.
self: Refers to the current instance of the class. It is required in methods to access instance variables and methods.

### Creating an Object (Instance):

```python

dog1 = Dog('Buddy', 5)  # Create an instance of the Dog class
print(dog1.bark())      # Output: Buddy says woof!
print(dog1.species)     # Output: Canine
```

## Python Functions:
A function is a reusable block of code that performs a specific task. It can accept input parameters and can return a result.

Basic Syntax for a Function:
```python

def greet(name):
    return f"Hello, {name}!"
```
Calling a Function:
```python

message = greet("Alice")
print(message)  # Output: Hello, Alice!
```
Functions can also accept default arguments and return multiple values.

Function with Default Parameters:
```python

def introduce(name, age=30):
    return f"My name is {name} and I am {age} years old."
```
Calling this function:

```python

print(introduce("John"))             # Output: My name is John and I am 30 years old.
print(introduce("Jane", age=25))     # Output: My name is Jane and I am 25 years old.
```
### Combining Classes and Functions:
Classes can contain multiple functions (methods) to define the behavior of the objects.

Example of a Class with Multiple Methods:
```python

class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

    def start_engine(self):
        return f"The {self.year} {self.make} {self.model}'s engine has started."

    def stop_engine(self):
        return f"The {self.year} {self.make} {self.model}'s engine has stopped."
```
Creating an instance and using its methods:

```python

my_car = Car("Toyota", "Camry", 2020)
print(my_car.start_engine())  # Output: The 2020 Toyota Camry's engine has started.
print(my_car.stop_engine())   # Output: The 2020 Toyota Camry's engine has stopped.
```
In summary, classes in Python allow you to model real-world entities, while functions help encapsulate logic. Both are essential for creating modular and maintainable code.

## what mean f"My 

In Python, f"My ..." is part of f-strings (formatted string literals), which were introduced in Python 3.6. They provide a way to embed expressions inside string literals, using curly braces {}.

The f before the string denotes that the string is a "formatted string" or f-string. It allows you to insert variables, or even expressions, directly inside the string by wrapping them in {}.

Example of an f-string:
```python

name = "Alice"
age = 30

# Using f-string to embed variables in the string
greeting = f"My name is {name} and I am {age} years old."
print(greeting)
```

Output:
```csharp

My name is Alice and I am 30 years old.
```
Key Features of f-strings:
Expression Evaluation: You can evaluate any Python expression inside the curly braces.
Type Casting: You can use built-in functions or methods inside the curly braces.

Example with Expressions:
```python

x = 10
y = 20
result = f"The sum of {x} and {y} is {x + y}."
print(result)
```
Output:
```python

The sum of 10 and 20 is 30.
```
F-strings are concise and powerful, making it easier to format strings dynamically without needing to use older methods like .format() or concatenation with +.

## Strict type syntax in functions, methods, attributes

Python supports type hints or type annotations for functions, methods, and attributes. While Python is dynamically typed (meaning it doesn’t enforce types at runtime), you can use type hints to explicitly specify the types of variables, parameters, and return values. This improves code readability, helps with documentation, and allows static type checkers (like mypy) or IDEs to catch type errors before runtime.

### Type Annotations in Functions
You can specify the types of function parameters and the return type using the following syntax:

Example:
```python

def add(a: int, b: int) -> int:
    return a + b
a: int: Specifies that the parameter a should be of type int.
-> int: Specifies that the return value of the function should be of type int.
Calling this function:
```
```python

result = add(3, 4)
print(result)  # Output: 7
```
### Type Annotations in Methods (Inside Classes)
Type annotations also work inside methods of a class.

Example:
```python

class Dog:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def bark(self) -> str:
        return f"{self.name} says woof!"
name: str: Specifies that the name parameter should be a string.
age: int: Specifies that the age parameter should be an integer.
-> str: Specifies that the method bark returns a string.
```
### Type Annotations for Attributes (Class Variables)
In Python 3.6 and later, you can annotate class attributes using type hints.

Example:
```python

class Car:
    make: str
    model: str
    year: int

    def __init__(self, make: str, model: str, year: int):
        self.make = make
        self.model = model
        self.year = year

    def start_engine(self) -> str:
        return f"{self.year} {self.make} {self.model}'s engine is starting."
```
In the above example:

make: str, model: str, and year: int annotate the class attributes with their respective types.

### Optional and Union Types
Sometimes, a parameter or attribute might accept more than one type. For example, a parameter could accept either int or None. For this, Python provides Optional and Union types from the typing module.

Example with Optional:
```python

from typing import Optional

def greet(name: Optional[str] = None) -> str:
    if name:
        return f"Hello, {name}!"
    return "Hello, guest!"
```
Optional[str]: Specifies that the name parameter can either be of type str or None.
Example with Union:
```python

from typing import Union

def add(a: Union[int, float], b: Union[int, float]) -> Union[int, float]:
    return a + b
Union[int, float]: Specifies that the parameters a and b can be either int or float.
```

### Type Checking with Static Analyzers
Although Python doesn’t enforce types at runtime, you can use static type checkers like mypy to analyze your code and ensure type correctness.

To check your code:

```bash

mypy your_code.py
```

Summary:
Type annotations provide clarity and help catch potential errors in large codebases.
Static type checking can help ensure that your code is type-safe.
Use Optional, Union, and other types from the typing module to handle more complex typing scenarios.
Here's an example combining all the concepts:

```python

from typing import Optional, Union

class Rectangle:
    width: float
    height: float

    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height

    def area(self) -> float:
        return self.width * self.height

    def resize(self, factor: Union[int, float]) -> None:
        self.width *= factor
        self.height *= factor

def describe_shape(name: Optional[str] = None) -> str:
    return f"Shape: {name}" if name else "Shape: Unknown"
```

In this example:

The Rectangle class uses type annotations for its attributes and methods.
The describe_shape function uses Optional for an optional parameter.

## variables - data types in python
In Python, variables can store different types of data, and Python handles these data types dynamically (i.e., you don’t need to explicitly declare a variable’s type). Python's data types fall into several categories, including numeric types, sequences, mappings, sets, and more.

### Common Data Types in Python
####Numeric Types

int: Integer values (positive or negative whole numbers).
float: Floating-point numbers (numbers with decimal points).
complex: Complex numbers with real and imaginary parts.

Example:
```python

x = 10      # int
y = 3.14    # float
z = 2 + 3j  # complex
```
Boolean Type

bool: Represents two values: True or False.
Example:
```python

is_active = True  # bool
```

String Type

str: A sequence of characters (text).
Example:
```python

name = "Alice"  # str
greeting = 'Hello, World!'  # str
Strings can use single quotes ' or double quotes ". Multiline strings can be created with triple quotes (''' or """).
```

List (Sequence)

list: An ordered, mutable sequence of values. Lists can hold values of different types and can be changed (mutable).
Example:
```python

numbers = [1, 2, 3, 4, 5]  # list of integers
mixed = [1, "apple", 3.14, True]  # list with mixed data types
```

Tuple (Sequence)

tuple: An ordered, immutable sequence of values. Once defined, the elements in a tuple cannot be changed.
Example:
```python

coordinates = (10.0, 20.0)  # tuple with float elements
mixed_tuple = (1, "apple", True)  # tuple with mixed data types
```

Dictionary (Mapping)

dict: An unordered collection of key-value pairs. Keys must be unique and can be of any immutable type (e.g., string, number, tuple).
Example:
```python

student = {"name": "John", "age": 20, "grades": [85, 90, 92]}  # dict with mixed values
```

Set (Collection)

set: An unordered collection of unique values. Sets do not allow duplicates and are mutable.
Example:
```python

fruits = {"apple", "banana", "cherry"}  # set
```
There is also a frozenset, which is an immutable version of a set.

NoneType

None: Represents the absence of a value or a null value. It is often used as a default value for variables or to indicate missing data.
Example:
```python

result = None  # NoneType
Examples of Using Python Data Types:
```python

# Numeric types
x = 10        # int
y = 5.5       # float
z = 2 + 3j    # complex
# Boolean

is_logged_in = True  # bool

# String
name = "Alice"  # str

# List
numbers = [1, 2, 3, 4, 5]  # list of integers

# Tuple
coordinates = (10, 20)  # tuple of integers

# Dictionary
person = {"name": "John", "age": 25}  # dict with string keys and mixed values

# Set
unique_numbers = {1, 2, 3, 3, 4}  # set with unique values (duplicate 3 is ignored)

# None
result = None  # NoneType to represent no value
```

More Complex Data Types (Collections & Other Built-ins)
Python provides additional types for more specific use cases:


bytes: Immutable sequence of bytes.

bytearray: Mutable sequence of bytes.

range: Immutable sequence of numbers, typically used in loops.

Example:

```python

numbers = range(1, 10)  # range from 1 to 9
```

frozenset: Immutable version of a set.

Example:
```python

frozen_fruits = frozenset(["apple", "banana", "cherry"])  # frozenset
```

Python also supports user-defined types using classes. This allows you to create complex objects with attributes and methods.

Example:
```python

class Dog:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age
```

Type Conversion (Casting)
You can convert between types using Python's built-in functions:

int(): Convert to integer
float(): Convert to floating-point number
str(): Convert to string
list(), tuple(), set(), etc.: Convert to respective collection types

Example:
```python

num_str = "100"
num = int(num_str)  # Converts string "100" to integer 100
Summary of Python's Basic Data Types:
Data Type	Example
int	10, -5
float	3.14, -0.001
complex	2 + 3j
bool	True, False
str	"Hello"
list	[1, 2, 3]
tuple	(1, 2, 3)
dict	{"key": "value"}
set	{1, 2, 3}
NoneType	None
These data types allow Python to handle various kinds of data in an efficient and flexible manner.
```
# loops

Loops are a way to repeatedly execute a block of code. Python supports two types of loops: `for` loops and `while` loops.

## 1. `for` Loop

The `for` loop in Python is used to iterate over a sequence (such as a list, tuple, dictionary, set, or string) or any other iterable object.

### Basic Syntax:
```python
for variable in iterable:
    # Code to execute
```

Example:
```python

fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```
```Output:

apple
banana
cherry
```
### Looping with range():
You can use the range() function to generate a sequence of numbers to loop over.

```python

for i in range(5):
    print(i)
```
```Output:

0
1
2
3
4
```
## while Loop
The while loop in Python is used to repeatedly execute a block of code as long as a given condition is True.

Basic Syntax:
```python

while condition:
    # Code to execute
```
Example:
```python

count = 0
while count < 5:
    print(count)
    count += 1
```
```Output:

0
1
2
3
4
```
## break and continue
break: Terminates the loop entirely.
continue: Skips the rest of the code inside the loop for the current iteration and jumps to the next iteration.

Example with break:
```python

for i in range(10):
    if i == 5:
        break
    print(i)
```
```Output:

0
1
2
3
4
```
Example with continue:
```python

for i in range(5):
    if i == 3:
        continue
    print(i)
```
```Output:

0
1
2
4
```
## else with Loops
Python allows an else clause with both for and while loops. The else block will be executed when the loop terminates naturally (without hitting a break).

Example:
```python

for i in range(5):
    print(i)
else:
    print("Loop completed without break.")
```

Output:
```kotlin

0
1
2
3
4
```
Loop completed without break.
## Nested Loops
A loop inside another loop is called a nested loop. You can use both for and while loops as nested loops.

Example:
```python

for i in range(3):
    for j in range(2):
        print(f"i={i}, j={j}")
```
Output:
```css

i=0, j=0
i=0, j=1
i=1, j=0
i=1, j=1
i=2, j=0
i=2, j=1
```
# Conditional Statements in Python

## 1. `if`, `elif`, and `else` Statements

In Python, conditional statements are used to perform different actions based on different conditions. The primary conditional operators in Python are `if`, `elif`, and `else`.

### Syntax:
```python
if condition1:
    # Code to execute if condition1 is True
elif condition2:
    # Code to execute if condition2 is True
else:
    # Code to execute if none of the above conditions are True
```
Example:
```python

x = 10

if x > 15:
    print("x is greater than 15")
elif x == 10:
    print("x is equal to 10")
else:
    print("x is less than 10")

Output:
```vbnet

x is equal to 10
```
## Nested if:
You can nest if statements inside other if statements.

```python

x = 10
y = 5

if x > 5:
    if y < 10:
        print("x is greater than 5 and y is less than 10")
```
Example:
```python

age = 18

if age >= 18:
    print("You are an adult.")
else:
    print("You are not an adult.")
```
## Python’s Alternative to switch-case
Python does not have a built-in switch-case statement like other languages (e.g., C, Java). However, you can achieve similar functionality using:

2.1 Using if-elif-else Chain
You can use a series of if-elif-else statements to mimic switch-case behavior.

Example:
```python

day = "Monday"

if day == "Monday":
    print("Start of the workweek.")
elif day == "Tuesday":
    print("Second day of the workweek.")
elif day == "Wednesday":
    print("Midweek.")
elif day == "Thursday":
    print("Almost Friday.")
elif day == "Friday":
    print("End of the workweek!")
else:
    print("It's the weekend!")
```

2.2 Using a Dictionary to Simulate switch-case
A more Pythonic way to simulate a switch-case is to use a dictionary where keys represent cases and values are functions or actions to be executed.

Example:
```python

def case_monday():
    return "Start of the workweek."

def case_tuesday():
    return "Second day of the workweek."

def case_default():
    return "Invalid day."

# Dictionary-based switch-case simulation
switch = {
    "Monday": case_monday,
    "Tuesday": case_tuesday
}

day = "Monday"
print(switch.get(day, case_default)())  # Output: Start of the workweek.
```

In this approach, the get() method retrieves the function for the given key (day), and case_default() acts as the default case if the key is not found.

2.3 Using match-case (Python 3.10+)
Starting from Python 3.10, Python introduced a new match-case syntax that allows pattern matching, which is very similar to switch-case.

Example:
```python

def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 401:
            return "Unauthorized"
        case 403:
            return "Forbidden"
        case 404:
            return "Not found"
        case _:
            return "Unknown error"
            
print(http_error(404))  # Output: Not found
```

The underscore (_) in match-case acts as a wildcard or default case.
match-case is a new feature and is recommended for more structured pattern matching in Python 3.10 and later.

## Conclusion
Use if-elif-else for simple conditionals.
You can simulate switch-case behavior using a dictionary or by using match-case in Python 3.10+.
match-case is the most structured approach to handling multiple conditions similar to switch-case in other languages.
