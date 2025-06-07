# IBM_c4_m1

## **Introduction to Python**

### 🐍 What is Python?

Python is a high-level, general-purpose programming language that is **easy to learn**, **versatile**, and **widely used in data science**. It was designed to be readable and simple, allowing beginners to pick it up quickly while remaining powerful enough for advanced applications.

### 🔥 Why is Python Important for Data Analysts?

Python is a **game-changer** in the data analytics space because:

- It has **powerful libraries** like Pandas, NumPy, Matplotlib, and Scikit-learn for data manipulation, visualization, and machine learning.
- It is **open-source**, meaning it’s free to use and has a massive **community** of developers improving it.
- It allows **automation**, reducing manual work when handling large datasets.
- It integrates well with databases, APIs, and cloud computing tools

### 📝 First Python Code: Hello, World!

Let’s write your first Python program! Open Jupyter Notebook, and type:

```python
print("Hello, World!")
```

🔍 **Explanation**:

- `print()` is a built-in function that displays output on the screen.
- `"Hello, World!"` is a string (text) that gets printed.

✅ **Try This Exercise**:

1. Modify the code to print your name instead.
2. Store your name in a **variable** and print it like this:
    
    ```python
    name = "Vybhav"
    print("Hello, " + name + "!")
    ```
    

---

## **Jupyter Notebook**

### 🧠 What is Jupyter Notebook?

Jupyter Notebook is an **interactive coding environment** that allows you to write and execute Python code **step by step**. It's widely used in data science, AI, and machine learning because:

- You can write code in small blocks (called "cells") and execute them independently.
- It supports rich outputs like tables, charts, and even interactive visuals.
- You can document your work using **Markdown**, making it easy to create notebooks with explanations and code.

### 🔥 Why is Jupyter Important for Data Analysts?

Imagine you're analyzing a large dataset—Jupyter helps you:

- **Test small sections of code** without running an entire script.
- **Keep track of experiments**, which is useful in AI and machine learning.
- **Visualize data** instantly using tools like Matplotlib and Seaborn.

### 📝 Exploring the Jupyter Interface

- **Notebook Cells** → Where you write Python code.
- **Run a Cell** → Press `Shift + Enter` to execute code.
- **Markdown Cells** → Use text formatting to document your work.
- **Save & Export** → Save notebooks as `.ipynb` or convert them to `.html`, `.pdf`, etc.

### ✨ First Jupyter Experiment:

Try running this simple code in a new Jupyter Notebook cell:

```python
# Basic Math in Jupyter
a = 10
b = 20
sum_ab = a + b
print("The sum is:", sum_ab)
```

✅ **Exercise**:

1. Modify the above code to perform **multiplication** instead of addition.
2. Create a Markdown cell and write a brief note: `"This is my first Jupyter Notebook!"`.
3. Explore the **help system** by running:
    
    ```python
    help(print)
    ```
    

---

## 📌 Presenting a Notebook Using Markdown & Code

Jupyter lets you mix **Markdown (text formatting)** with **Python code** to create **clear, well-structured notebooks** that look professional and easy to understand.

### ✨ Markdown Basics

To create a Markdown cell:

1. Select a cell.
2. Change the cell type to **Markdown** (`Cell → Cell Type → Markdown`).
3. Write text using Markdown syntax.

Here’s how you can format your presentation:

✅ **Headings (for structure)**

```markdown
# Title (Largest Heading)
## Subtitle (Medium Heading)
### Section (Smaller Heading)
```

✅ **Bold & Italics (for emphasis)**

```markdown
**Bold Text**
*Italicized Text*
```

✅ **Lists (for bullet points)**

```markdown
- First item
- Second item
   - Indented item
```

✅ **Adding Code Blocks (without execution)**

```markdown
```python
# This is a Python code snippet
print("Hello, World!")
```

```

✅ **Adding Images**
```markdown
![Python Logo](<https://www.python.org/static/community_logos/python-logo.png>)
```

### 🔥 Combining Markdown with Code for Presentations

Example of a **well-structured notebook** combining Markdown and Python:

```markdown
# 📊 Data Analysis Project

## 📌 Overview
This project analyzes sales data to identify revenue trends.

## 🔍 Loading the Dataset
We use Pandas to load and explore data.
```

```python
import pandas as pd

# Load sales data
df = pd.read_csv("sales_data.csv")

# Display first 5 rows
df.head()
```

```markdown
## 📈 Visualizing Sales Trends
We plot revenue growth over time.
```

```python
import matplotlib.pyplot as plt

# Plot sales trend
plt.plot(df["Date"], df["Revenue"])
plt.title("Sales Revenue Over Time")
plt.xlabel("Date")
plt.ylabel("Revenue")
plt.show()
```

- Use **Markdown for structure** and **Python for execution**.
- Add **comments in code cells** to explain your logic.
- Use **headers, bold text, lists, and images** to make notebooks visually appealing.
- Export your notebook (`File → Download as → HTML/PDF`) for sharing or presentations.

---

## Basic Info:

### 🐍 **Version in Python**

Python has multiple versions, and it's important to know which one you're using.

To check your **Python version**, open a terminal or command prompt and run:

```bash
python --version
```

or

```bash
import sys
print(sys.version)
```

📌 **Python 2 vs. Python 3**

- Python 2 is outdated and no longer supported.
- Python 3 (latest versions) is widely used in **data science, AI, and general programming**.

💡 **Why Python Version Matters?**

Some libraries or features work **only in specific versions**, so checking your version ensures compatibility.

### 📝 **Comments in Python**

**Comments** are lines of text **ignored by Python** but useful for explaining code.

### **Single-line Comment**

Use `#` at the beginning of a line:

```python
# This is a comment
print("Hello, World!")  # This prints a message
```

### **Multi-line Comment**

Use triple quotes (`"""` or `'''`) for multiple lines:

```python
"""
This is a multi-line comment.
Python ignores these lines.
Useful for documentation.
"""
print("Python is awesome!")
```

💡 **Why Are Comments Important?**

- Help **others (or your future self)** understand your code.
- Useful for **debugging** (temporarily removing code without deleting it).

## ❌ **Errors in Python**

Errors, also called **exceptions**, occur when something goes wrong in your code.

### **Common Errors**

1️⃣ **Syntax Error (Typing Mistake)**

```python
print("Hello"   # Missing closing parenthesis
```

🔥 **Fix:** Close the parentheses properly.

2️⃣ **Name Error (Undefined Variable)**

```python
print(my_variable)  # my_variable is not defined
```

🔥 **Fix:** Define `my_variable` before using it.

3️⃣ **Type Error (Mismatched Types)**

```python
print("Age: " + 25)  # Cannot add string and integer
```

🔥 **Fix:** Convert `25` to a string:

```python
print("Age: " + str(25))
```

4️⃣ **Index Error (Out of Range)**

```python
numbers = [1, 2, 3]
print(numbers[5])  # Index 5 does not exist
```

🔥 **Fix:** Ensure the index is within the list's range.

### 🤔 **Does Python Know Errors Before Running the Code?**

Python **does not** predict errors **before execution**, but it **checks syntax errors** before running.

- If there’s a syntax mistake, Python **stops immediately** and shows an error.
- If the error happens **while running** (e.g., dividing by zero), Python catches it at that moment.

✅ **Try This in Jupyter Notebook**

```python
print("Start")

print(10 / 0)  # ZeroDivisionError (Python detects this while running)

print("End")  # This won't execute

```

📌 Python **executes code line by line**, and stops at the first error.

### 🚀 **Basic Python Programs**

### 1️⃣ **Printing a Message**

```python
print("Hello, Data Science!")
```

### 2️⃣ **Basic Math Operations**

```python
x = 10
y = 5
sum_xy = x + y
print("Sum:", sum_xy)
```

### 3️⃣ **Using Variables**

```python
name = "Vybhav"
age = 25
print("My name is", name, "and I'm", age, "years old.")
```

### 4️⃣ **Conditional Statements**

```python
age = 18
if age >= 18:
    print("You are an adult.")
else:
    print("You are a minor.")
```

### 5️⃣ **Looping Through a List**

```python
fruits = ["Apple", "Banana", "Cherry"]
for fruit in fruits:
    print(fruit)
```

---

## Types (Data types):

### 1. **Dynamic Typing Explained**

Python is a **dynamically typed language**, meaning that you don't explicitly declare a variable's type. Instead, Python infers it at runtime. This makes coding more flexible, but it also means you should be mindful of the kinds of data your variables hold. For example, if you add an integer to a string by mistake, Python will raise an error because operations depend on data types.

### 2. **Numeric Types**

### **Integers (`int`)**

These represent whole numbers—both positive and negative (or zero).

**Example:**

```python
age = 25
year = 2025
print(type(age))  # <class 'int'>
```

### **Floating-point Numbers (`float`)**

These are for numbers that have a decimal point. They’re used when precision matters, like in calculations or measurements.

**Example:**

```python
temperature = 36.6
pi = 3.14159
print(type(temperature))  # <class 'float'>
```

### **Complex Numbers (`complex`)**

Used less frequently in data analytics and more in scientific computing, they have a real and an imaginary part.

**Example:**

```python
complex_num = 2 + 3j
print(type(complex_num))  # <class 'complex'>
```

### 3. **Boolean Type (`bool`)**

The Boolean type represents truth values: `True` or `False`. They often result from comparisons and logical operations.

**Example:**

```python
is_adult = True
result = 10 > 5  # This will return True
print(is_adult, result)
print(type(result))  # <class 'bool'>
```

### 4. **Sequence Types**

### **Strings (`str`)**

Strings are sequences of characters enclosed in single (`'...'`) or double quotes (`"..."`). They are immutable, meaning once created, their content cannot be changed.

**Example:**

```python
greeting = "Hello, Data Science!"
print(greeting)
print(type(greeting))  # <class 'str'>
```

*Tip:* Use the `+` operator to concatenate strings and slicing (`greeting[0:5]`) to extract parts.

### **Lists (`list`)**

Lists are ordered and mutable collections that can hold items of different types. They’re perfect for storing sequences of data like numbers, strings, or even other lists.

**Example:**

```python
my_list = [10, 20, "Python", True]
print(my_list)
print(type(my_list))  # <class 'list'>

# Accessing elements
print(my_list[2])  # Outputs: Python

# List operations
my_list.append("New Element")
print(my_list)
```

### **Tuples (`tuple`)**

Tuples are similar to lists, but they are immutable. Once a tuple is created, you cannot change its content. They’re useful when you want to ensure data remains constant.

**Example:**

```python
my_tuple = (1, 2, 3, "Data")
print(my_tuple)
print(type(my_tuple))  # <class 'tuple'>
```

### **Ranges (`range`)**

This type represents an arithmetic progression, often used in loops. It generates a sequence of numbers.

**Example:**

```python
numbers = range(0, 10, 2)  # start at 0, go up to 10 (exclusive), step by 2
print(list(numbers))  # Convert to list to see all values
print(type(numbers))  # <class 'range'>
```

### 5. **Mapping Type**

### **Dictionaries (`dict`)**

Dictionaries store key-value pairs and are highly useful for representing structured data. They are mutable and unordered (prior to Python 3.7, where insertion order started being preserved) but ideal for fast lookups.

**Example:**

```python
person = {
    "name": "Vybhav",
    "age": 25,
    "course": "IBM Data Analyst Professional Certificate"
}
print(person)
print(type(person))  # <class 'dict'>

# Accessing values by key
print(person["name"])
```

### 6. **Set Types**

### **Sets (`set`)**

Sets are unordered collections of unique items. They’re great for membership testing and removing duplicates.

**Example:**

```python
my_set = {1, 2, 3, 2, 1}
print(my_set)  # Outputs: {1, 2, 3}
print(type(my_set))  # <class 'set'>
```

### **Frozen Sets (`frozenset`)**

Frozen sets are just like sets but immutable. Once created, you cannot add or remove items from a frozenset.

**Example:**

```python
immutable_set = frozenset([1, 2, 3, 3])
print(immutable_set)
print(type(immutable_set))  # <class 'frozenset'>
```

### 7. **None Type**

The **`None`** type represents the absence of a value. It’s like a placeholder and can be very useful when you need to initialize variables or indicate that no valid value exists.

**Example:**

```python
no_value = None
print(no_value)
print(type(no_value))  # <class 'NoneType'>
```

### 8. **Type Conversion and Checking**

You can convert between types using built-in functions:

- `int()`: Convert to integer.
- `float()`: Convert to float.
- `str()`: Convert to string.
- `list()`: Convert to list,
- `set()` : Convert to set to remove duplicates etc.

**Example of Conversions:**

```python
num_str = "100"
num_int = int(num_str)  # Convert string to integer
print(num_int, type(num_int))

# Converting a list to a set to remove duplicates
my_list = [1, 2, 2, 3, 4, 4]
unique_items = set(my_list)
print(unique_items)

# Checking type using the type() function:
print(type(3.14))
```

### 9. **Summary Table**

| Data Type | Description | Example |
| --- | --- | --- |
| `int` | Whole numbers | `5`, `-10` |
| `float` | Numbers with a decimal point | `3.14`, `-0.001` |
| `complex` | Numbers with a real and imaginary part | `2 + 3j` |
| `bool` | Boolean values representing True or False | `True`, `False` |
| `str` | Text (sequence of characters) | `"Hello"`, `'Data'` |
| `list` | Ordered, mutable sequence of elements | `[1, 2, "Python"]` |
| `tuple` | Ordered, immutable sequence of elements | `(1, 2, "Immutable")` |
| `range` | Sequence representing an arithmetic progression | `range(5)` |
| `dict` | Collection of key-value pairs | `{"name": "Vybhav", "age": 25}` |
| `set` | Unordered collection of unique elements | `{1, 2, 3}` |
| `frozenset` | Immutable version of a set | `frozenset([1, 2, 3])` |
| `None` | Represents the absence of a value | `None` |

Please practise the structure - braces and all.

### **Practical Tips for Data Analysts**

- **Data Validation:** When working with real-world datasets, you often need to ensure that data conforms to expected types. For example, converting strings to numbers before performing mathematical analyses.
- **Error Handling:** Knowing the data type helps avoid errors. For instance, adding an integer and a string without proper conversion will raise a `TypeError`.
- **Data Manipulation:** Using lists, dictionaries, and sets allows you to clean, organize, and analyze data effectively. For example, dictionaries are great for mapping categorical data to numerical values for analysis.

### **Exercises: Try These in Your Notebook**

1. **Experiment with Type Conversion:**
    - Create a variable with a numeric string (e.g., `"123"`).
    - Convert it to an integer and add another number.
2. **Manipulate a List and a Tuple:**
    - Create a list with a mix of numbers and strings.
    - Attempt to change an element in the list.
    - Create a tuple with the same elements and try modifying it; observe what happens.
3. **Dictionary Operations:**
    - Create a dictionary to map product names to their prices.
    - Write a small piece of code to iterate over the dictionary and print each product's details.
4. **Using Sets to Remove Duplicates:**
    - Create a list with duplicate values.
    - Convert it to a set to see unique values.

---

## Expressions and Variables

### What Is an Expression?

An **expression** in Python is any combination of values, variables, and operators that Python can evaluate to produce a new value. For example, in the expression `3 + 4`, Python computes the result `7`. Expressions can be as simple as a single number or as complex as a calculation involving multiple operators and functions.

### Common Mathematical Operators

Here are the primary arithmetic operators used in Python:

- **Addition (`+`):**
    
    Adds two numbers.
    
    **Example:**
    
    ```python
    3 + 5  # Evaluates to 8
    ```
    
- **Subtraction ():**
    
    Subtracts one number from another.
    
    **Example:**
    
    ```python
    10 - 3  # Evaluates to 7
    ```
    
- **Multiplication ():**
    
    Multiplies two numbers.
    
    **Example:**
    
    ```python
    4 * 2  # Evaluates to 8
    ```
    
- **Division (`/`):**
    
    Divides one number by another and always returns a float.
    
    **Example:**
    
    ```python
    9 / 3  # Evaluates to 3.0
    ```
    
- **Floor Division (`//`):**
    
    Divides and returns the largest whole number (integer) less than or equal to the result.
    
    **Example:**
    
    ```python
    7 // 2  # Evaluates to 3
    ```
    
- **Modulus (`%`):**
    
    Returns the remainder of division.
    
    **Example:**
    
    ```python
    7 % 2  # Evaluates to 1
    ```
    
- **Exponentiation (`*`):**
    
    Raises one number to the power of another.
    
    **Example:**
    
    ```python
    2 ** 3  # Evaluates to 8
    ```
    

### Operator Precedence

Just like in traditional mathematics, Python follows a specific order in evaluating expressions.

The typical order—often remembered by the acronym **PEMDAS** (Parentheses, Exponents, Multiplication/Division, Addition/Subtraction):

1. **Parentheses:** `()`
2. **Exponentiation:** `*`
3. **Multiplication/Division, Floor Division, Modulus:** `, /, //, %`
4. **Addition/Subtraction:** `+, -`

**Example:**

```python
result = 3 + 2 * 4  # Multiplication happens first: 2 * 4 = 8; then addition: 3 + 8 = 11
print(result)  # Outputs: 11
```

**Tip:** Use parentheses to make your intended order explicit:

```python
result = (3 + 2) * 4  # Now addition happens first: 3 + 2 = 5; then multiplication: 5 * 4 = 20
print(result)  # Outputs: 20
```

### Hands-On Exercise with Expressions

1. Open a new cell in Jupyter Notebook or VS Code.
2. Write code to compute the following:
    - **Area of a rectangle:**
        
        ```python
        length = 10
        width = 5
        area = length * width
        print("Area of the rectangle:", area)
        ```
        
    - **Circle's area:**
    Use the formula *πr²*. Python doesn't have a built-in `π`, but you can import it:
        
        ```python
        import math
        radius = 7
        area_circle = math.pi * (radius ** 2)
        print("Area of the circle:", area_circle)
        ```
        

### 2. Variables

### What Are Variables?

A **variable** in Python is a label that refers to a value stored in the computer's memory. Think of it as a container or a box where you store data that you can use later in your code. Variables give you the flexibility to name data and work with it in a readable way.

### Creating and Using Variables

- **Assigning a Value to a Variable**
    
    You don't need to declare the type of a variable beforehand. The assignment happens using the `=` operator.
    
    ```python
    x = 10          # x is assigned the integer value 10
    greeting = "Hello, Data Science!"  # greeting is assigned a string
    ```
    
- **Using Variables in Expressions**
    
    Once a variable has a value, you can use it in any expression.
    
    ```python
    # Performing arithmetic with variables
    a = 5
    b = 3
    sum_ab = a + b
    product_ab = a * b
    print("Sum:", sum_ab)          # Outputs: 8
    print("Product:", product_ab)  # Outputs: 15
    ```
    

### Variable Naming Conventions

To keep your code readable and maintainable:

- Choose **descriptive names** (e.g., `radius`, `temperature`, `total_sales`).
- Use **lowercase letters** and underscores for separation (`snake_case`), such as `student_score`.
- Avoid using Python reserved words like `print`, `if`, or `while`.

### Example: Using Variables in a Simple Program

Let's combine expressions and variables in a small program that calculates the Body Mass Index (BMI):

```python
# BMI = weight (kg) / (height (m))^2

weight = 70  # in kilograms
height = 1.75  # in meters

bmi = weight / (height ** 2)
print("The BMI is:", bmi)
```

This exercise illustrates how variables store data, and expressions (including mathematical operations) compute a new value based on that data.

### Bringing It All Together: Practical Exercises

1. **Temperature Converter: Celsius to Fahrenheit**
    
    Formula: Fahrenheit = (Celsius * 9/5) + 32
    
    **Exercise:**
    
    ```python
    celsius = 25
    fahrenheit = (celsius * 9/5) + 32
    print("Temperature in Fahrenheit:", fahrenheit)
    ```
    
2. **Calculate the Perimeter and Area of a Triangle**
    
    Given base, height, and side lengths, calculate:
    
    - Perimeter: Sum of all sides.
    - Area: (Base * Height) / 2
    
    **Exercise:**
    
    ```python
    base = 8
    height = 5
    side1 = 7
    side2 = 6
    side3 = 8  # Assuming the triangle has sides of these lengths
    
    perimeter = side1 + side2 + side3
    area = (base * height) / 2
    
    print("Perimeter:", perimeter)
    print("Area:", area)
    ```
    
3. **Operator Precedence Challenge**
    
    Write an expression that calculates `result = (10 + 5) * (12 / 3) - 2 ** 3` and predict the output before running it (result = 52.0)
    

---

## String operations

### 1. Creating and Representing Strings

A **string** can be enclosed in single quotes (`'...'`), double quotes (`"..."`), or triple quotes (`'''...'''` or `"""..."""`). Triple quotes allow you to create multi-line strings.

**Example:**

```python
single_quote = 'Hello, Data Science!'
double_quote = "Hello, Data Science!"
multi_line = """This is a multi-line string.
It spans multiple lines gracefully."""
```

### 2. String Concatenation and Repetition

### Concatenation

You can combine (concatenate) strings using the `+` operator.

**Example:**

```python
first_name = "Vybhav"
last_name = "Sharma"
full_name = first_name + " " + last_name  # adds a space between first and last names
print(full_name)  # Output: Vybhav Sharma
```

### Repetition

The `*` operator repeats a string a specified number of times.

**Example:**

```python
repeat_str = "ha" * 3
print(repeat_str)  # Output: hahaha (ha repeated three times)
```

### 3. Indexing and Slicing

### Indexing

Strings are **indexed** starting at 0. You can access any character by its position.

**Example:**

```python
text = "Data Science"
print(text[0])  # 'D'
print(text[5])  # 'S'
```

Negative indexing lets you start from the end:

```python
print(text[-1])  # 'e'
print(text[-2])  # 'c'
```

### Slicing

Slicing allows you to extract a substring. The syntax is:

`string[start:stop:step]`

- **`start`**: index to begin (inclusive)
- **`stop`**: index to end (exclusive)
- **`step`**: how many characters to skip

**Examples:**

```python
s = "PythonString"
print(s[0:6])    # 'Python' (characters from index 0 up to, but not including, 6)
print(s[6:])     # 'String' (from index 6 to the end)
print(s[::2])    # Every second character in the string
```

### 4. Common String Methods

Python strings come with many built-in methods. Here are a few that you’ll use often:

### a. Changing Case

- **`upper()`** and **`lower()`**:

```python
sentence = "Data Science is fun!"
print(sentence.upper())  # "DATA SCIENCE IS FUN!"
print(sentence.lower())  # "data science is fun!"
```

- **`capitalize()`** makes the first letter uppercase:

```python
print(sentence.capitalize())  # "Data science is fun!"
```

### b. Splitting and Joining

- **`split()`** breaks a string into a list, using a delimiter (default is whitespace):

```python
words = sentence.split()
print(words)  # ['Data', 'Science', 'is', 'fun!']
```

- **`join()`** is the reverse, concatenating list elements into a string:

```python
joined = " ".join(words)
print(joined)  # "Data Science is fun!"
```

### c. Trimming Whitespace

- **`strip()`**, **`lstrip()`**, and **`rstrip()`** remove unwanted whitespace.

```python
messy = "   Clean me up!   "
print(messy.strip())   # "Clean me up!"
print(messy.lstrip())  # "Clean me up!   "
print(messy.rstrip())  # "   Clean me up!"
```

### d. Replacing and Searching

- **`replace(old, new)`** substitutes parts of a string:

```python
text = "I love Python. Python is great!"
new_text = text.replace("Python", "data analysis")
print(new_text)  # "I love data analysis. data analysis is great!"
```

- **`find(sub)`** returns the index of the first occurrence of a substring or `1` if not found:

```python
position = text.find("Python")
print(position)  # Position of the first occurrence of 'Python'
```

### e. Other Useful Methods

- **`count(sub)`**: Count how many times a substring appears.

```python
print(text.count("Python"))  # Count of "Python" in the text
```

- **`startswith(prefix)`** and **`endswith(suffix)`**: Check how a string begins or ends.

```python
print(text.startswith("I love"))  # True
print(text.endswith("great!"))    # True
```

### 5. String Formatting

Formatting strings lets you insert variables into text, making your output dynamic.

### Using f-strings (Python 3.6+)

```python
name = "Vybhav"
course = "Data Analytics"
message = f"Hello, my name is {name} and I'm studying {course}."
print(message)
```

### Using `.format()`

```python
message = "Hello, my name is {} and I'm studying {}.".format(name, course)
print(message)
```

### Old-style (%) formatting

```python
message = "Hello, my name is %s and I'm studying %s." % (name, course)
print(message)
```

### 6. Real-World Relevance for Data Analysts

- **Data Cleaning:**
    
    When handling text data, you'll often need to remove whitespace, standardized casing, or replace parts of strings.
    
- **Parsing Data:**
    
    CSV files and text logs require splitting and trimming operations to transform raw data into a form suitable for analysis.
    
- **Reporting:**
    
    String formatting is essential when dynamically generating reports or dashboards where variables must be incorporated into textual content.
    

### 7. Hands-On Exercise

1. **Customize Your Greeting:**
    - Create a string variable with a greeting message.
    - Use concatenation and f-string formatting to personalize it with your name.
    - Experiment by converting the entire message to uppercase.
    
    **Try:**
    
    ```python
    greeting = "Welcome to the world of Python!"
    name = "Vybhav"
    personalized_greeting = greeting + " My name is " + name + "."
    print(personalized_greeting)
    print(personalized_greeting.upper())
    ```
    
2. **Extracting Information:**
    - Create a string with a sentence that includes your favorite data science tool.
    - Use slicing and the `find()` method to extract just the tool's name.
    
    **Try:**
    
    ```python
    sentence = "I frequently use Jupyter Notebook for interactive coding."
    # Let's assume you want to extract "Jupyter Notebook"
    start = sentence.find("Jupyter")
    end = sentence.find("for", start)
    tool = sentence[start:end].strip()  # .strip() removes unwanted spaces
    
    print("Tool found:", tool)
    ```
    
3. **Splitting and Rejoining:**
    1. Create a comma-separated string (e.g., "Python,SQL,Excel") and convert it into a list.
    2. Then modify one of the items and join them back into a comma-separated string.

```
```python
tools = "Python,SQL,Excel"
tool_list = tools.split(",")
# Replace 'Excel' with 'Power BI'
tool_list[-1] = "Power BI"
updated_tools = ", ".join(tool_list)
print("Updated Tools:", updated_tools)
```

---