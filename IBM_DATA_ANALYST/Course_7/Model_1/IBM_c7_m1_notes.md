# IBM_c7_m1

## Data and datasets

### 1. What is Data?

Data is essentially raw information—facts, numbers, or observations—that are collected from various sources. Think of data as individual pieces of a puzzle. It can be simple numbers, text, images, or even timestamps. Data comes in many forms:

- **Numerical Data:** Measurements like age, salary, or temperature.
- **Categorical Data:** Names, labels, or classifications such as gender, or types of fruits.

*Why is it important?*

Data is the raw material that, when processed and analyzed, can reveal patterns, trends, and insights. For instance, understanding numerical sales data over time could help a business predict future trends and make informed decisions.

### 2. What is a Dataset?

A **dataset** is a structured collection of data. Imagine assembling all the puzzle pieces into a box that’s perfectly organized so you can easily see the complete picture. Here are key elements of a dataset:

- **Rows (Observations):** Each row typically represents a single observation or record. For example, in a dataset of students, each row could represent a single student.
- **Columns (Features/Variables):** Each column represents a particular feature or attribute about the observations. In our student example, columns could be “Name,” “Age,” “Grade,” etc.
- **Metadata:** This is information about the data—data about data. It might include a data dictionary that explains what each column is, its data type (number, text, date), its units, and any special characteristics (like if missing values have a particular meaning).

*Why is this structured approach important?*

Structure helps you understand and manipulate data efficiently. In data analysis, knowing how your data is organized lets you decide which tools and techniques to use. For example, if a column represents dates, you might know to convert it into a date format in Python to perform time series analysis.

### 3. Data Types and Their Impact on Analysis

When you dig deeper into a dataset, you’ll find that each column can have different data types. Here’s why this matters:

- **Numerical Types:** Decide what kind of mathematical operations you can perform. For example, averaging a column of numbers.
- **Categorical Types:** They often represent groups or classes which might need encoding or special handling when modeling.
- **Boolean Types:** Indicate true/false values which are useful for filtering or conditional operations.

Understanding these differences helps avoid pitfalls—like trying to calculate the mean of text data—and ensures accuracy in your analysis.

### 4. Why Understanding Data and Datasets is Crucial

**Real-World Decision Making:**

Before diving into any analysis, it’s vital to know what data you’re working with. For instance, an error in understanding what a column represents—such as mixing up “revenue” with “profit”—can lead to incorrect analyses and poor business decisions.

**Efficient Data Cleaning:**

Understanding the dataset's structure helps you design your data cleaning strategy better. Recognize which columns might need type conversion, which might have missing values, or which might require normalization.

**Model Building and Interpretation:**

For any predictive modeling or machine learning task, grasping the nuances of your data—such as numerical scales and categorical distributions—plays a huge role. It influences which models are best suited and how you can interpret the results.

---

## Python packages for DS

### 1. What Are Python Packages?

In Python, **packages** are collections of modules—code files that group together functions, classes, and variables to perform specific tasks. When you use a package, you’re simply reusing someone else’s well-tested tools to solve problems faster. For example, if you need to manage data or create plots, rather than writing everything from scratch, you use these packages to handle the heavy lifting.

### 2. Key Python Packages for Data Science

### **a. NumPy**

- **Purpose:**
    
    NumPy (Numerical Python) provides support for large, multi-dimensional arrays and matrices. It also includes functions for performing high-level mathematical operations on these arrays.
    
- **Why It Matters:**
    
    Many data science libraries, even pandas, build on NumPy arrays for efficient computation. When working with numeric data such as timings or measurements, NumPy ensures operations are fast and memory-efficient.
    
- **Example Use Case:**
    
    Compute the statistical mean or standard deviation of data quickly or perform vectorized operations for large datasets.
    
- **Simple Exercise:**
    
    Open a Jupyter Notebook or VS Code and try:
    
    ```python
    import numpy as np
    
    # Create a numpy array
    data = np.array([1, 2, 3, 4, 5])
    print("Mean:", np.mean(data))
    print("Standard Deviation:", np.std(data))
    ```
    

### **b. Pandas**

- **Purpose:**
    
    Pandas is the go-to library for data manipulation and analysis. It provides the `DataFrame` structure, which allows you to work with tabular data (think of spreadsheets or SQL tables) with rows and columns.
    
- **Why It Matters:**
    
    Most real-world data comes in messy formats (CSV, Excel files, JSON, etc.). Pandas helps clean, transform, and explore this data quickly. It’s essential for preparing data before you can visualize or analyze it further.
    
- **Example Use Case:**
    
    Load a CSV file, inspect the first few rows, find missing values, and summarize the dataset.
    
- **Simple Exercise:**
    
    ```python
    import pandas as pd
    
    # Load a sample CSV file (replace with actual file path or URL)
    df = pd.read_csv('path/to/your/dataset.csv')
    
    # Display a snapshot of the data
    print(df.head())
    
    # Get information about data types and missing values
    print(df.info())
    
    # Get summary statistics for numerical columns
    print(df.describe())
    ```
    

### **c. Matplotlib**

- **Purpose:**
    
    Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python.
    
- **Why It Matters:**
    
    Visualizations turn numbers into stories. Whether it's a line chart for trends over time or a histogram for distributions, Matplotlib helps you see and communicate patterns clearly.
    
- **Example Use Case:**
    
    Visualize a dataset’s distribution or plot a trend line from time series data.
    
- **Simple Exercise:**
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    
    # Generate some data
    x = np.linspace(0, 10, 100)
    y = np.sin(x)
    
    # Create a simple line plot
    plt.plot(x, y)
    plt.title("Sine Wave")
    plt.xlabel("X-axis")
    plt.ylabel("Y-axis")
    plt.show()
    ```
    

### **d. Seaborn**

- **Purpose:**
    
    Seaborn is built on top of Matplotlib and provides a higher-level interface for creating attractive and informative statistical graphics.
    
- **Why It Matters:**
    
    For a data analyst, visual appeal and easy interpretation are crucial. Seaborn’s default themes and more complex plot types (like violin plots or heatmaps) allow you to dive into data relationships quickly.
    
- **Example Use Case:**
    
    Create a heatmap to see correlations between different features in a dataset.
    
- **Simple Exercise:**
    
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt
    
    # Load example dataset
    df = sns.load_dataset("tips")
    
    # Create a correlation heatmap
    plt.figure(figsize=(8, 6))
    sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
    plt.title("Correlation Heatmap")
    plt.show()
    ```
    

### **e. SciPy**

- **Purpose:**
    
    SciPy builds on NumPy to offer additional modules for optimization, statistics, and more scientific calculations.
    
- **Why It Matters:**
    
    Many data analyses require statistical tests or advanced mathematical computations. SciPy’s tools make tasks like curve fitting or performing T-tests straightforward.
    
- **Example Use Case:**
    
    Conduct a statistical test to understand if there is a significant difference between two groups in your sample.
    
- **Simple Exercise:**
    
    ```python
    from scipy import stats
    
    # Sample data for two groups
    group1 = [12, 15, 14, 10, 13]
    group2 = [22, 25, 21, 20, 23]
    
    # Perform a t-test to see if the means are different
    t_stat, p_value = stats.ttest_ind(group1, group2)
    print("T-statistic:", t_stat)
    print("P-value:", p_value)
    ```
    

### **f. Scikit-Learn**

- **Purpose:**
    
    Scikit-Learn (sklearn) is a powerhouse for machine learning in Python, providing algorithms for classification, regression, clustering, and more.
    
- **Why It Matters:**
    
    While data preparation and visualization are critical, predictive modeling forms the backbone of many data-driven decisions. Scikit-Learn offers a consistent API to experiment with various models and evaluate their performance.
    
- **Example Use Case:**
    
    Build a simple linear regression model to predict house prices based on features like area, number of rooms, etc.
    
- **Simple Exercise:**
    
    ```python
    from sklearn.linear_model import LinearRegression
    import numpy as np
    
    # Sample data for linear regression
    X = np.array([[1], [2], [3], [4], [5]])
    y = np.array([2, 4, 5, 4, 5])
    
    # Build and fit the model
    model = LinearRegression()
    model.fit(X, y)
    
    # Make a prediction
    prediction = model.predict([[6]])
    print("Prediction for input 6:", prediction)
    ```
    

### 3. Why These Packages Are Crucial in Data Analytics

Every package has its role in the data science workflow:

- **Efficiency:** They allow you to rapidly manipulate and analyze data without reinventing the wheel.
- **Interoperability:** These libraries are designed to work well together. A NumPy array can be easily converted to a pandas DataFrame, and data visualizations created in Seaborn can complement your Matplotlib plots.
- **Real-World Impact:** In your daily work, whether cleaning up a messy dataset or building a predictive model, these packages are the tools that empower you to drive data-based decisions in business, healthcare, finance, and beyond.

---

## Importing and exporting data in python

### 1. Importing Data

### **a. Using Pandas to Import Data**

**CSV Files:**

CSV (Comma-Separated Values) is one of the most common file formats for storing tabular data. Pandas' `read_csv()` function makes it incredibly easy to bring this data into a DataFrame, which is the go-to data structure in Python for tabular data.

**Example:**

```python
import pandas as pd

# Load data from a CSV file; replace the path with your file's location.
df = pd.read_csv('data/sample_data.csv')

# Display the first few rows of the dataset.
print(df.head())
```

Here, `df.head()` is an excellent tool to quickly peek at your data and understand its structure—helping you check for consistency, missing values, or surprises in data types.

**JSON Files:**

Often, data might be provided in JSON (JavaScript Object Notation) format, which is a popular format for web APIs and configuration files.

**Example:**

```python
# Load data from a JSON file.
df_json = pd.read_json('data/sample_data.json')

# Take a look at the JSON data converted into a DataFrame.
print(df_json.head())
```

JSON structures can range from simple to nested. When working with nested JSON, you might need additional steps to flatten the data.

**Excel Files:**

Excel files are widely used in business and research. Pandas provides the `read_excel()` function, which is very handy—just note that you might need to install an engine like `openpyxl` or `xlrd` depending on your Excel file type.

**Example:**

```python
# Load data from an Excel file.
df_excel = pd.read_excel('data/sample_data.xlsx', sheet_name='Sheet1')

# Preview the data
print(df_excel.head())
```

By specifying the `sheet_name`, you ensure you’re bringing in the correct part of the workbook.

### 2. Exporting Data

Once you've analyzed or transformed your data, you often need to share it, save your work, or load it into another system. Exporting data in Python is just as straightforward.

### **a. Exporting with Pandas**

**Exporting to CSV:**

```python
# Export the DataFrame to a new CSV file.
df.to_csv('data/modified_data.csv', index=False)
```

Setting `index=False` prevents Pandas from writing the row indices (which are often not needed) to the file.

**Exporting to JSON:**

```python
# Export the DataFrame to a JSON file.
df.to_json('data/modified_data.json', orient='records', lines=True)
```

Using parameters like `orient='records'` helps control the JSON structure, making it easier to read or integrate with other systems.

**Exporting to Excel:**

```python
# Export the DataFrame to an Excel file.
df.to_excel('data/modified_data.xlsx', index=False, sheet_name='CleanedData')
```

You can specify the sheet name, making it easier to organize multiple outputs in one workbook.

### 3. Why Importing and Exporting Data Is Crucial

**Real-World Flexibility:**

Data in the real world rarely comes pre-packaged in the format you need. Being adept at importing multiple data types means you can seamlessly integrate from various sources like public datasets, internal business systems, or APIs.

**Efficiency in Data Preparation:**

Understanding how to efficiently load and save data reduces downtime. You can rapidly prototype your analysis, test various transformations, and store clean datasets for production use.

**Interoperability:**

Being able to export data ensures that your analyses can be shared with non-technical stakeholders, integrated into data pipelines, or even fed into another model or visualization tool.

---

## Analysing data in python

Let's dive into getting started with data analysis in Python using **SalesDataset**. 

This dataset features columns like:

- **Order_Id**
- **Amount**
- **Profit**
- **Quantity**
- **Category**
- **Sub-category**
- **PaymentMode**
- **Order_date**
- **CustomerName**
- **State**
- **City**
- **Year-Month**

### 1. Importing Your Data

Before any analysis, you need to bring your data into Python. With the help of the **pandas** library, you can easily load, inspect, and manipulate your dataset.

**Exercise:**

Create a file called `SalesDataset.csv` containing your data (or use an existing file) and run:

```python
import pandas as pd

# Load the SalesDataset CSV file.
sales_df = pd.read_csv('SalesDataset.csv')

# Quick look at the first five rows.
print(sales_df.head())
```

This command loads your dataset into a DataFrame and shows you the first few records, giving you an initial feel for how the data is structured.

### 2. Inspecting and Exploring Your Data

Once the data is loaded, you'll want to understand its structure and content. This stage is called **Exploratory Data Analysis (EDA)**. Key tasks include:

### a. Checking Data Types and Missing Values

**Why?**

Knowing the data types (e.g., numeric, string, datetime) guides how you process each column. You also want to identify any missing values that might affect your analysis.

**Exercise:**

```python
# Check data types and non-null counts.
print(sales_df.info())

# Find out how many missing values each column has.
print(sales_df.isnull().sum())
```

### b. Summary Statistics

**Why?**

Descriptive statistics give you a quantitative overview of your numerical columns. For example, you can quickly see the average Amount or the distribution of Profit.

**Exercise:**

```python
# Get summary statistics for numeric columns.
print(sales_df.describe())

# Optionally, explore statistics specific to columns.
print("Total Orders:", sales_df['Order_Id'].count())
print("Total Revenue (Amount):", sales_df['Amount'].sum())
```

### 3. Data Cleaning and Preparation

Real-world data can be messy. It’s common to clean or transform data before diving deeper.

### a. Converting Columns to Appropriate Types

For example, if **Order_date** or **Year-Month** is stored as a string, you might convert it to a datetime type for time series analysis:

```python
# Convert Order_date to datetime format.
sales_df['Order_date'] = pd.to_datetime(sales_df['Order_date'])

# If Year-Month is in a format like '2020-01', convert it.
sales_df['Year-Month'] = pd.to_datetime(sales_df['Year-Month'], format='%Y-%m')
```

### b. Handling Missing Values

If you discover missing values, you could decide to fill or remove them:

```python
# Fill missing Profit values with 0 (as an example).
sales_df['Profit'].fillna(0, inplace=True)
```

### 4. Data Analysis: Gaining Insights

Now that your data is clean and well-prepared, you can start the actual analysis.

### a. Analyzing Sales by Category

**Objective:** Understand total sales per category to see which product lines perform best.

```python
# Group by Category and calculate total sales (Amount) per group.
category_sales = sales_df.groupby('Category')['Amount'].sum().reset_index()
print(category_sales)
```

### b. Trend Analysis Over Time

**Objective:** Check how sales change over different months.

```python
# Group by Year-Month and calculate total sales.
time_sales = sales_df.groupby('Year-Month')['Amount'].sum().reset_index()
print(time_sales)
```

### c. Profit Margin Calculation

**Objective:** Determine the profitability of each order or category by calculating a profit margin.

```python
# Create a new column for Profit Margin.
sales_df['Profit_Margin'] = sales_df['Profit'] / sales_df['Amount']

# See a sample of orders with the new calculation.
print(sales_df[['Order_Id', 'Amount', 'Profit', 'Profit_Margin']].head())
```

### 5. Visualizing Your Data

Visualization helps bring your analysis to life and makes it easier to spot patterns or outliers.

### a. Plotting Sales by Category

**Exercise:** Use **Matplotlib** to visualize which categories are leading in sales.

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
plt.bar(category_sales['Category'], category_sales['Amount'], color='skyblue')
plt.title('Total Sales by Category')
plt.xlabel('Category')
plt.ylabel('Total Amount')
plt.xticks(rotation=45)
plt.show()
```

### b. Sales Trend over Time

**Exercise:** Plot sales over time to observe seasonal patterns or trends.

```python
plt.figure(figsize=(10, 6))
plt.plot(time_sales['Year-Month'], time_sales['Amount'], marker='o')
plt.title('Sales Trend Over Time')
plt.xlabel('Year-Month')
plt.ylabel('Total Sales Amount')
plt.xticks(rotation=45)
plt.grid(True)
plt.show()
```

### 6. Why This Approach Is Key in Data Analysis

Understanding and analyzing your data is the cornerstone of data-driven decision making:

- **Informed Business Decisions:** You pinpoint which categories drive revenue or identify declining trends in sales.
- **Data Cleaning:** Performing exploratory analysis early helps you avoid pitfalls like missing values or incorrect data types.
- **Actionable Insights:** From calculating profit margins to visualizing trends, every step builds towards a comprehensive view of your business' performance.

---

## Accessing Databases with python

### 1. Using the Built-in `sqlite3` Library

Python comes with a built-in module called `sqlite3` that lets you interact with SQLite databases. SQLite databases are file-based and are perfect for learning or small-to-medium-sized datasets.

### **a. Connecting and Creating a Table**

Let's start by creating a simple database (or connecting to it if it already exists) and ensuring that a table named `SalesDataset` (with the columns you mentioned) exists.

```python
import sqlite3

# Connect to a new (or existing) SQLite database file
conn = sqlite3.connect('sales_data.db')
cursor = conn.cursor()

# Create the SalesDataset table if it doesn't exist
cursor.execute('''
CREATE TABLE IF NOT EXISTS SalesDataset (
    Order_Id INTEGER PRIMARY KEY,
    Amount REAL,
    Profit REAL,
    Quantity INTEGER,
    Category TEXT,
    Sub_category TEXT,
    PaymentMode TEXT,
    Order_date TEXT,
    CustomerName TEXT,
    State TEXT,
    City TEXT,
    Year_Month TEXT
)
''')

conn.commit()  # Save (commit) the changes
```

### **b. Inserting and Querying Data**

Once the table is set up, you can insert records into it or query existing data. For demonstration, here’s how you might insert a sample record and then fetch data:

```python
# Inserting a sample record into SalesDataset
cursor.execute('''
INSERT INTO SalesDataset (Order_Id, Amount, Profit, Quantity, Category, Sub_category,
    PaymentMode, Order_date, CustomerName, State, City, Year_Month)
VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
''', (1, 1500.0, 300.0, 5, 'Electronics', 'Mobile', 'Credit Card',
      '2025-06-18', 'John Doe', 'Karnataka', 'Bengaluru', '2025-06'))

conn.commit()

# Querying all records from SalesDataset
cursor.execute('SELECT * FROM SalesDataset')
rows = cursor.fetchall()

for row in rows:
    print(row)

# Don't forget to close the connection after your operations
cursor.close()
conn.close()
```

This snippet shows you how to:

- **Insert Data**: Using parameterized queries to add a new record safely.
- **Query Data**: Executing a SELECT query to retrieve records and iterating over the results.

### 2. Using SQLAlchemy for More Advanced Database Access

As you grow more confident, you might prefer using **SQLAlchemy**, a powerful Object Relational Mapper (ORM) that offers a more Pythonic way to work with databases. SQLAlchemy allows you to write database queries in Python code and easily integrate with pandas to load data for analysis.

### **a. Setting Up SQLAlchemy**

First, install SQLAlchemy (if you haven't yet):

```bash
pip install sqlalchemy
```

### **b. Connecting to the Database and Fetching Data with Pandas**

Here’s how you can connect to the same SQLite database and fetch the `SalesDataset` table into a pandas DataFrame:

```python
from sqlalchemy import create_engine
import pandas as pd

# Create an engine that connects to the SQLite database
engine = create_engine('sqlite:///sales_data.db')

# Reading the SalesDataset table into a pandas DataFrame
sales_df = pd.read_sql('SELECT * FROM SalesDataset', engine)
print(sales_df.head())
```

With SQLAlchemy, you can:

- **Leverage ORM Techniques:** Define models for your tables and interact with your database using Python classes.
- **Seamlessly Integrate with Pandas:** Directly load query results into a DataFrame, which is ideal for further data cleaning, analysis, or visualization.

---

## Diving deeper - database connection

### 1. The Python DB API (PEP 249)

The Python DB API is a standardized specification (defined in [PEP 249](https://www.python.org/dev/peps/pep-0249/)) that outlines how Python modules should communicate with relational databases. It offers a consistent interface, which means whether you're using `sqlite3`, `psycopg2` for PostgreSQL, or any other compliant library, the workflow is very similar.

**Key Takeaways from the DB API:**

- **Uniformity:** Most database modules implement the same set of methods and exceptions. This makes it easier for you to switch backend databases without rewriting all your code.
- **Core Concepts:** The main components you’ll work with are **connection objects** and **cursor objects**.

### 2. The Connection Object

### What Is a Connection Object?

A connection object represents the ongoing session with your database. When you "connect" to a database, you're opening a channel through which your program can execute SQL commands. This object provides methods that manage your session.

### Key Methods:

- **`connect()`**: This function (provided by your database module, for example, `sqlite3.connect()`) establishes a connection.
- **`commit()`**: When you perform insertions, updates, or deletions, the changes are kept in a transaction until you commit them. The `commit()` method finalizes those changes.
- **`rollback()`**: If something goes wrong during a transaction, you can revert all the changes made in the current transaction using `rollback()`.
- **`close()`**: Always close your connection when you're done to free resources.

### Example with SQLite:

```python
import sqlite3

# Connect to (or create) a database file named 'sales_data.db'
conn = sqlite3.connect('sales_data.db')

# Always check that you're getting a valid connection by exploring its properties:
print("Database opened successfully!")
```

In this example, `conn` is your connection object. It’s your gateway for any operations, including creating tables, inserting data, and querying.

### 3. The Cursor Object

### What Is a Cursor Object?

Once you have an active connection to the database, you need a way to interact with it. Enter the **cursor object**. Think of the cursor as a vehicle that travels over your query results. It's created from the connection and gives you the methods you need to execute SQL commands and fetch data.

### Key Methods:

- **`cursor()`**: Called on a connection object, it returns a new cursor.
- **`execute(sql, [parameters])`**: Executes an SQL command (optionally with parameters to prevent SQL injection).
- **`executemany(sql, seq_of_parameters)`**: Executes the same SQL command for a list of parameter tuples.
- **`fetchone()`**: Returns the next row from the query result.
- **`fetchall()`**: Returns all rows from the query result.
- **`close()`**: Closes the cursor (always a good practice once you are done with it).

### Example with SalesDataset Table:

Imagine you have the `SalesDataset` table with columns like **Order_Id, Amount, Profit, ...**. After opening the connection, here’s how you can work with a cursor to insert and retrieve data:

```python
import sqlite3

# Connect to the database
conn = sqlite3.connect('sales_data.db')
cursor = conn.cursor()

# Create the SalesDataset table if it doesn't exist
cursor.execute('''
CREATE TABLE IF NOT EXISTS SalesDataset (
    Order_Id INTEGER PRIMARY KEY,
    Amount REAL,
    Profit REAL,
    Quantity INTEGER,
    Category TEXT,
    Sub_category TEXT,
    PaymentMode TEXT,
    Order_date TEXT,
    CustomerName TEXT,
    State TEXT,
    City TEXT,
    Year_Month TEXT
)
''')
conn.commit()

# Inserting a sample record using parameterized query
sample_data = (
    1,          # Order_Id
    1500.0,     # Amount
    300.0,      # Profit
    5,          # Quantity
    'Electronics',  # Category
    'Mobile',       # Sub_category
    'Credit Card',  # PaymentMode
    '2025-06-18',   # Order_date
    'John Doe',     # CustomerName
    'Karnataka',    # State
    'Bengaluru',    # City
    '2025-06'       # Year_Month
)
cursor.execute('''
INSERT INTO SalesDataset (Order_Id, Amount, Profit, Quantity, Category, Sub_category,
PaymentMode, Order_date, CustomerName, State, City, Year_Month)
VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
''', sample_data)
conn.commit()

# Querying data using the cursor
cursor.execute('SELECT * FROM SalesDataset')
rows = cursor.fetchall()

print("Fetched rows from SalesDataset:")
for row in rows:
    print(row)

# Always close your cursor and connection
cursor.close()
conn.close()
```

### What's Happening Here?

1. **Connection Setup:**
We open a connection to the SQLite database file and then create a cursor from that connection.
2. **Table Creation:**
We ensure the `SalesDataset` table exists with our specified structure.
3. **Parameterized Query:**
Parameters (the placeholders "?" in the SQL statement) prevent SQL injection and ensure that data types are correctly handled.
4. **Fetching Rows:**
We execute a SELECT query, fetch all rows, and then iterate through them to print the results.
5. **Cleanup:**
Closing the cursor and connection is crucial to free up system resources.

### 4. Advanced Cursor Operations and Transaction Management

### Parameterized Queries

When you pass parameters as a tuple (or list) to `execute()`, the DB API takes care of escaping values properly. This is critical for security.

### Batch Operations with `executemany()`

If you need to insert multiple rows efficiently, you can use `executemany()`. For example:

```python
sample_records = [
    (2, 2000.0, 500.0, 8, 'Furniture', 'Chair', 'Debit Card', '2025-06-19', 'Jane Doe', 'Karnataka', 'Mysuru', '2025-06'),
    (3, 3500.0, 650.0, 10, 'Electronics', 'Laptop', 'Credit Card', '2025-06-20', 'Jim Beam', 'Maharashtra', 'Pune', '2025-06')
]

cursor.executemany('''
INSERT INTO SalesDataset (Order_Id, Amount, Profit, Quantity, Category, Sub_category,
PaymentMode, Order_date, CustomerName, State, City, Year_Month)
VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
''', sample_records)
conn.commit()
```

### Transaction Management

Database operations that write data are executed within transactions. Until you call `conn.commit()`, the changes remain temporary. If something goes wrong, you can call `conn.rollback()` to undo those changes. This mechanism ensures the integrity of your data.

```python
try:
    cursor.execute("INSERT INTO SalesDataset (Order_Id, Amount) VALUES (?, ?)", (4, 4000.0))
    # Suppose subsequent operations fail, you can rollback:
    conn.rollback()
except Exception as e:
    print("An error occurred:", e)
else:
    conn.commit()
```

---