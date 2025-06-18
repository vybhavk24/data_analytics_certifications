# IBM_c6_m4

## How to access databases using Python

### 1. The Python DB API 2.0 Standard

Most Python database modules (such as `sqlite3`, `psycopg2` for PostgreSQL, and `mysql.connector` for MySQL) follow the [DB API 2.0 standard](https://www.python.org/dev/peps/pep-0249/). This standard specifies common methods and constructs such as:

- **Connection objects:** To establish and manage a connection with the database.
- **Cursor objects:** To execute SQL queries and fetch results.
- **Transaction management:** Operations like `commit()` and `rollback()`.
- **Parameter substitution:** To prevent SQL injection via parameterized queries (always preferred over string concatenation).

Understanding this common interface makes it easier to switch between different databases with minimal code changes.

### 2. Using Built-in Modules: SQLite and the `sqlite3` Module

SQLite is a self-contained, file-based database system that comes with Python as the built-in `sqlite3` module. It’s ideal for prototyping, testing, or smaller projects.

- You can run these in a Jupyter notebook and see the results.

### a. Connecting to a SQLite Database

```python
import sqlite3

# Connect to a database file. If it doesn't exist, it will be created.
connection = sqlite3.connect('sales_dataset.db')
cursor = connection.cursor()  # Creating a cursor to execute SQL commands

print("Connected to SQLite database!")
```

### b. Creating a Table

```python
create_table_query = '''
CREATE TABLE IF NOT EXISTS SalesDataset (
    Order_Id INTEGER PRIMARY KEY AUTOINCREMENT,
    Amount REAL,
    Profit REAL,
    Quantity INTEGER,
    Category TEXT,
    "Sub-category" TEXT,
    PaymentMode TEXT,
    Order_date TEXT,  -- storing as text for simplicity (or use ISO format strings)
    CustomerName TEXT,
    State TEXT,
    City TEXT,
    "Year-Month" TEXT
);
'''

cursor.execute(create_table_query)
connection.commit()
print("Table created successfully!")
```

### c. Inserting Data

```python
insert_query = '''
INSERT INTO SalesDataset (Amount, Profit, Quantity, Category, "Sub-category", PaymentMode,
                            Order_date, CustomerName, State, City, "Year-Month")
VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
'''
data = (500.00, 50.00, 5, 'Electronics', 'Smartphone', 'Credit Card',
        '2024-04-15', 'Alice Johnson', 'California', 'Los Angeles', '2024-04')

cursor.execute(insert_query, data)
connection.commit()
print("Record inserted successfully!")
```

### d. Querying Data

```python
select_query = 'SELECT * FROM SalesDataset;'
cursor.execute(select_query)
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### e. Closing the Connection

```python
cursor.close()
connection.close()
print("Connection closed.")
```

This complete workflow shows how you can connect, create a table, insert, query, and finally close the connection using SQLite.

### 3. Connecting to Other Relational Databases

Python's ecosystem includes drivers for many other relational databases. Here are a couple of popular ones:

### a. PostgreSQL with `psycopg2`

1. **Installation:**
    
    ```bash
    pip install psycopg2-binary
    ```
    
2. **Example Code:**
    
    ```python
    import psycopg2
    
    try:
        # Connect to PostgreSQL
        conn = psycopg2.connect(
            host="localhost",
            port="5432",
            database="salesdb",
            user="your_username",
            password="your_password"
        )
        cur = conn.cursor()
    
        # Create a sample table
        cur.execute('''
        CREATE TABLE IF NOT EXISTS SalesDataset (
            Order_Id SERIAL PRIMARY KEY,
            Amount NUMERIC,
            Profit NUMERIC,
            Quantity INTEGER,
            Category VARCHAR(50),
            "Sub-category" VARCHAR(50),
            PaymentMode VARCHAR(50),
            Order_date DATE,
            CustomerName VARCHAR(100),
            State VARCHAR(50),
            City VARCHAR(50),
            "Year-Month" VARCHAR(7)
        );
        ''')
        conn.commit()
        print("PostgreSQL table created!")
    
        # Always close your connection and cursor
        cur.close()
        conn.close()
    except Exception as e:
        print("An error occurred:", e)
    ```
    

### b. MySQL with `mysql.connector`

1. **Installation:**
    
    ```bash
    pip install mysql-connector-python
    ```
    
2. **Example Code:**
    
    ```python
    import mysql.connector
    
    conn = mysql.connector.connect(
        host="localhost",
        user="your_username",
        password="your_password",
        database="salesdb"
    )
    cursor = conn.cursor()
    
    cursor.execute('''
    CREATE TABLE IF NOT EXISTS SalesDataset (
        Order_Id INT AUTO_INCREMENT PRIMARY KEY,
        Amount DECIMAL(10,2),
        Profit DECIMAL(10,2),
        Quantity INT,
        Category VARCHAR(50),
        `Sub-category` VARCHAR(50),
        PaymentMode VARCHAR(50),
        Order_date DATE,
        CustomerName VARCHAR(100),
        State VARCHAR(50),
        City VARCHAR(50),
        `Year-Month` VARCHAR(7)
    );
    ''')
    conn.commit()
    print("MySQL table created!")
    
    cursor.close()
    conn.close()
    ```
    

Each database adapter follows the DB API 2.0 standard, so the structure of your code looks similar: open a connection, create a cursor, execute SQL queries, commit changes (if needed), and close the connection.

### 4. Best Practices: Transactions, Error Handling, and Security

- **Parameterized Queries:**
    
    Use placeholders (e.g., `?` for sqlite3 or `%s` for psycopg2/mysql) to safely pass parameters.
    
- **Transactions:**
    
    Use `commit()` to save changes and `rollback()` in case of errors.
    
    ```python
    try:
        cursor.execute(insert_query, data)
        connection.commit()
    except Exception as e:
        connection.rollback()
        print("Error occurred:", e)
    ```
    
- **Context Managers:**
    
    For automatic handling, you can use Python’s `with` statement. For example, with SQLite:
    
    ```python
    import sqlite3
    
    with sqlite3.connect('sales_dataset.db') as connection:
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM SalesDataset;")
        for row in cursor.fetchall():
            print(row)
    # Connection automatically commits and closes.
    ```
    
- **Close Connections:**
    
    Always close your cursor and connection to free resources. When using context managers, this happens automatically.
    
- **Security:**
    
    Avoid constructing SQL queries by string concatenation to prevent SQL injection. Always use parameterized queries.
    

### 5. Using SQLAlchemy

SQLAlchemy is a powerful toolkit that provides an ORM (Object Relational Mapping) and also supports SQL expression language for those who prefer to write raw SQL.

### a. Installation

```bash
pip install sqlalchemy
```

### b. Connecting and Executing Queries (Core Layer)

```python
from sqlalchemy import create_engine, text

# Create an engine for SQLite (you can also create engines for PostgreSQL or MySQL)
engine = create_engine('sqlite:///sales_dataset.db')

with engine.connect() as connection:
    # Example: Creating a table using a raw SQL statement
    connection.execute(text('''
    CREATE TABLE IF NOT EXISTS SalesDataset (
        Order_Id INTEGER PRIMARY KEY AUTOINCREMENT,
        Amount REAL,
        Profit REAL,
        Quantity INTEGER,
        Category TEXT,
        "Sub-category" TEXT,
        PaymentMode TEXT,
        Order_date TEXT,
        CustomerName TEXT,
        State TEXT,
        City TEXT,
        "Year-Month" TEXT
    );
    '''))

    # Inserting data
    connection.execute(text('''
    INSERT INTO SalesDataset (Amount, Profit, Quantity, Category, "Sub-category", PaymentMode,
                                Order_date, CustomerName, State, City, "Year-Month")
    VALUES (:amount, :profit, :quantity, :category, :sub_category, :payment_mode,
            :order_date, :customer_name, :state, :city, :year_month)
    '''), {
        'amount': 750.00,
        'profit': 90.00,
        'quantity': 3,
        'category': 'Electronics',
        'sub_category': 'Laptop',
        'payment_mode': 'Credit Card',
        'order_date': '2024-05-20',
        'customer_name': 'Bob Smith',
        'state': 'Texas',
        'city': 'Austin',
        'year_month': '2024-05'
    })
    connection.commit()
```

### c. Using the ORM

The SQLAlchemy ORM allows you to define your database schema as Python classes.

```python
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, Float, String, Date
from sqlalchemy.orm import sessionmaker

Base = declarative_base()

class SalesDataset(Base):
    __tablename__ = 'SalesDataset'
    Order_Id = Column(Integer, primary_key=True, autoincrement=True)
    Amount = Column(Float)
    Profit = Column(Float)
    Quantity = Column(Integer)
    Category = Column(String)
    Sub_category = Column(String)
    PaymentMode = Column(String)
    Order_date = Column(String)  # Could also use Date
    CustomerName = Column(String)
    State = Column(String)
    City = Column(String)
    Year_Month = Column(String)  # Using underscore instead of dash

# Create engine and session
engine = create_engine('sqlite:///sales_dataset.db')
Base.metadata.create_all(engine)  # Create tables based on the Base classes

Session = sessionmaker(bind=engine)
session = Session()

# Add a record using the ORM
new_order = SalesDataset(
    Amount=1200.00,
    Profit=150.00,
    Quantity=2,
    Category='Furniture',
    Sub_category='Chair',
    PaymentMode='Net Banking',
    Order_date='2024-06-15',
    CustomerName='Alice Green',
    State='Florida',
    City='Miami',
    Year_Month='2024-06'
)
session.add(new_order)
session.commit()

print("Record added using SQLAlchemy ORM!")
session.close()

```

The ORM means you can now work with Python objects directly, making your code more modular and maintainable.

### 6. Integration with Pandas for Data Analysis

Once your data is in a relational database, you can easily load it into Pandas for analysis:

```python
import pandas as pd
import sqlite3

# Connect to the SQLite database
conn = sqlite3.connect('sales_dataset.db')

# Run a query and load the results into a DataFrame
df = pd.read_sql_query("SELECT * FROM SalesDataset", conn)
print(df.head())

conn.close()
```

This is a common workflow for data analysis in Python: store or retrieve data via a database and then apply the rich data manipulation and visualization tools available in Pandas.

---

## Writing code using DB-API

The DB-API (PEP 249) is a standard interface for working with relational databases. Most Python database modules—such as `sqlite3`, `psycopg2` (PostgreSQL), and `mysql.connector` (MySQL)—adhere to its conventions. 

This ensures that once you learn the basic patterns, you can use similar code with different databases with only minor changes.

### 1. Core Concepts of the Python DB-API

- **Connection Object:**
    
    This represents an open connection to the database. You use it to create cursors, manage transactions (with methods like `commit()` and `rollback()`), and eventually close the connection.
    
- **Cursor Object:**
    
    Once connected, you create a cursor to execute SQL commands. A cursor lets you run queries and fetch results.
    
- **Parameterized Queries:**
    
    Always use parameterized queries (placeholders) when inserting user or variable data into SQL commands to prevent SQL injection.
    
    - For SQLite and `mysql.connector`, you would use the `?` placeholder or `%s` (depending on the adapter).
    - For example, SQLite uses `?` which looks like:
        
        ```python
        cursor.execute("INSERT INTO table (column) VALUES (?)", (value,))
        ```
        
- **Transactions:**
    
    Most operations occur in a transaction. Changes are committed with the `commit()` method. In case of error, you can `rollback()` the changes.
    
- **Exception Handling:**
    
    Use try/except blocks to catch any DB API exceptions (such as `sqlite3.DatabaseError`) and ensure you always close your connection.
    
- **Closing Resources:**
    
    Always close your cursor and connection objects in a finally block (or by using context managers) to free up database resources.
    

### 2. A Complete Example Using SQLite and `sqlite3`

Below is a self-contained snippet that demonstrates connecting to a SQLite database, creating a table, inserting data using parameterized queries, querying the data, and finally closing the connection.

```python
import sqlite3

def main():
    # Use a try/except/finally pattern to catch errors and ensure resources are closed.
    connection = None
    try:
        # Establish a connection to the SQLite database file (it will be created if it doesn't exist)
        connection = sqlite3.connect('sales_dataset.db')
        cursor = connection.cursor()
        print("Connected to the database.")

        # Create a table using a SQL statement
        create_table_sql = '''
        CREATE TABLE IF NOT EXISTS SalesDataset (
            Order_Id INTEGER PRIMARY KEY AUTOINCREMENT,
            Amount REAL,
            Profit REAL,
            Quantity INTEGER,
            Category TEXT,
            "Sub-category" TEXT,
            PaymentMode TEXT,
            Order_date TEXT, -- Can also use DATE or DATETIME if supported
            CustomerName TEXT,
            State TEXT,
            City TEXT,
            "Year-Month" TEXT
        );
        '''
        cursor.execute(create_table_sql)
        connection.commit()
        print("Table created successfully.")

        # Insert a record using a parameterized query
        insert_sql = '''
        INSERT INTO SalesDataset (Amount, Profit, Quantity, Category, "Sub-category", PaymentMode,
                                    Order_date, CustomerName, State, City, "Year-Month")
        VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
        '''
        data = (750.00, 90.00, 3, 'Electronics', 'Laptop', 'Credit Card',
                '2024-05-20', 'Bob Smith', 'Texas', 'Austin', '2024-05')
        cursor.execute(insert_sql, data)
        connection.commit()
        print("Record inserted successfully.")

        # Execute a SELECT query to fetch records
        select_sql = "SELECT Order_Id, CustomerName, Amount, Order_date FROM SalesDataset;"
        cursor.execute(select_sql)
        rows = cursor.fetchall()

        print("Fetched rows:")
        for row in rows:
            print(row)

    except sqlite3.DatabaseError as e:
        # Rollback any pending transaction if error occurs
        if connection:
            connection.rollback()
        print("Database error occurred:", e)
    except Exception as e:
        print("An unexpected error occurred:", e)
    finally:
        # Always close the connection to release resources
        if connection:
            connection.close()
            print("Database connection closed.")

if __name__ == '__main__':
    main()
```

### Explanation

1. **Establishing the Connection:**
    
    We use `sqlite3.connect('sales_dataset.db')` to connect to the database file. If the file doesn’t exist, it’s created.
    
2. **Creating a TABLE:**
    
    The `CREATE TABLE IF NOT EXISTS` statement makes sure that the table is created only if it isn’t already present.
    
    We call `connection.commit()` after executing the DDL statement.
    
3. **Inserting Data:**
    
    The parameterized query uses question mark placeholders.
    
    Data is passed as a tuple, ensuring the values are safely incorporated and preventing SQL injection.
    
4. **Querying Data:**
    
    We execute a simple SELECT command and fetch all rows using `fetchall()`, then loop through and print each row.
    
5. **Error Handling and Cleanup:**
    
    The try/except/finally pattern ensures that if any error occurs, transactions are rolled back and the connection is always closed at the end in the finally block.
    

### 3. Other Databases and Adapters

The pattern shown above is common to many relational databases:

- **PostgreSQL:** Use `psycopg2.connect()` and `%s` as the placeholder.
- **MySQL:** Use `mysql.connector.connect()` with `%s` or the appropriate placeholder.
- Engines like SQLAlchemy build on top of these adapters if you need an ORM or more advanced query building.

For each, the steps remain similar:

1. Connect to the database.
2. Create a cursor.
3. Execute SQL commands using parameterized queries.
4. Commit transactions.
5. Handle exceptions.
6. Close resources.

---

## Connecting to databases using SQL magic

"SQL Magic" typically refers to the functionality available in Jupyter Notebook (or similar environments) that lets you run SQL queries directly within your notebook cells without having to write separate Python code to connect and query your database. 

One popular tool for this is the **ipython-sql** extension. This integration enables rapid prototyping and interactive data exploration, making it easier to switch between SQL and Python in one document.

### 1. Installing and Enabling SQL Magic

Before you begin, install the ipython-sql package (if you haven’t already):

```bash
pip install ipython-sql
```

Then, load the SQL magic extension in a notebook cell:

```python
%load_ext sql
```

This command registers a set of magic commands (`%sql` for line magics and `%%sql` for cell magics) that allow you to execute SQL code directly.

### 2. Connecting to a Database

SQL magic supports many databases via a single connection string syntax. Here are a few examples:

- **SQLite:**
    
    Connect to a local SQLite database file (which is great for prototyping):
    
    ```python
    %sql sqlite:///sales_dataset.db
    ```
    
    This command tells SQL magic to use SQLite and open (or create) a file named `sales_dataset.db`.
    
- **PostgreSQL:**
    
    Suppose you want to connect to a PostgreSQL database:
    
    ```python
    %sql postgresql://username:password@localhost:5432/salesdb
    ```
    
- **MySQL:**
    
    For MySQL with the mysqlconnector driver:
    
    ```python
    %sql mysql+mysqlconnector://username:password@localhost/salesdb
    
    ```
    

Each connection string is composed of:

- A dialect (sqlite, postgresql, mysql+mysqlconnector, etc.),
- Credentials and host information,
- And the database name.

Once connected, the magic extension maintains the connection for you, and you can now write SQL queries directly in your notebook cells.

### 3. Running SQL Queries with SQL Magic

### A. Using Line Magic `%sql`

For a one-liner SQL query, use `%sql` in a cell:

```python
%sql SELECT * FROM SalesDataset LIMIT 5;
```

This will display the first five records from the `SalesDataset` table in a nicely formatted output.

### B. Using Cell Magic `%%sql`

For multi-line SQL code, start your cell with `%%sql`. For example, to create a table:

```sql
%%sql
CREATE TABLE IF NOT EXISTS SalesDataset (
    Order_Id INTEGER PRIMARY KEY AUTOINCREMENT,
    Amount REAL,
    Profit REAL,
    Quantity INTEGER,
    Category TEXT,
    "Sub-category" TEXT,
    PaymentMode TEXT,
    Order_date TEXT,
    CustomerName TEXT,
    State TEXT,
    City TEXT,
    "Year-Month" TEXT
);
```

The cell magic allows you to write full SQL scripts spanning multiple lines. You can even embed SQL transactions, insert statements, and so on.

### 4. Using Variables and Python Interoperability

SQL magic also lets you pass Python variables into your SQL queries. For example, suppose you want to filter the dataset dynamically:

```python
# Define a Python variable
min_amount = 500

# Use the variable in your SQL query with a colon syntax
%%sql --params min_amount=$min_amount
SELECT Order_Id, Amount, CustomerName
FROM SalesDataset
WHERE Amount > :min_amount;
```

Notice the two things here:

- You pass the Python variable as a parameter using the `-params` flag.
- Inside the SQL code, you use `:min_amount` to refer to the parameter.

This integration makes it seamless to mix Python-driven logic with SQL querying.

### 5. Viewing and Storing Results

When you run a query using SQL magic, the result is returned as a special object that can be inspected or even converted to a Pandas DataFrame. For instance:

```python
result = %sql SELECT * FROM SalesDataset LIMIT 10;
# Convert to a DataFrame for further analysis with Pandas:
df = result.DataFrame()
df.head()
```

This ability to easily transition between SQL results and the Pandas DataFrame structure is powerful for exploratory analysis, data visualization, or further processing directly in Python.

### 6. Practical Workflow Example

Imagine you have uploaded your sales dataset into an SQLite database (`sales_dataset.db`) and you want to perform several operations using SQL magic. Here's an example workflow:

1. **Load SQL Magic and Connect:**
    
    ```python
    %load_ext sql
    %sql sqlite:///sales_dataset.db
    ```
    
2. **Create (or Verify) the Table:**
    
    ```sql
    %%sql
    CREATE TABLE IF NOT EXISTS SalesDataset (
        Order_Id INTEGER PRIMARY KEY AUTOINCREMENT,
        Amount REAL,
        Profit REAL,
        Quantity INTEGER,
        Category TEXT,
        "Sub-category" TEXT,
        PaymentMode TEXT,
        Order_date TEXT,
        CustomerName TEXT,
        State TEXT,
        City TEXT,
        "Year-Month" TEXT
    );
    
    ```
    
3. **Query to Explore the Data:**
    
    ```sql
    %%sql
    SELECT * FROM SalesDataset LIMIT 5;
    ```
    
4. **Filtering Data Dynamically:**
    
    ```python
    min_profit = 100
    %%sql --params min_profit=$min_profit
    SELECT Order_Id, Profit, CustomerName
    FROM SalesDataset
    WHERE Profit > :min_profit;
    ```
    
5. **Summarizing Data:**
    
    ```sql
    %%sql
    SELECT Category, COUNT(Order_Id) AS TotalOrders, SUM(Amount) AS TotalSales
    FROM SalesDataset
    GROUP BY Category;
    ```
    

Each cell allows you to run fully featured SQL queries without leaving your notebook environment while taking advantage of Python's flexibility for dynamic parameters and further analysis.

---

## Analysing data using Python

### 1. Getting Started & Key Libraries

Python’s rich ecosystem for data analysis includes:

- **Pandas** – The workhorse for tabular data (DataFrames, Series).
- **NumPy** – Provides fast, vectorized computations on arrays.
- **Matplotlib** and **Seaborn** – For plotting and visualization.
- **SciPy** – For statistical tests and more scientific computing functions.
- **Scikit-learn** – For machine learning and predictive analytics (if you move beyond descriptive analysis).
- **Jupyter Notebook** – An interactive environment that’s great for EDA and sharing your work.

You’ll typically begin by installing these packages (if you haven’t already):

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
```

### 2. Data Ingestion

Before analyzing data, you first need to load it into Python. Data can be ingested from various sources such as CSV files, Excel workbooks, SQL databases, or even JSON files.

### Example: Loading Data from a CSV File

Let’s assume you have a sales dataset (e.g., `sales_dataset.csv`). You can load it using Pandas:

```python
import pandas as pd

# Read the CSV file into a DataFrame
df = pd.read_csv('sales_dataset.csv')

# Display the first 5 rows to verify the load
print(df.head())
```

For database access, you might use Python’s DB-API or SQLAlchemy to pull data directly into DataFrames (or use the Pandas function `pd.read_sql_query`).

### 3. Data Cleaning and Preparation

Data rarely comes in a perfect shape. Cleaning involves handling missing values, removing duplicates, transforming columns to correct types, and sometimes creating new features.

### Common Tasks:

- **View Data Types:**
    
    ```python
    print(df.dtypes)
    ```
    
- **Handling Missing Data:**
    
    ```python
    # Identify missing values
    print(df.isnull().sum())
    
    # Fill missing values, e.g., with the column's mean or a placeholder
    df['Amount'] = df['Amount'].fillna(df['Amount'].mean())
    df['CustomerName'] = df['CustomerName'].fillna('Unknown')
    ```
    
- **Converting Data Types:**
    
    ```python
    # Convert string dates to datetime objects
    df['Order_date'] = pd.to_datetime(df['Order_date'])
    ```
    
- **Removing Duplicates:**
    
    ```python
    df = df.drop_duplicates()
    ```
    
- **Creating New Columns:**
    
    ```python
    # Suppose your dataset has a "Profit" and "Amount" column; you might create a profit margin:
    df['ProfitMargin'] = df['Profit'] / df['Amount']
    ```
    

This preparation ensures that later analyses are accurate and meaningful.

### 4. Exploratory Data Analysis (EDA)

EDA is the process of exploring your dataset to understand its structure, spot anomalies, test hypotheses, and learn about the underlying distributions.

### Techniques and Tools:

- **Descriptive Statistics:**
    
    ```python
    # Summary statistics for numerical columns
    print(df.describe())
    
    # Information on column types and non-null counts
    print(df.info())
    ```
    
- **Correlation Analysis:**
    
    ```python
    # Get the correlation matrix
    correlation_matrix = df.corr()
    print(correlation_matrix)
    ```
    
- **Grouping and Aggregation:**
    
    ```python
    # Group data by "Category" and get aggregate sales values
    category_summary = df.groupby('Category').agg(
        TotalSales=('Amount', 'sum'),
        AverageProfit=('Profit', 'mean'),
        Orders=('Order_Id', 'count')
    )
    print(category_summary)
    ```
    
- **Pivot Tables:**
    
    ```python
    # Create a pivot table of sales per month per category (assuming "Year-Month" is present)
    pivot = pd.pivot_table(df, values='Amount', index='Year-Month', columns='Category', aggfunc='sum', fill_value=0)
    print(pivot)
    ```
    

EDA is iterative: as you uncover patterns, you refine your queries and visualizations.

### 5. Data Visualization

Visualization is key for communicating findings and revealing patterns that might be hidden in raw numbers. Two widely used libraries are Matplotlib and Seaborn.

### Basic Visualizations:

- **Line Plot (e.g., Sales over Time):**
    
    ```python
    import matplotlib.pyplot as plt
    
    # Plot total sales over time
    sales_over_time = df.groupby('Year-Month')['Amount'].sum()
    sales_over_time.plot(kind='line', figsize=(10, 5))
    plt.title('Total Sales Over Time')
    plt.xlabel('Year-Month')
    plt.ylabel('Sales Amount')
    plt.show()
    ```
    
- **Histogram (Distribution of Sales Amounts):**
    
    ```python
    plt.figure(figsize=(8, 5))
    plt.hist(df['Amount'], bins=20, color='cornflowerblue', edgecolor='black')
    plt.title('Distribution of Sales Amounts')
    plt.xlabel('Amount')
    plt.ylabel('Frequency')
    plt.show()
    ```
    
- **Box Plot (Analyzing Profit Distribution by Category):**
    
    ```python
    import seaborn as sns
    
    plt.figure(figsize=(10, 6))
    sns.boxplot(x='Category', y='Profit', data=df)
    plt.title('Profit Distribution by Category')
    plt.show()
    ```
    
- **Scatter Plot (Relationship between Amount and Profit):**
    
    ```python
    plt.figure(figsize=(8, 5))
    plt.scatter(df['Amount'], df['Profit'], alpha=0.5)
    plt.title('Relationship Between Sales Amount and Profit')
    plt.xlabel('Amount')
    plt.ylabel('Profit')
    plt.show()
    ```
    

Seaborn also provides easy-to-use functions for more sophisticated visualizations like pairplots, heatmaps (for correlation matrices), and categorical plots.

### 6. Advanced Analytics and Machine Learning

If you wish to move beyond descriptive analysis, Python supports advanced techniques that include predictive modeling and clustering.

### Examples:

- **Predictive Modeling:** Using scikit-learn to predict profit or sales from other features.
    
    ```python
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LinearRegression
    from sklearn.metrics import mean_squared_error
    
    # Example: Predict Profit based on Amount and Quantity
    X = df[['Amount', 'Quantity']]
    y = df['Profit']
    
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    
    model = LinearRegression()
    model.fit(X_train, y_train)
    
    predictions = model.predict(X_test)
    mse = mean_squared_error(y_test, predictions)
    print("Mean Squared Error:", mse)
    ```
    
- **Clustering:** Identify groups in your sales data using algorithms like K-means.
    
    ```python
    from sklearn.cluster import KMeans
    
    # Assuming you want to cluster orders based on Amount and Profit
    X = df[['Amount', 'Profit']]
    
    kmeans = KMeans(n_clusters=3, random_state=42)
    df['Cluster'] = kmeans.fit_predict(X)
    
    # Visualize the clusters
    plt.figure(figsize=(8, 5))
    sns.scatterplot(x='Amount', y='Profit', hue='Cluster', data=df, palette='Set2')
    plt.title('Clustering of Orders Based on Amount and Profit')
    plt.show()
    ```
    

These methods help in forecasting trends or uncovering market segments, though they come after the initial exploratory and descriptive analysis.

### 7. Best Practices & Tools for Reproducible Analysis

- **Use Jupyter Notebooks or JupyterLab:**
    
    These interactive environments allow you to mix code, visualizations, and narrative text, making it easier to document your steps.
    
- **Version Control with Git:**
    
    Save your notebooks and scripts in a version control system for reproducibility.
    
- **Automate EDA:**
    
    Tools like [Pandas Profiling](https://pandas-profiling.ydata.ai/) or [Sweetviz](https://github.com/fbdesignpro/sweetviz) can automatically generate comprehensive EDA reports.
    
- **Modularize Your Code:**
    
    Separate data ingestion, cleaning, analysis, and visualization into functions or dedicated scripts. This organization makes it easier to maintain and iterate on your analysis.
    
- **Document Your Workflow:**
    
    Add comments and markdown explanations in your notebooks so that your thought process is clear to collaborators and to your future self.
    

---

## Quick recap:

1. **SQLite3 as an In-Process Library:**
    
    We explained that SQLite3 is a self-contained, serverless, zero-configuration database engine that runs in-process. This makes it ideal for prototyping or smaller-scale applications since you don't have to manage a separate database server.
    
2. **Reading CSV Files with Pandas:**
    
    We touched on using `pandas.read_csv` to load CSV data into a DataFrame. This is often the first step when you have data stored as CSV files and want to explore or import it into a database.
    
    ```python
    import pandas as pd
    df = pd.read_csv('sales_dataset.csv')
    print(df.head())
    ```
    
3. **Connecting to a Database with SQLite3:**
    
    We showed how to use `sqlite3.connect` to establish a connection to a database file. This function opens the connection to the SQLite database (creating the file if it doesn't exist).
    
    ```python
    import sqlite3
    connection = sqlite3.connect('sales_dataset.db')
    cursor = connection.cursor()
    ```
    
4. **Using Pandas to Retrieve Data via SQL:**
    
    We demonstrated how to use Pandas' `read_sql_query` (or `read_sql`) method to execute a SQL SELECT query and load data directly from your database into a DataFrame for analysis.
    
    ```python
    df = pd.read_sql_query("SELECT * FROM SalesDataset LIMIT 10;", connection)
    ```
    
5. **Visualizing Data with Seaborn's Swarmplot:**
    
    We also covered data visualization techniques using Seaborn—for example, creating a categorical scatterplot (a swarmplot) which shows the distribution of data points across different categories.
    
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt
    
    # Assume df is your DataFrame loaded with relevant data
    plt.figure(figsize=(10, 6))
    sns.swarmplot(x='Category', y='Amount', data=df)
    plt.title('Categorical Distribution of Sales Amounts')
    plt.show()
    ```
    

Each of these components plays an essential role in the overall workflow for analyzing data with Python - From data ingestion (reading CSVs), connecting to and querying a database (using SQLite3 and Pandas), and finally, visualizing insights (with Seaborn).