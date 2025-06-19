# IBM_c4_m2

## Lists and Tuples

### 1. Lists

### What Is a List?

A **list** is an **ordered** collection of items that is **mutable** (i.e., you can change, add, or remove elements after its creation). Lists can contain items of varying data types (numbers, strings, other lists, etc.), making them a versatile structure for storing and processing data.

### Creating a List

You create a list by placing elements inside square brackets `[ ]`, separated by commas.

**Example:**

```python
# A list of numbers
numbers = [10, 20, 30, 40]

# A list of strings
fruits = ["apple", "banana", "cherry"]

# A mixed list
mixed_list = [1, "Python", 3.14, True]
```

### Accessing Elements

Lists are **indexed** starting at 0, meaning the first element has index 0.

**Examples:**

```python
print(numbers[0])       # Outputs: 10
print(fruits[1])        # Outputs: banana
print(mixed_list[-1])   # Negative index accesses from the end (Outputs: True)
```

### Slicing a List

Slicing allows you to retrieve a subset of a list by specifying a start and stop index.

**Example:**

```python
# Given the list below:
colors = ["red", "green", "blue", "yellow", "purple"]

# Retrieve a sublist from green to yellow (inclusive start, exclusive stop):
sub_colors = colors[1:4]
print(sub_colors)  # Outputs: ['green', 'blue', 'yellow']

```

### Modifying Lists

Since lists are mutable, you can change elements, add new items, or remove items after creation.

### Changing an Element

```python
fruits[0] = "avocado"
print(fruits)  # Now fruits becomes ['avocado', 'banana', 'cherry']
```

### Adding Elements

- **`append()`** — Adds an element to the end of the list:
    
    ```python
    fruits.append("date")
    print(fruits)  # Outputs: ['avocado', 'banana', 'cherry', 'date']
    ```
    
- **`insert()`** — Inserts an element at a specific index:
    
    ```python
    fruits.insert(1, "blueberry")
    print(fruits)  # Now fruits includes 'blueberry' at index 1
    ```
    

### Removing Elements

- **`remove()`** — Removes the first occurrence of a value:
    
    ```python
    fruits.remove("banana")
    print(fruits)  # 'banana' is removed
    ```
    
- **`pop()`** — Removes and returns the element at a specific index (default is the last element):
    
    ```python
    last_item = fruits.pop()
    print(last_item)  # The popped element
    print(fruits)     # List after removal
    ```
    
- **`clear()`** — Removes all items from the list:
    
    ```python
    fruits.clear()
    print(fruits)  # Outputs: []
    ```
    

### Iterating Through a List

You can loop through each element of the list using a `for` loop:

```python
for color in colors:
    print(color)
```

### Other Useful List Methods

- **`extend()`** — Combines two lists:
    
    ```python
    more_colors = ["orange", "pink"]
    colors.extend(more_colors)
    print(colors)
    ```
    
- **`sort()`** — Sorts the list in place:
    
    ```python
    numbers = [30, 10, 20, 40]
    numbers.sort()
    print(numbers)  # Outputs: [10, 20, 30, 40]
    ```
    
- **`reverse()`** — Reverses the list in place:
    
    ```python
    numbers.reverse()
    print(numbers)  # Outputs: [40, 30, 20, 10]
    ```
    
- **`len()`** — Returns the number of items in the list:
    
    ```python
    print(len(numbers))  # Outputs: 4
    ```
    

### Hands-On Exercise with Lists

1. **Stock Inventory Example:**
    
    Create a list that stores product names. Then:
    
    - Append a new product.
    - Insert a product at the beginning.
    - Remove a product by name.
    - Loop through the list to print each product.
    
    **Try:**
    
    ```python
    products = ["laptop", "tablet", "smartphone"]
    products.append("smartwatch")
    products.insert(0, "desktop")
    products.remove("tablet")
    for product in products:
        print("Product:", product)
    ```
    
2. **List Slicing and Concatenation:**
    
    Create two lists of numbers and then:
    
    - Slice a portion from each list.
    - Concatenate the slices into a new list.
    
    **Try:**
    
    ```python
    list1 = [1, 2, 3, 4, 5]
    list2 = [6, 7, 8, 9, 10]
    slice1 = list1[1:4]  # [2, 3, 4]
    slice2 = list2[0:3]  # [6, 7, 8]
    combined = slice1 + slice2
    print("Combined List:", combined)
    ```
    

### Copy and clone - Lists

At first glance, copying a list might seem straightforward, but it's essential to understand the difference between simply referencing a list versus creating a new, independent list. This concept is vital when you're modifying data without affecting the original dataset—a common scenario in data analysis.

### **1. Assignment vs. Copying**

Simply assigning a list to a new variable does not create a copy; it only creates a new reference to the same list in memory.

```python
original_list = [1, 2, 3]
new_reference = original_list
new_reference.append(4)

print("Original:", original_list)  # Outputs: [1, 2, 3, 4]
```

Since both names point to the same object, any change affects both.

### **2. Shallow Copy**

A **shallow copy** creates a new list container, but the elements themselves are still references to the objects in the original list. For lists that contain only immutable elements (like numbers or strings), a shallow copy is usually enough.

### **Methods to Create a Shallow Copy:**

### **a. Using Slicing**

```python
original_list = [1, 2, 3]
shallow_copy = original_list[:]  # Slicing creates a shallow copy

shallow_copy.append(4)
print("Original:", original_list)  # [1, 2, 3]
print("Shallow Copy:", shallow_copy)  # [1, 2, 3, 4]
```

### **b. Using the `list()` Constructor**

```python
original_list = [1, 2, 3]
shallow_copy = list(original_list)
```

### **c. Using the `.copy()` Method (Python 3.x)**

```python
original_list = [1, 2, 3]
shallow_copy = original_list.copy()
```

### **d. Using the `copy` Module for a Shallow Copy**

```python
import copy

original_list = [1, 2, 3]
shallow_copy = copy.copy(original_list)
```

> Note: All these methods create a shallow copy. They work well if your list has only simple data types. However, if your list contains nested (mutable) objects like other lists, only the outer list is copied; the inner objects remain shared.
> 

### **3. Deep Copy**

A **deep copy** creates a new list and recursively copies all objects stored within the original list. This is crucial when your list contains mutable objects (such as sublists) and you want complete independence between the original and the copied list.

### **Using the `deepcopy()` Function**

```python
import copy

original_list = [1, 2, [3, 4]]
deep_copy_list = copy.deepcopy(original_list)

# Modify the nested list in the original
original_list[2].append(5)

print("Original:", original_list)       # [1, 2, [3, 4, 5]]
print("Deep Copy:", deep_copy_list)       # [1, 2, [3, 4]]

```

In this example, modifying the inner list of the original does not affect the deep copy.

### **Summary Chart**

| Method | Type of Copy | Example Usage (for a list `L`) |
| --- | --- | --- |
| Assignment (`L2 = L`) | Reference only | Changes in `L2` reflect in `L` |
| Slicing (`L[:]`) | Shallow Copy | `L2 = L[:]` |
| `list(L)` Constructor | Shallow Copy | `L2 = list(L)` |
| `L.copy()` | Shallow Copy | `L2 = L.copy()` |
| `copy.copy(L)` | Shallow Copy | `import copy; L2 = copy.copy(L)` |
| `copy.deepcopy(L)` | Deep Copy | `import copy; L2 = copy.deepcopy(L)` |

### **When Should You Copy a List?**

- **Shallow Copy:**
    
    Use when your list elements are immutable (like numbers, strings) or when you want the nested objects to be shared.
    
- **Deep Copy:**
    
    Use when your list contains nested or mutable objects and you need the copy to be completely independent of the original.
    

### 2. Tuples

### What Is a Tuple?

A **tuple** is also an **ordered** collection of items, but it is **immutable**—once you create it, you cannot modify its contents. Tuples are defined using parentheses `( )`, though you can also create them without explicit parentheses by separating items with commas.

### Creating a Tuple

**Example:**

```python
# A tuple of numbers
dimensions = (1920, 1080)

# A tuple of strings
days = ("Monday", "Tuesday", "Wednesday")

# A mixed tuple (parentheses are optional)
person_info = "Vybhav", 25, "Data Analyst"
```

### Accessing Tuple Elements

Tuples behave like lists in terms of **indexing** and **slicing**.

**Example:**

```python
print(days[0])     # Outputs: 'Monday'
print(dimensions[1])  # Outputs: 1080
print(person_info[-1])  # Outputs: 'Data Analyst'
```

### Tuple Immutability

Once a tuple is created, its elements cannot be modified, added, or removed. This property ensures that the data remains constant, which can be valuable for:

- **Data integrity:** When you need to make sure values should not change.
- **Using as dictionary keys:** Because dictionaries require immutable keys.

**Attempting Modification:**

```python
# This will raise an error:
# days[0] = "Sunday"  # Uncommenting this line will result in a TypeError
```

### Tuple Unpacking

One of the most powerful features of tuples is unpacking, where you can assign tuple values to multiple variables at once.

**Example:**

```python
coordinates = (10, 20)
x, y = coordinates  # Unpack tuple values into variables
print("x =", x)
print("y =", y)
```

### When to Use Tuples Over Lists

- **Use Tuples:**
    - When you have a fixed collection of items.
    - When you need an immutable data structure.
    - When the data is meant to be read-only.
- **Use Lists:**
    - When your collection is expected to change.
    - When you need built-in methods like append, remove, or sort.

### Hands-On Exercise with Tuples

1. **Basic Tuple Operations:**
    - Create a tuple that holds the names of three programming languages.
    - Try to access the second language.
    
    **Try:**
    
    ```python
    languages = ("Python", "JavaScript", "SQL")
    print("The second language is:", languages[1])
    ```
    
2. **Tuple Unpacking:**
    - Create a tuple with your birthdate `(day, month, year)`.
    - Unpack the tuple into three variables and print them.
    
    **Try:**
    
    ```python
    birthdate = (15, "August", 1995)
    day, month, year = birthdate
    print(f"Born on: {day} {month} {year}")
    ```
    

### 3. Comparing Lists and Tuples

| Feature | List | Tuple |
| --- | --- | --- |
| **Mutability** | Mutable (can change elements) | Immutable (cannot change elements) |
| **Syntax** | Square brackets `[ ]` | Parentheses `( )` or comma-separated |
| **Use Cases** | When the data collection can change | When the collection is fixed |
| **Methods** | Many built-in methods (append, etc.) | Fewer methods available (count, index) |
| **Performance** | Slightly slower due to mutability | Generally faster and uses less memory |

---

## Dictionary

### 1. What Is a Dictionary?

A **dictionary** in Python is an *unordered* (prior to Python 3.7) collection of key-value pairs, where each key is unique.

- **Key:** A unique identifier (typically immutable types like strings, numbers, or tuples).
- **Value:** Data associated with that key. Values can be of any type, including other dictionaries.

### Example:

```python
# A simple dictionary representing a person
person = {
    "name": "Vybhav",
    "age": 25,
    "course": "IBM Data Analyst Professional Certificate"
}
```

This dictionary has three key-value pairs and lets you efficiently look up, update, or remove data.

### 2. Creating and Accessing Dictionaries

### Creating a Dictionary

You can create a dictionary using curly braces `{}` with keys and values separated by a colon (`:`), or via the `dict()` constructor.

**Example:**

```python
# Using curly braces
student = {
    "id": 101,
    "name": "Alice",
    "grades": [85, 92, 78]
}

# Using the dict() constructor
employee = dict(name="Bob", role="Data Analyst", salary=75000)
```

### Accessing Elements

Use the key inside square brackets to retrieve its value:

```python
print(student["name"])  # Outputs: Alice
```

Or use the `get()` method, which is safer because it allows you to provide a default value if the key is not found:

```python
print(student.get("age", "Not Available"))  # Outputs: "Not Available" since age is not defined
```

### 3. Modifying Dictionaries

### Adding or Updating Key-Value Pairs

Assign a value to a new or existing key. If the key exists, its value is updated; if not, a new key-value pair is added.

```python
# Adding a new key-value pair
student["major"] = "Data Science"
print(student)

# Updating an existing value
student["grades"].append(95)
print(student)
```

### Removing Items

You can remove a key-value pair with several methods:

- **`del` statement:**
    
    ```python
    del employee["salary"]
    ```
    
- **`pop()` method:** Removes the key and returns its value; you can provide a default to avoid errors if the key is missing.
    
    ```python
    role = employee.pop("role", "No role found")
    print("Removed role:", role)
    ```
    
- **`popitem()` method:** Removes and returns the last inserted key-value pair (useful in Python 3.7+ where dictionaries preserve insertion order).
    
    ```python
    key, value = student.popitem()
    print(f"Removed ({key}: {value})")
    ```
    
- **`clear()` method:** Empties the entire dictionary.
    
    ```python
    student.clear()
    print(student)  # Outputs: {}
    ```
    

### 4. Iterating Over Dictionaries

Loop over keys, values, or key-value pairs as needed:

- **Iterate over keys:**
    
    ```python
    for key in employee:
        print(key)
    ```
    
- **Iterate over values:**
    
    ```python
    for value in employee.values():
        print(value)
    ```
    
- **Iterate over key-value pairs:**
    
    ```python
    for key, value in employee.items():
        print(f"{key}: {value}")
    ```
    

This level of iteration is particularly helpful for examining, filtering, or transforming your data.

### 5. Dictionary Methods and Operations

Dictionaries in Python come with many built-in methods that can greatly simplify your coding tasks:

- **`keys()`:** Returns a view object of the dictionary's keys.
    
    ```python
    print(person.keys())
    ```
    
- **`values()`:** Returns a view object of the dictionary's values.
    
    ```python
    print(person.values())
    ```
    
- **`items()`:** Returns a view object of the dictionary's key-value pairs.
    
    ```python
    print(person.items())
    ```
    
- **`update()`:** Merges one dictionary into another. If keys overlap, the values in the updated dictionary overwrite those in the original.
    
    ```python
    extra_info = {"hobby": "painting", "age": 26}  # This age will override the original
    person.update(extra_info)
    print(person)
    ```
    
- **`copy()`:** Creates a shallow copy of the dictionary.
    
    ```python
    person_copy = person.copy()
    ```
    
- **Membership Test:** Use the `in` keyword to check if a key exists.
    
    ```python
    if "name" in person:
        print("Name is available")
    ```
    

### 6. Nested Dictionaries

Dictionaries can contain other dictionaries, enabling you to represent more complex and hierarchical data structures.

### Example:

```python
students = {
    "student1": {"name": "Alice", "grade": "A"},
    "student2": {"name": "Bob", "grade": "B"},
    "student3": {"name": "Charlie", "grade": "A"}
}

# Accessing nested elements
print(students["student2"]["name"])  # Outputs: Bob
```

Nested dictionaries are commonly used in scenarios such as JSON data parsing, configuration files, or organizing related records.

### 7. Dictionary Comprehensions

Just like list comprehensions, dictionary comprehensions allow you to construct dictionaries in a concise and readable way.

### Example:

```python
# Creating a dictionary of squares for numbers 1 through 5
squares = {num: num ** 2 for num in range(1, 6)}
print(squares)  # Outputs: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

This technique is particularly useful when you need to transform or filter data on the fly.

### 8. Real-World Relevance for Data Analysts

- **Data Mapping:**
    
    Dictionaries are ideal for mapping categorical data to numerical values (e.g., mapping "good", "average", "poor" to 3, 2, 1 respectively).
    
- **Storing Records:**
    
    When dealing with datasets like a CSV file where each row contains multiple attributes, you can represent each row as a dictionary connecting field names to values.
    
- **Configuration Settings:**
    
    Many APIs and programs use dictionaries to store configuration parameters, making them very useful in automation scripts and data pipelines.
    
- **Aggregation and Counting:**
    
    Dictionaries serve as a powerful tool when counting occurrences (e.g., word frequency counts, summarizing results).
    

### 9. Hands-On Exercises

### Exercise 1: Student Record Management

1. Create a dictionary representing a student with keys: `"name"`, `"age"`, and `"courses"` (the latter being a list of course names).
2. Add a new course to the `"courses"` list.
3. Update the student's age.
4. Loop through the dictionary and print each key-value pair.

```python
student = {
    "name": "Vybhav",
    "age": 25,
    "courses": ["Python for Data Science", "Data Visualization"]
}

# Add a new course
student["courses"].append("Machine Learning")

# Update age
student["age"] = 26

# Iterate and print
for key, value in student.items():
    print(f"{key}: {value}")
```

### Exercise 2: Dictionary Comprehension

Construct a dictionary that maps each lowercase letter in a string (without repetition) to its ASCII value.

```python
sample_text = "dataanalysis"
ascii_map = {char: ord(char) for char in set(sample_text)}
print(ascii_map)

```

### Exercise 3: Nested Dictionary

Create a dictionary to store information about multiple employees, where each employee has a unique ID and is associated with another dictionary containing `"name"`, `"department"`, and `"salary"`. Then, print the details of each employee.

```python
employees = {
    "E001": {"name": "Alice", "department": "Finance", "salary": 55000},
    "E002": {"name": "Bob", "department": "IT", "salary": 60000},
    "E003": {"name": "Charlie", "department": "HR", "salary": 50000}
}

for emp_id, details in employees.items():
    print(f"Employee ID: {emp_id}")
    for key, value in details.items():
        print(f"  {key}: {value}")
```

---

## Sets

### 1. What Is a Set?

A **set** is an unordered collection of unique elements. This means:

- **Unordered:** The items in a set do not maintain any particular order. You cannot access or change items by an index.
- **Unique Elements:** Duplicate items are automatically removed, making sets ideal for eliminating duplicates.
- **Mutable:** Standard sets are mutable, so you can add or remove items after creation. However, the elements themselves must be immutable (e.g., numbers, strings, tuples).

### Creating a Set

There are two common ways to create a set:

1. **Using Curly Braces:**
    
    ```python
    fruits = {"apple", "banana", "cherry"}
    ```
    
2. **Using the `set()` Constructor:**
    
    ```python
    numbers = set([1, 2, 3, 3, 4])  # Duplicates (the extra 3) are removed automatically
    print(numbers)  # Might print {1, 2, 3, 4} (order may vary)
    ```
    

> Note: An empty set must be created with set(), not with {}, because {} creates an empty dictionary.
> 

### 2. Basic Set Operations

Sets support many mathematical operations, similar to set theory in mathematics. These include:

### Membership Testing

Check if an element is in a set using the `in` keyword:

```python
colors = {"red", "green", "blue"}
print("green" in colors)  # Outputs: True
```

### Adding and Removing Elements

- **Adding an Element:**
    
    ```python
    colors.add("yellow")  # Adds 'yellow' to the set
    ```
    
- **Updating with Multiple Elements:**
    
    ```python
    colors.update(["cyan", "magenta"])
    # Note: update() works with any iterable.
    ```
    
- **Removing an Element:**
    - Using `remove()`:
        
        ```python
        colors.remove("green")  # Raises KeyError if the element does not exist.
        ```
        
    - Using `discard()`:
        
        ```python
        colors.discard("purple")  # Does nothing if the element is not in the set.
        ```
        
    - Using `pop()`:
        
        ```python
        popped_element = colors.pop()  # Removes and returns an arbitrary element
        print("Popped:", popped_element)
        ```
        
- **Clearing a Set:**
    
    ```python
    colors.clear()  # Empties the set
    ```
    

### 3. Mathematical Set Operations

Sets allow you to perform common mathematical operations:

### Union

Returns a set containing all elements from both sets.

```python
set_a = {1, 2, 3}
set_b = {3, 4, 5}
union_result = set_a | set_b  # Output: {1, 2, 3, 4, 5}
# Alternatively:
union_result = set_a.union(set_b)
```

### Intersection

Returns a set with elements common to both sets.

```python
intersection_result = set_a & set_b  # Output: {3}
# Alternatively:
intersection_result = set_a.intersection(set_b)
```

### Difference

Returns a set with elements in one set but not in the other.

```python
difference_result = set_a - set_b  # Output: {1, 2}
# Alternatively:
difference_result = set_a.difference(set_b)
```

### Symmetric Difference

Returns a set with elements in either set, but not in both.

```python
sym_diff_result = set_a ^ set_b  # Output: {1, 2, 4, 5}
# Alternatively:
sym_diff_result = set_a.symmetric_difference(set_b)
```

### 4. Set Comprehensions

Set comprehensions allow you to create a set in a single, concise line, similar to list comprehensions.

```python
# Create a set of squares for numbers 0 through 4:
squares = {x ** 2 for x in range(5)}
print(squares)  # Might output: {0, 1, 4, 9, 16}
```

### 5. Frozen Sets

A **frozenset** is an immutable version of a set. Once created, you cannot add or remove items. This is useful when you require a set that you can use as a key in another dictionary or need to ensure the data doesn't change.

```python
immutable_set = frozenset([1, 2, 3, 2])
print(immutable_set)  # Outputs: frozenset({1, 2, 3})
# Because it's immutable, operations like add or remove are not allowed:
# immutable_set.add(4)  # This will raise an AttributeError.
```

### 6. Practical Use Cases for Sets

- **Eliminating Duplicates:**
    
    When processing data, you might need to remove duplicate entries. Converting a list to a set is a quick way to do that.
    
    ```python
    data = [1, 2, 2, 3, 4, 4, 4, 5]
    unique_data = set(data)
    print(unique_data)  # Outputs: {1, 2, 3, 4, 5}
    ```
    
- **Membership Testing:**
    
    Sets offer very fast membership tests compared to lists, which is crucial when checking for membership in large datasets.
    
- **Mathematical Operations:**
    
    Their natural support for unions, intersections, and differences makes sets ideal for tasks such as combining tags, finding common items between datasets, or filtering out unwanted elements.
    

### 7. Hands-On Exercises

1. **Removing Duplicates:**
    
    Write a program that takes a list with duplicate values and prints a list of unique values.
    
    ```python
    numbers = [3, 5, 3, 1, 2, 5, 3, 1]
    unique_numbers = list(set(numbers))
    print("Unique numbers:", unique_numbers)
    ```
    
2. **Set Operations:**
    
    Create two sets of integers and then use union, intersection, difference, and symmetric difference methods to produce the corresponding results.
    
    ```python
    set1 = {1, 2, 3, 4}
    set2 = {3, 4, 5, 6}
    print("Union:", set1.union(set2))
    print("Intersection:", set1.intersection(set2))
    print("Difference (set1 - set2):", set1.difference(set2))
    print("Symmetric Difference:", set1.symmetric_difference(set2))
    ```
    
3. **Set Comprehension:**
    
    Build a set of all even numbers between 1 and 20 using set comprehension.
    
    ```python
    even_numbers = {num for num in range(1, 21) if num % 2 == 0}
    print("Even numbers:", even_numbers)
    ```
    

---