# IBM_c4_m3

## Conditions and Branching:

### 1. Boolean Expressions & Truthy/Falsey Values

At its core, conditions evaluate to a Boolean value—either `True` or `False`. In Python, any expression that can be interpreted as a Boolean falls into one of these categories:

- **Truthy:** Values that evaluate to `True` such as non-zero numbers, non-empty strings, lists, etc.
- **Falsey:** Values that evaluate to `False` such as `0`, `None`, empty sequences (`""`, `[]`, `{}`), and so on.

For instance:

```python
if 5:
    print("This prints because 5 is truthy.")

if "":
    print("This won't print because an empty string is false.")
```

Understanding truthy versus falsey concepts is fundamental when you write conditions that operate implicitly on non-Boolean data types.

### 2. Comparison and Logical Operators

Conditions are built using comparison operators and can be combined with logical operators.

### **Comparison Operators**

These operators compare two values:

| Operator | Meaning | Example |
| --- | --- | --- |
| `==` | Equal to | `5 == 5` → `True` |
| `!=` | Not equal to | `5 != 3` → `True` |
| `<` | Less than | `3 < 5` → `True` |
| `>` | Greater than | `7 > 2` → `True` |
| `<=` | Less than or equal to | `3 <= 3` → `True` |
| `>=` | Greater than or equal | `5 >= 2` → `True` |

### **Logical Operators**

These combine multiple conditions:

- **`and`** — both conditions must be `True`.
- **`or`** — at least one condition must be `True`.
- **`not`** — reverses the truth value.

**Example:**

```python
age = 25
income = 45000

if age > 18 and income > 30000:
    print("Eligible for the loan application.")
```

### 3. The `if`, `elif`, and `else` Statements

These statements allow your program to branch based on conditions.

### **Basic `if` Statement**

When the condition is `True`, the block of code inside the `if` statement executes:

```python
x = 10

if x > 5:
    print("x is greater than 5.")
```

### **`if...else` Statement**

If the `if` condition is `False`, the `else` block executes:

```python
x = 2

if x > 5:
    print("x is greater than 5.")
else:
    print("x is not greater than 5.")
```

### **`if...elif...else` Chain**

When you have multiple conditions to check, use `elif`:

```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
else:
    print("Grade: D")
```

This structure is especially useful for data validation, grading systems, or categorizing data records.

### 4. Nested Conditions

Conditions can be nested within one another to handle more complex decision trees.

**Example:**

```python
temperature = 28
humidity = 85

if temperature > 25:
    if humidity > 80:
        print("It feels hot and humid!")
    else:
        print("It's warm, but the air is dry.")
else:
    print("The weather is cool.")

```

While nested conditions provide flexibility, be cautious with deep nesting as it can make your code harder to read. Consider refactoring into functions if it becomes too complex.

### 5. The Ternary (Conditional) Operator

For simple conditional assignments, you can use Python’s inline conditional expression (also known as the ternary operator):

```python
age = 17
status = "adult" if age >= 18 else "minor"
print("Status:", status)
```

This one-liner is perfect for straightforward decisions where a full `if...else` statement might be overkill.

### 6. Combining Conditions

You can group conditions using parentheses to ensure the intended order of evaluation:

```python
a = 10
b = 20
c = 5

if (a < b) and (a > c):
    print("a is between b and c in a logical context.")
```

Using parentheses improves readability and makes complex conditions easier to debug.

### 7. Real-World Relevance

- **Data Filtering:**
    
    Conditions are used extensively in filtering datasets. For example, when cleaning data with Pandas, you might use conditions to select rows with valid data:
    
    ```python
    # Example with Pandas:
    # df[df['age'] >= 18] selects rows where age is at least 18.
    ```
    
- **User Input Validation:**
    
    Verifying that user input meets certain criteria before processing ensures robust data pipelines.
    
- **Error Handling:**
    
    Conditions help in checking preconditions (such as file existence or valid numerical ranges) before executing further code, thus reducing runtime errors.
    

## 8. Hands-On Exercises

1. **Age and Income Categorization:**
    
    Write a program that checks if a person is eligible for a premium credit card based on age and income:
    
    ```python
    age = 30
    income = 70000
    
    if age >= 25 and income >= 60000:
        print("Eligible for premium credit card.")
    else:
        print("Not eligible for premium credit card.")
    ```
    
2. **Grade Calculation:**
    
    Create a small program that assigns a letter grade based on a numeric score using an `if...elif...else` chain.
    
    ```python
    score = 78
    
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"
    
    print("Score:", score, "Grade:", grade)
    ```
    
3. **Complex Condition with Nested If Statements:**
    
    Write a program to evaluate if a student qualifies for passing a course based on attendance and exam scores.
    
    ```python
    attendance = 80  # in percentage
    exam_score = 75  # out of 100
    
    if attendance >= 75:
        if exam_score >= 70:
            print("Student has passed!")
        else:
            print("Insufficient exam score, despite good attendance.")
    else:
        print("Poor attendance. Student has not passed.")
    ```
    

---

## Loops

Loops let you execute a block of code repeatedly until a certain condition is met. They are indispensable when you need to process collections of data, perform repetitive tasks, or carry out computations that require iteration.

### 1. The `for` Loop

The `for` loop in Python is used to iterate over a sequence (such as lists, strings, tuples, dictionaries, sets, or even file objects). Instead of looping over an index as in some other languages, Python's `for` loop directly traverses the elements of the collection.

### Basic Syntax

```python
for element in iterable:
    # Execute statements using element
```

**Example – Iterating Over a List:**

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

In this example, the loop iterates over each element in the `fruits` list and prints it.

### Iterating Over Other Data Structures

- **Strings:**
    
    ```python
    word = "Python"
    for letter in word:
        print(letter)
    ```
    
- **Dictionaries:**
    
    You can iterate over keys, values, or both:
    
    ```python
    student = {"name": "Alice", "age": 22, "major": "Data Science"}
    # Iterate over keys
    for key in student:
        print(key, student[key])
    # Or iterate using items()
    for key, value in student.items():
        print(key, ":", value)
    ```
    
- **Using `enumerate()`:**
    
    When you need both the index and the element, use `enumerate()`:
    
    ```python
    colors = ["red", "green", "blue"]
    for index, color in enumerate(colors):
        print(f"Color {index}: {color}")
    ```
    

### 2. The `while` Loop

The `while` loop executes as long as a condition remains true. It is useful when the number of iterations is not predetermined.

### Basic Syntax

```python
while condition:
    # Execute statements
```

**Example – Counting with a `while` Loop:**

```python
count = 1
while count <= 5:
    print("Count:", count)
    count += 1  # Make sure to modify the variable to avoid an infinite loop!
```

### Avoiding Infinite Loops

Always ensure that the loop’s condition will eventually be false. A common pitfall is forgetting to update the condition:

```python
# Incorrect Example – This loop never ends!
# while True:
#     print("This is an infinite loop!")
```

You can break out of an infinite loop using control statements, as we'll see next.

### 3. Loop Control Statements

Python provides additional commands to control loop execution:

### `break`

The `break` statement immediately exits the current loop, even if the condition is still true. This is useful if you need to stop processing when a condition is met.

```python
for num in range(1, 11):
    if num == 5:
        break  # Exit loop when num equals 5
    print(num)
```

### `continue`

The `continue` statement skips the rest of the current iteration and moves to the next one.

```python
for num in range(1, 6):
    if num == 3:
        continue  # Skip the number 3
    print(num)
```

### The `else` Clause on Loops

Both `for` and `while` loops can have an `else` clause that executes if the loop completes normally (i.e., it did not encounter a `break` statement).

```python
for num in range(1, 4):
    print(num)
else:
    print("Loop completed without break.")

# If break is used:
for num in range(1, 4):
    if num == 2:
        break
    print(num)
else:
    print("This will not print because the loop was broken.")
```

The `else` clause is particularly useful when searching for an item in a sequence. If the search loop exits without finding the target (and thus without breaking), the `else` block can handle the "not found" case.

### 4. Nested Loops

Nested loops are loops within loops. They are helpful when working with multi-dimensional data or scenarios where you need to combine iterations.

**Example – Printing a Multiplication Table:**

```python
for i in range(1, 4):  # Outer loop for rows
    for j in range(1, 4):  # Inner loop for columns
        print(f"{i * j:2}", end=" ")  # Multiply and format output
    print()  # Newline after each row
```

In this example, the inner loop runs completely every time the outer loop iterates once.

### 5. Best Practices for Using Loops

- **Keep It Simple:**
    
    Design your loops to do one clear task. Complex logic within loops can become hard to read and debug.
    
- **Avoid Deep Nesting:**
    
    Deeply nested loops can quickly become confusing. If you find yourself nesting more than two or three levels, consider refactoring your approach into functions.
    
- **Use Descriptive Variable Names:**
    
    Informative names for loop variables and counters can greatly improve code clarity.
    
- **Leverage Python’s Built-In Functions:**
    
    Python offers many built-ins (like `enumerate()`, `zip()`, and comprehensions) that can simplify your loops and make your code more expressive.
    
- **Be Cautious with Infinite Loops:**
    
    Always ensure your loop conditions lead to termination. If using a `while` loop, confirm that the condition will eventually become `False`.
    

### 6. Real-World Examples of Loops

- **Data Processing:**
    
    Iterate over rows in a dataset (using a list of dictionaries or a Pandas DataFrame) to perform data cleaning, transformation, or aggregation.
    
- **Searching and Filtering:**
    
    Loop through items to find ones that meet specific conditions (e.g., filtering data based on a threshold).
    
- **Simulation and Modeling:**
    
    Repeatedly simulate events in scientific computations or process large amounts of real-world data.
    
- **Automation Tasks:**
    
    Automate repetitive tasks, such as file processing or web scraping, by looping through directories or network responses.
    

### 7. Hands-On Exercises

1. **Sum Calculation:**
    
    Write a program using a `while` loop that calculates the sum of numbers from 1 to 100.
    
    ```python
    total = 0
    num = 1
    while num <= 100:
        total += num
        num += 1
    print("Sum from 1 to 100:", total)
    ```
    
2. **User Input Validation:**
    
    Write a program that asks the user to enter a password. Use a loop to repeatedly prompt until the provided password matches a preset correct value.
    
    ```python
    correct_password = "data123"
    while True:
        password = input("Enter the password: ")
        if password == correct_password:
            print("Access granted!")
            break
        else:
            print("Wrong password, try again.")
    ```
    
3. **Loop with `else`:**
    
    Create a search program in a list of fruits. If a fruit is found, print it with a message. Otherwise, use the `else` clause to print that the fruit was not found.
    
    ```python
    fruits = ["apple", "banana", "cherry"]
    search_item = "grape"
    for fruit in fruits:
        if fruit == search_item:
            print(f"{search_item} found!")
            break
    else:
        print(f"{search_item} not found in the list.")
    ```
    

---

## Functions

### 1. What Is a Function?

A **function** is a named block of code that encapsulates a particular task or related group of tasks. Once defined, you can call (or invoke) a function anywhere in your program, optionally passing data (arguments) to it, and it can return a result. Functions form the building blocks of a well-organized codebase.

**Key Benefits:**

- **Reusability:** Write code once and reuse it in many places.
- **Modularity:** Break complex operations into simple, logical pieces.
- **Abstraction:** Hide implementation details and expose clear interfaces.
- **Testing & Maintenance:** Smaller functions mean easier debugging and testing.

### 2. Defining a Function

You define a function using the `def` keyword, followed by a function name, parameters (if any), a colon, and an indented block of code. Optionally, you can include a docstring (a documentation string) to describe what the function does.

**Basic Syntax:**

```python
def function_name(parameters):
    """
    Docstring: Explains what the function does.
    """
    # Code that performs the task
    return result  # Optional
```

**Example – A Simple Greeting Function:**

```python
def greet(name):
    """
    Prints a welcome message for the given name.
    """
    message = f"Hello, {name}! Welcome to the world of Python."
    print(message)

# Calling the function
greet("Vybhav")
```

### 3. Function Parameters and Arguments

### a. Positional Arguments

Values are passed to parameters in the order they appear.

```python
def multiply(a, b):
    return a * b

result = multiply(3, 4)  # 3 is assigned to a and 4 to b, result is 12
```

### b. Default Arguments

You can assign default values to parameters. If no argument is provided, the default is used.

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("Alice"))             # Uses default greeting, outputs "Hello, Alice!"
print(greet("Bob", greeting="Hi"))  # Overrides default, outputs "Hi, Bob!"
```

### c. Keyword Arguments

When calling a function, specify arguments by parameter name.

```python
def power(base, exponent):
    return base ** exponent

# Calling with keyword arguments (order doesn't matter)
print(power(exponent=3, base=2))  # Outputs: 8
```

### d. Arbitrary Arguments (`args` and `*kwargs`)

- **`args`** allows you to pass a variable number of **positional arguments**.
- **`*kwargs`** allows you to pass a variable number of **keyword arguments**.

```python
def summarize(*args, **kwargs):
    # args is a tuple of positional arguments
    total = sum(args)

    # kwargs is a dictionary of keyword arguments
    message = kwargs.get("message", "Sum is")

    return f"{message}: {total}"

print(summarize(1, 2, 3, message="Total"))  # Outputs: "Total: 6"
```

### 4. Return Values

A function can return data using the `return` statement. If no return is specified, Python returns `None` by default.

**Example – A Function That Computes Factorial:**

```python
def factorial(n):
    """
    Returns the factorial of a non-negative integer n.
    """
    # Base case
    if n == 0 or n == 1:
        return 1

    # Recursive computation
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

print(factorial(5))  # Outputs: 120 because 5*4*3*2*1 = 120
```

### 5. Function Scope and Variable Lifetime

### a. Local vs. Global Variables

- **Local Variables:** Defined within a function and accessible only there.
- **Global Variables:** Defined outside functions and accessible throughout the module unless shadowed by local names.

```python
global_var = "I am global"

def test_scope():
    local_var = "I am local"
    print(global_var)  # Accesses the global variable
    print(local_var)

test_scope()
# print(local_var)  # This would raise an error; local_var is not defined outside
```

### b. The `global` Keyword

You can use `global` to modify a global variable within a function.

```python
counter = 0

def increment():
    global counter
    counter += 1

increment()
print(counter)  # Outputs: 1

```

### 6. Advanced Topics

### a. Nested Functions and Closures

Functions can be defined inside other functions. A **closure** occurs when a nested function captures the local variables of its enclosing function even after the outer function has finished executing.

```python
def outer(message):
    def inner():
        print(f"Message: {message}")
    return inner

func = outer("Hello from closure!")
func()  # The inner function "remembers" the message
```

### b. Lambda Functions (Anonymous Functions)

Lambdas are short, anonymous functions defined with the `lambda` keyword.

```python
square = lambda x: x ** 2
print(square(5))  # Outputs: 25

# Often used in higher-order functions:
numbers = [1, 2, 3, 4]
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(squared_numbers)  # Outputs: [1, 4, 9, 16]
```

### c. Decorators

Decorators are a powerful tool that allows you to modify the behavior of functions or classes. They take a function as an argument, add functionality, and return it, all without modifying the original code.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before the function call")
        result = func(*args, **kwargs)
        print("After the function call")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    print(f"Hello, {name}!")

say_hello("Vybhav")

```

In this example, the `@my_decorator` syntax is a shorthand that applies the decorator to `say_hello`.

### d. Recursion

A function can call itself to solve smaller instances of the same problem. Recursion is useful for tasks such as traversing tree-like structures or solving factorials.

```python
def fibonacci(n):
    """
    Returns the n-th Fibonacci number.
    """
    # Base cases
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # Outputs: 8 (sequence: 0, 1, 1, 2, 3, 5, 8, ...)

```

*Note:* Be cautious with recursion as it can lead to performance issues and hitting the recursion depth limit in Python for large `n`.

### 7. First-Class Functions

In Python, functions are first-class citizens, which means:

- They can be assigned to variables.
- They can be passed as arguments to other functions.
- They can be returned from another function.

```python
def shout(text):
    return text.upper()

def whisper(text):
    return text.lower()

def speak(func, message):
    # Here, func is a function passed as an argument
    print(func(message))

speak(shout, "Hello")
speak(whisper, "Hello")
```

This concept is often used for creating flexible, higher-order functions that help build more abstract and reusable code modules.

### 8. Best Practices for Writing Functions

- **Single Responsibility Principle:** Each function should have a single, well-defined purpose.
- **Clear Naming:** Use descriptive names for functions and parameters to make your code self-documenting.
- **Documentation:** Always include a docstring for your functions to explain what they do, outline parameters, and specify what they return.
- **Avoid Side-Effects:** Try to write functions that do not alter global state, which makes testing and reusability easier.
- **Modularity:** Breakdown complex operations into smaller functions.
- **Testing:** Write tests for your functions to ensure correctness across various cases.

### 9. Real-World Relevance

For a data analyst:

- **Data Transformation & Cleaning:** Functions let you modularize processes for cleaning, transforming, and processing data.
- **Reporting:** Use functions to generate sections of reports or visualizations.
- **Automation of Repetitive Tasks:** From querying databases to generating summary statistics, functions make your code DRY (Don't Repeat Yourself) and easier to maintain.
- **Modular Pipelines:** In a data pipeline, each step (extraction, transformation, loading) can be encapsulated in functions that can be tested independently and reused across projects.

### 10. Hands-On Exercises

1. **Write a Calculator Function:**
    
    Create a function that takes two numbers and an operator (as a string: `'+'`, `'-'`, `'*'`, or `'/'`) and returns the result of the corresponding arithmetic operation.
    
    ```python
    def calculator(a, b, operator):
        if operator == '+':
            return a + b
        elif operator == '-':
            return a - b
        elif operator == '*':
            return a * b
        elif operator == '/':
            # Handle division by zero
            return a / b if b != 0 else "Division by zero is not allowed."
        else:
            return "Invalid operator!"
    
    print(calculator(10, 5, '+'))  # Outputs: 15
    print(calculator(10, 0, '/'))  # Outputs: Division by zero is not allowed.
    ```
    
2. **Recursive Factorial:**
    
    Write a recursive function to compute the factorial of a number.
    
    ```python
    def factorial(n):
        if n <= 1:
            return 1
        else:
            return n * factorial(n - 1)
    
    print(factorial(5))  # Outputs: 120
    ```
    
3. **Decorator Practice:**
    
    Create a decorator that logs the time a function takes to execute.
    
    ```python
    import time
    
    def timing_decorator(func):
        def wrapper(*args, **kwargs):
            start_time = time.time()
            result = func(*args, **kwargs)
            end_time = time.time()
            print(f"{func.__name__} executed in {end_time - start_time:.4f} seconds")
            return result
        return wrapper
    
    @timing_decorator
    def compute_sum(n):
        total = 0
        for i in range(n):
            total += i
        return total
    
    print(compute_sum(1000000))
    ```
    

---

## Exception Handling

### 1. What Are Exceptions?

Exceptions are events that occur during the execution of your program and disrupt its normal flow. They represent errors or unusual conditions (like dividing by zero, accessing a non-existent file, or converting invalid data formats) that can be caught and handled.

- **Runtime Errors:** These happen while your code is running.
- **Syntax Errors:** These are caught prior to execution by the Python interpreter (and are not handled with try/except).

For data analysts, robust exception handling prevents your data pipelines or analysis scripts from crashing unexpectedly and allows you to provide meaningful error messages or recover gracefully.

### 2. The Basic Try-Except Structure

The simplest form of exception handling uses the `try` and `except` blocks. The code that might generate an error is placed inside the `try` block, and the `except` block catches and handles the error.

**Example:**

```python
try:
    numerator = 10
    denominator = 0
    result = numerator / denominator  # This will raise a ZeroDivisionError.
except ZeroDivisionError as e:
    print(f"Error encountered: {e}")
```

In the above code:

- The division by zero is caught by the `except` clause.
- The error message, accessible as the variable `e`, informs you about the issue.

### 3. The Else and Finally Clauses

Python allows you to extend the try-except block with two additional clauses:

### Else Clause

- **Purpose:** Executes only if no exception occurs within the try block.
- **Usage:** Place code here that should run if the try block is successful.

**Example:**

```python
try:
    result = numerator / 2  # Assuming denominator here is non-zero.
except ZeroDivisionError:
    print("Division error!")
else:
    print("Division succeeded, result is:", result)
```

### Finally Clause

- **Purpose:** Executes regardless of whether an exception was raised or not.
- **Usage:** Ideal for cleanup tasks, such as closing files or releasing resources.

**Example:**

```python
try:
    f = open("data.csv", "r")
    data = f.read()
except FileNotFoundError as e:
    print("File not found:", e)
else:
    print("File read successfully!")
finally:
    f.close()  # Ensures the file is closed whether or not an error occurred.

```

### 4. Catching Specific Exceptions Versus a General Exception

It’s best practice to catch specific exceptions rather than using a bare `except:`. This way, you handle known error types without inadvertently silencing unexpected issues.

**Example:**

```python
def process_number(value):
    try:
        # Try converting input to integer.
        number = int(value)
    except ValueError as ve:
        print("ValueError:", ve)
    else:
        print("The processed number is:", number)

process_number("123")  # Works fine.
process_number("abc")  # Raises ValueError and is caught.
```

Catching general exceptions should be done sparingly:

```python
try:
    # Some risky operation.
    risky_operation()
except Exception as e:
    print("An error occurred:", e)
```

### 5. Raising Exceptions

You can raise exceptions deliberately using the `raise` statement. This is useful for enforcing conditions or signaling that something has gone wrong.

**Example:**

```python
def check_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative!")
    print(f"Age is {age}")

# Uncommenting the following line will raise a ValueError.
# check_age(-5)
```

By manually raising exceptions, you ensure your functions validate inputs and signal incorrect usage clearly.

### 6. Custom Exceptions

For more clarity and control, you can define your own exception classes by subclassing Python's built-in `Exception` class. This approach is particularly useful in larger projects or libraries, where you want to create a hierarchy of meaningful error types.

**Example:**

```python
class DataValidationError(Exception):
    """Exception raised for errors in the input data."""
    def __init__(self, message):
        super().__init__(message)
        self.message = message

def validate_data(data):
    if not isinstance(data, list):
        raise DataValidationError("Data must be a list!")
    print("Data is valid.")

try:
    validate_data("not a list")
except DataValidationError as dve:
    print("Custom Exception caught:", dve)
```

Custom exceptions ensure that error messages are tailored to the domain of your application (e.g., data validation errors for a data pipeline).

### 7. Best Practices in Exception Handling

1. **Catch Specific Exceptions:**
    
    Target known exceptions (like `ZeroDivisionError`, `FileNotFoundError`) to prevent masking unexpected issues.
    
2. **Clean Up Resources:**
    
    Use the `finally` block (or context managers with the `with` statement) to ensure resources (files, network connections) are always released.
    
3. **Avoid Silent Failures:**
    
    Don’t use a bare `except:` silently. At the very least, log the exception so you have a record of what went wrong.
    
4. **Provide Useful Error Messages:**
    
    When raising exceptions, include sufficient detail so that debugging is easier.
    
5. **Keep Exception Handling Separate:**
    
    Large try-except blocks can become hard to read. Consider breaking down your code into smaller functions and handling exceptions close to where they occur.
    
6. **Use Context Managers:**
    
    Python’s context managers (using the `with` statement) often wrap exception handling for file operations and other resources, making code cleaner.
    

**Example with a Context Manager:**

```python
try:
    with open("data.csv", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("Could not find the file 'data.csv'.")
```

### 8. Real-World Relevance for Data Analysts

- **Data Pipelines:**
    
    Exception handling ensures that data processing pipelines continue running even when encountering corrupt data, missing files, or connection issues.
    
- **User Input Validation:**
    
    It is crucial when dealing with user-provided data (such as configurations, file paths, or numeric inputs) to validate inputs and handle errors gracefully.
    
- **Automation & Scripting:**
    
    In automated reporting or analysis scripts, you can catch exceptions to log errors and minimize downtime.
    

### 9. Sample Comprehensive Scenario

Imagine you're writing a function to load and process a CSV file. Instead of crashing if the file is missing or if the content is malformed, your code might look like this:

```python
import csv

def load_csv(filename):
    try:
        with open(filename, newline="") as csvfile:
            reader = csv.DictReader(csvfile)
            data = [row for row in reader]
    except FileNotFoundError as fnf_error:
        print(f"Error: {fnf_error}")
        data = []  # Return an empty list or handle appropriately.
    except csv.Error as csv_error:
        print("CSV processing error:", csv_error)
        data = []  # Handle CSV-specific errors.
    else:
        print("CSV loaded successfully, total records:", len(data))
    finally:
        print("Finished processing the file.")
    return data

# Load a CSV file safely.
dataset = load_csv("sales_data.csv")
```

This example demonstrates how you can:

- Manage multiple potential sources of error.
- Use `else` to confirm success.
- Use `finally` to execute cleanup or logging code regardless of the outcome.

---

## Classes and Objects

In Python, **everything is an object**—from simple data types like integers and strings to complex user-defined structures.

### 1. The Basics: Classes and Objects

### What Is a Class?

A **class** is a blueprint for creating objects (instances). It defines the data attributes (state) and methods (behavior) that the objects created from it will possess. Think of a class as a template, while an object is an instance built from that template.

### What Is an Object?

An **object** is a specific instance of a class. It has its own unique state (via attributes) and can perform actions defined by its class (via methods).

**Example:**

```python
class Car:
    def __init__(self, brand, model, year):
        """Constructor: Initializes a new Car object."""
        self.brand = brand    # Instance attribute
        self.model = model    # Instance attribute
        self.year = year      # Instance attribute

    def drive(self):
        """An instance method that simulates driving."""
        print(f"The {self.brand} {self.model} is now driving.")

# Creating an object (instance) of the Car class
my_car = Car("Toyota", "Corolla", 2020)

# Accessing attributes and methods
print(my_car.brand)   # Outputs: Toyota
my_car.drive()        # Outputs: The Toyota Corolla is now driving.
```

In this example:

- `Car` is a class with a constructor method `__init__` that initializes each object with specific values.
- `my_car` is an object (or instance) of the class `Car`.

### 2. Attributes and Methods

### Attributes

- **Instance Attributes:** These belong to each individual object.
    
    In the example above, `brand`, `model`, and `year` are instance attributes, specific to every `Car` object created.
    
- **Class Attributes:** These are attributes common to all instances of the class.
    
    ```python
    class Car:
        wheels = 4  # Class attribute, common for all cars
    
        def __init__(self, brand, model):
            self.brand = brand
            self.model = model
    
    car1 = Car("Honda", "Civic")
    car2 = Car("Ford", "Focus")
    print(car1.wheels)  # Outputs: 4
    print(car2.wheels)  # Outputs: 4
    ```
    

### Methods

- **Instance Methods:** Regular functions defined within a class that operate on instances. They always take `self` as the first parameter.
- **Class Methods:** Defined with the `@classmethod` decorator and take `cls` (class itself) as the first parameter. They can access class attributes and methods.
- **Static Methods:** Defined with the `@staticmethod` decorator that does not take `self` or `cls` as a parameter. They behave like regular functions but live in the class’s namespace.

**Example of all three:**

```python
class MathOperations:
    multiplier = 2  # Class attribute

    def __init__(self, value):
        self.value = value  # Instance attribute

    def double(self):
        """Instance method: returns value multiplied by 2."""
        return self.value * 2

    @classmethod
    def multiply(cls, a, b):
        """Class method: multiplies a and b, then applies a class multiplier."""
        return cls.multiplier * a * b

    @staticmethod
    def add(a, b):
        """Static method: simple addition of a and b."""
        return a + b

# Using the instance method
op = MathOperations(5)
print(op.double())  # Outputs: 10

# Using the class method
print(MathOperations.multiply(3, 4))  # Outputs: 24 (2 * 3 * 4)

# Using the static method
print(MathOperations.add(3, 4))  # Outputs: 7
```

### 3. Special Methods (Dunder Methods)

Special methods, often known as **dunder (double underscore) methods**, allow you to define how objects behave with built-in Python operations.

- **`__init__`:** Called when an object is instantiated.
- **`__str__` and `__repr__`:** Control the string representations of your objects.
- **`__len__`:** Enables the use of the `len()` function.
- **`__eq__`:** Allows comparison of equality between objects.
- **`__add__`:** Defines behavior for the addition operator (`+`).

**Example:**

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Point({self.x}, {self.y})"

    def __add__(self, other):
        if isinstance(other, Point):
            return Point(self.x + other.x, self.y + other.y)
        return NotImplemented

p1 = Point(2, 3)
p2 = Point(4, 5)
print(p1)         # Outputs: Point(2, 3)
print(p1 + p2)    # Uses __add__ and outputs: Point(6, 8)
```

Special methods make your classes feel “native” to Python and let you integrate seamlessly with built-in operations.

### 4. Inheritance and Polymorphism

### Inheritance

Inheritance allows you to create a new class (child class) that inherits attributes and methods from an existing class (parent class). This promotes code reuse and logical hierarchy.

**Example:**

```python
class Vehicle:
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def start(self):
        print("Vehicle starting...")

class Car(Vehicle):  # Car inherits from Vehicle
    def start(self):
        print(f"{self.make} {self.model} car is starting with a roar!")

my_vehicle = Vehicle("Generic", "ModelX")
my_car = Car("Tesla", "Model S")
my_vehicle.start()  # Outputs: Vehicle starting...
my_car.start()      # Outputs: Tesla Model S car is starting with a roar!
```

- **Overriding Methods:**
    
    The child class can override a parent's method (as with the `start()` method above).
    
- **Using `super()`:**
    
    Call methods from the parent class.
    
    ```python
    class Car(Vehicle):
        def start(self):
            super().start()  # Calls the parent's start() method
            print(f"{self.make} {self.model} car has ignited!")
    ```
    

### Polymorphism

Polymorphism allows methods to behave differently based on the object that is calling them. Even if two objects come from different classes, if they define a common method name, you can use them interchangeably.

**Example:**

```python
class Dog:
    def speak(self):
        print("Woof!")

class Cat:
    def speak(self):
        print("Meow!")

def animal_sound(animal):
    animal.speak()

dog = Dog()
cat = Cat()
animal_sound(dog)  # Outputs: Woof!
animal_sound(cat)  # Outputs: Meow!
```

### 5. Encapsulation and Abstraction

### Encapsulation

Encapsulation is about bundling the data (attributes) and the methods that operate on the data into a single unit (a class), and controlling access to that data. In Python, encapsulation is achieved by:

- **Public Attributes/Methods:** Accessible from anywhere.
- **Protected Attributes/Methods:** Conventionally indicated by a single underscore (e.g., `_attribute`), suggesting they should not be accessed directly.
- **Private Attributes/Methods:** Indicated by a double underscore (e.g., `__attribute`), which uses name mangling to help prevent accidental access from outside the class.

**Example:**

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner         # Public attribute
        self.__balance = balance   # Private attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print(f"Deposited {amount}.")
        else:
            print("Deposit amount must be positive.")

    def get_balance(self):
        return self.__balance

acct = Account("Alice", 1000)
acct.deposit(200)
print("Balance:", acct.get_balance())
# print(acct.__balance)  # This would raise an AttributeError.
```

### Abstraction

Abstraction means hiding the complex implementation details from the user and exposing only what is necessary. For instance, you do not need to know how a method calculates a result; you just need to know that it does.

### 6. Composition vs. Inheritance

While inheritance models "is-a" relationships, **composition** models "has-a" relationships. You can design classes that contain instances of other classes, which can be more flexible than inheritance.

**Example:**

```python
class Engine:
    def start(self):
        print("Engine starting...")

class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model
        self.engine = Engine()  # Composition: Car "has an" Engine

    def start(self):
        self.engine.start()  # Delegate to the Engine's start

my_car = Car("Ford", "Mustang")
my_car.start()  # Outputs: Engine starting...
```

### 7. Advanced Topics

### Dynamism and Reflection

Python's dynamic nature allows you to add or modify attributes of an object at runtime. You can also inspect objects using functions like `type()`, `dir()`, and `getattr()`.

```python
class DynamicExample:
    pass

obj = DynamicExample()
obj.new_attr = "I was added later"
print(obj.new_attr)  # Outputs: I was added later
print(dir(obj))      # Lists attributes of the object
```

### Properties and Decorators

You can use the `@property` decorator to create getter, setter, and deleter methods that control access to private attributes while providing an easy-to-use interface.

```python
class Temperature:
    def __init__(self, kelvin):
        self._kelvin = kelvin

    @property
    def celsius(self):
        return self._kelvin - 273.15

    @celsius.setter
    def celsius(self, value):
        self._kelvin = value + 273.15

temp = Temperature(300)
print(temp.celsius)  # Outputs: Approximately 26.85
temp.celsius = 100   # Sets the temperature appropriately in Kelvin
print(temp._kelvin)
```

### 8. Hands-On Exercises

1. **Library System:**
    - Create a `Book` class with attributes like title, author, and ISBN.
    - Create a `Library` class that contains a list of `Book` objects.
    - Implement methods to add a book, remove a book, and search for a book by title.
    
    *Hint:* Use composition to let the `Library` manage its collection of `Book` objects.
    
2. **Shape Hierarchy:**
    - Define a base class `Shape` with a method `area()` that returns `0` by default.
    - Create subclasses `Rectangle` and `Circle` that override `area()` to compute the actual area.
    - Use polymorphism to iterate through a list of shapes and print their areas.
3. **Student Record Management:**
    - Create a `Student` class that stores student details (name, ID).
    - Add methods to update scores, and use private attributes to encapsulate score data.
    - Implement a custom `__str__` method to display the student information nicely.

---