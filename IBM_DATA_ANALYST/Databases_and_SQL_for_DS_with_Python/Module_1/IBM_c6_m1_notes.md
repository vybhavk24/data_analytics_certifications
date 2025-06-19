# IBM_c6_m1

## Data and Database:

### 1. What Is Data?

### **Definition and Nature**

- **Data** refers to discrete pieces of information. It can be anything from numbers and text to images and sensor readings. Think of data as the raw ingredients of any analysis.
- It’s **unprocessed** information. For example, a list of temperatures over a week is data. Once we do something with it—calculate averages, draw trends—it transitions into information.

### **Types of Data**

- **Structured Data:**
This is highly organized and often stored in tables (like Excel sheets or databases). Each piece of data fits neatly into rows and columns. For example, a customer table with columns for name, email, and purchase history.
- **Unstructured Data:**
Data that doesn’t follow a specific format, such as images, videos, or email texts. Although rich in information, unstructured data requires special processing to extract usable insights.
- **Semi-Structured Data:**
Falls in between the two—for instance, JSON or XML files, which have organizational properties but are not as rigid as relational tables.

### **Real-World Importance**

- **Decision-Making:**
Data is the fuel behind decisions. From a business determining its marketing strategy to a scientist testing a hypothesis, interpreting data accurately is crucial.
- **Personalization:**
Many products and services today—from streaming recommendations to targeted ads—rely on data analysis of user behavior and preferences.

### 2. What Is a Database?

### **Definition and Purpose**

- A **database** is an organized collection of data, typically stored and accessed electronically from a computer system. Think of it as a digital filing cabinet that ensures information is neatly categorized for quick lookup and analysis.
- **Purpose:**
It facilitates the storage, retrieval, and management of data efficiently. For data analysts, databases are invaluable because they provide a structured environment to write queries, extract insights, and update records as new data comes in.

### **Types of Databases**

### **Relational Databases (SQL Databases)**

- **Structure:**
Data is stored in tables made up of rows and columns. Each row represents a record and each column a field.
- **Key Concepts:**
    - **Primary Keys:** Unique identifiers for each record.
    - **Foreign Keys:** Fields that link rows in different tables, helping maintain relationships between data.
    - **Normalization:** Organizing data to reduce redundancy, ensuring that each piece of information is stored only once.
- **Examples:**
MySQL, PostgreSQL, SQLite, and Microsoft SQL Server.
- **Use in Data Science:**
They support complex queries, aggregations, and joins that enable deep insights into structured data—vital for reports, dashboards, and predictive analysis.

### **Non-Relational Databases (NoSQL Databases)**

- **Structure:**
These can be document-based, key-value stores, wide-column, or graph databases. They are designed to handle large volumes of unstructured or semi-structured data.
- **Common Use Cases:**
Big data analytics, real-time web applications, and scenarios where rapid scaling is needed.
- **Examples:**
MongoDB, Cassandra, Redis, and Neo4j.

### **Real-World Relevance**

- **Scalability and Performance:**
Businesses deal with massive volumes of data daily. Databases are optimized for both speed and integrity, ensuring that data is consistent, reliable, and quickly accessible.
- **Integration:**
In a data analyst's role, you might extract data from a relational database to create reports in BI tools or visualize in Python notebooks. A solid understanding helps you optimize these processes.
- **Security:**
Databases incorporate layers of security to protect sensitive data—vital for industries like finance and healthcare.

### 3. How Data and Databases Work Together

Imagine you’re analyzing customer data for an online business:

- **Data Collection:**
Every customer transaction (data) is recorded.
- **Storage:**
These transactions are stored in a relational database with tables for customers, orders, and products.
- **Querying:**
Using SQL (Structured Query Language), you can write queries to join these tables, aggregate the data (like summing total sales), or filter it (such as retrieving transactions for a specific period).
- **Analysis:**
Once you have refined data from your queries, you can import it into Python (via libraries like Pandas) for advanced analytics, visualization, or predictive modeling.

### 4. Practical Hands-On: A Simple SQL Experiment with SQLite

### **Why This Exercise?**

SQLite is a lightweight, file-based database that's perfect for beginners. It allows you to practice SQL without complex installations or server configurations.

### **Setup and Exercise in VS Code or Jupyter Notebook**

### **Step 1: Create a Simple Database**

```python
import sqlite3

# Create a new SQLite connection (or connect to an existing database file)
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# Create a table
cursor.execute('''
CREATE TABLE IF NOT EXISTS customers (
    id INTEGER PRIMARY KEY,
    name TEXT,
    email TEXT,
    age INTEGER
)
''')
conn.commit()
print("Table created successfully!")
```

*What you’re doing:*

- Connecting to a database file named `example.db`.
- Creating a table named `customers` with columns for ID, name, email, and age.

### **Step 2: Insert Some Data**

```python
# Insert some records into the table
customers = [
    ("Alice", "alice@example.com", 30),
    ("Bob", "bob@example.com", 25),
    ("Charlie", "charlie@example.com", 35)
]

cursor.executemany('''
INSERT INTO customers (name, email, age) VALUES (?, ?, ?)
''', customers)
conn.commit()
print("Data inserted successfully!")
```

*What you’re doing:*

- Inserting multiple customer records into the database.

### **Step 3: Query the Data**

```python
# Query the data: select all customers older than 28
cursor.execute('''
SELECT * FROM customers WHERE age > 28
''')
results = cursor.fetchall()

print("Customers older than 28:")
for row in results:
    print(row)
```

*What you’re doing:*

- Writing a query to select customers based on a condition and then printing the results.

### **Step 4: Close the Connection**

```python
conn.close()
print("Database connection closed!")
```

*Why this matters:*

It’s always good practice to close your connections to free up resources and ensure data integrity.

### 5. Why Mastering Data and Databases Is Crucial for a Data Analyst

- **Foundational Skill:**
Every real-world data project begins with data collection and storage. Without a solid understanding of databases, your analyses might become inefficient or error-prone.
- **Data Integrity and Cleaning:**
Knowing how data is structured helps you clean and validate it effectively—essential for drawing accurate conclusions.
- **Scalable Solutions:**
As data volume increases, efficient database management becomes indispensable for performance.
- **Enhanced Analysis:**
Combining your SQL skills with tools like Python (and libraries like Pandas) can make your insights richer and more compelling.

---

## Basic Info:

### 1. Data

**What It Is:**

- **Data** represents raw facts and figures—numbers, texts, dates, images, or any measurable information.
- Think of data as the raw ingredients in a recipe. On its own, it’s unrefined and requires context or organization to become meaningful.

**Real-World Example:**

Imagine tracking temperatures over a week or recording customer names and purchases. These individual pieces of information are your data.

### 2. Database

**What It Is:**

- A **database** is a systematic way to store and manage data.
- It’s like a digital filing cabinet where data is organized so you can quickly search, update, or analyze the information stored inside.

**Why It Matters:**

Organizing data into a database prevents chaos. Whether you’re managing a small list of contacts or a vast repository of business transactions, a database provides structure and integrity.

### 3. Relational Databases

**What They Are:**

- **Relational databases** are a specific type of database that organizes data into structured tables.
- Each table (like a spreadsheet) contains rows (records) and columns (fields), and tables can be related to one another through keys.

**Key Concepts:**

- **Tables:** Collections of related data.
- **Rows:** Individual records (for example, one customer’s information).
- **Columns:** Attributes of the data (like customer name, email, age).

**Why They Matter:**

The relational model makes it easy to link data across different tables, ensuring that complex relationships (like a customer's orders or transactions) are maintained and can be queried efficiently.

### 4. RDBMS (Relational Database Management System)

**What It Is:**

- An **RDBMS** is the software that manages relational databases.
- It controls how data is stored, retrieved, updated, and secured. Popular RDBMS include MySQL, PostgreSQL, SQLite, and Microsoft SQL Server.

**Key Functions:**

- **Data Integrity:** Ensuring that relationships between tables are maintained without errors.
- **Query Handling:** Interpreting SQL commands to perform tasks like data retrieval or modification.
- **Security & Concurrency:** Managing user permissions and handling multiple users accessing data simultaneously.

**Real-World Importance:**

Whether you're in finance, healthcare, or e-commerce, RDBMS systems form the backbone of data operations, making sure data remains consistent, secure, and accessible.

### 5. SQL (Structured Query Language)

**What It Is:**

- **SQL** is the language used to interact with RDBMS. It’s like the set of instructions you give to your RDBMS to perform specific tasks.
- Through SQL, you define structures, insert data, update information, and retrieve data insights.

**Why It Matters:**

SQL is widely used in nearly every industry that relies on data. Learning SQL empowers you to extract meaningful insights from databases, a key skill for any data analyst.

### 6. Basic SQL Commands

These commands are the building blocks for managing and interacting with your data in an RDBMS:

### a. `CREATE`

- **Purpose:** Define new database objects like tables.
- **Example Code:**
    
    ```sql
    CREATE TABLE customers (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        email TEXT NOT NULL,
        age INTEGER
    );
    ```
    
- **Explanation:** This command sets up a new table named `customers` that will later store your data.

### b. `INSERT`

- **Purpose:** Add new records to your tables.
- **Example Code:**
    
    ```sql
    INSERT INTO customers (name, email, age)
    VALUES ('Alice', 'alice@example.com', 30);
    ```
    
- **Explanation:** It adds a new row to the `customers` table, inserting the data provided.

### c. `SELECT`

- **Purpose:** Retrieve data from the database.
- **Example Code:**
    
    ```sql
    SELECT * FROM customers;
    ```
    
- **Explanation:** This command fetches all columns for every record in the `customers` table. It can be refined using conditions to filter specific subsets of data.

### d. `UPDATE`

- **Purpose:** Modify existing data within a table.
- **Example Code:**
    
    ```sql
    UPDATE customers
    SET email = 'alice.new@example.com'
    WHERE name = 'Alice';
    ```
    
- **Explanation:** It changes the email address for the customer named "Alice." Always use a `WHERE` clause to update only specific records.

### e. `DELETE`

- **Purpose:** Remove records from your table.
- **Example Code:**
    
    ```sql
    DELETE FROM customers
    WHERE name = 'Alice';
    ```
    
- **Explanation:** This command removes the record for the customer "Alice." Without a `WHERE` clause, it would remove all records from the table.

### Putting It All Together

**Chronological Flow Recap:**

1. **Data:** The raw ingredients (e.g., customer names, temperatures).
2. **Database:** The container that organizes your data systematically.
3. **Relational Database:** A type of database that structures data into interconnected tables.
4. **RDBMS:** The software that manages relational databases, ensuring data integrity and accessibility.
5. **SQL:** The language that you use to communicate with your RDBMS.
6. **Basic SQL Commands:** The individual instructions (`CREATE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`) that let you build, populate, and manipulate your database.

**Real-World Application:**

Imagine you're working at an online store. You first gather raw data about customer purchases. You then store this data in a relational database managed by an RDBMS. Using SQL, you can create tables for customers and orders, insert the daily transactions, query these records to analyze buying patterns, update details if a customer changes their information, and delete records that are no longer needed.

This step-by-step evolution holds great significance, as understanding each layer equips you to handle complex data projects efficiently—from initial data collection to detailed analytical insights.

---

## CREATE statement:

### 1. The Role of the CREATE Statement

The **CREATE** statement defines the structure of a database object, setting the foundation for how your data will be stored. Think of it as drawing the blueprint for your data "home." Every column, its data type, and the constraints (rules) are laid out here. This planning is indispensable for ensuring data integrity and proper query performance later on.

### **Why It Matters:**

- **Structure and Order:** Creating tables with thoughtful design helps prevent data inconsistencies.
- **Data Integrity:** Constraints (like primary keys and foreign keys) enforce the rules that protect your data.
- **Long-Term Maintenance:** A well-designed schema makes future data integration, modification, and scaling much simpler.

### 2. Basic Syntax of CREATE TABLE

When creating a table, the standard syntax is:

```sql
CREATE TABLE table_name (
    column1 datatype [constraint],
    column2 datatype [constraint],
    ...
);
```

### **Breaking Down the Components:**

- **`table_name`:** The name you give to your new table.
- **Columns:** Define the fields that will hold your data.
    - **Data types:** Specify what kind of data will be stored (e.g., INTEGER, TEXT, DATE, REAL).
    - **Constraints:** Rules like `NOT NULL`, `PRIMARY KEY`, `UNIQUE`, `DEFAULT`, or even `FOREIGN KEY` relationships to other tables.

### 3. In-Depth: Creating a Table with Examples

Let’s build a simple table for a customer database.

### **Example 1: A Simple Customers Table**

```sql
CREATE TABLE customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE,
    age INTEGER,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Explanation:**

- **`id INTEGER PRIMARY KEY AUTOINCREMENT`:**
This creates a unique identifier for each customer. The `AUTOINCREMENT` keyword automatically generates a sequential number every time a new record is inserted.
- **`name TEXT NOT NULL`:**
The `name` column stores text data and cannot be NULL, ensuring that every customer has a name.
- **`email TEXT NOT NULL UNIQUE`:**
This column stores email addresses. The `UNIQUE` constraint prevents duplicate email entries—a common requirement for customer databases.
- **`age INTEGER`:**
An optional numeric field recording the customer's age.
- **`created_at DATETIME DEFAULT CURRENT_TIMESTAMP`:**
Automatically records the date and time when a record is inserted, ensuring you have a log of when each customer was added.

### **Example 2: Creating a Table with a Foreign Key**

Imagine you have a second table for orders, and each order is linked to a customer from the customers table. You could create the orders table like this:

```sql
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER,
    order_date DATE NOT NULL,
    amount REAL,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

**Explanation:**

- **`order_id INTEGER PRIMARY KEY AUTOINCREMENT`:**
Defines a unique order identifier.
- **`customer_id INTEGER`:**
This column will store the ID of the customer who placed each order.
- **`order_date DATE NOT NULL`:**
Stores the date of the order; must be provided.
- **`amount REAL`:**
Represents the order amount, allowing decimal values.
- **`FOREIGN KEY (customer_id) REFERENCES customers(id)`:**
Establishes a relationship between the orders table and the customers table, ensuring that every order is associated with a valid customer.

### 4. Practical Hands-On: Creating Tables in Python with SQLite

### **Step-by-Step Exercise**

If you’re using SQLite and Python, here’s a complete example you can run in VS Code or a Jupyter Notebook:

```python
import sqlite3

# Connect to a database (or create it if it doesn't exist)
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# Create the customers table
cursor.execute('''
CREATE TABLE IF NOT EXISTS customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE,
    age INTEGER,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
)
''')
conn.commit()
print("Customers table created successfully!")

# Create the orders table with a foreign key relationship
cursor.execute('''
CREATE TABLE IF NOT EXISTS orders (
    order_id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER,
    order_date DATE NOT NULL,
    amount REAL,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
)
''')
conn.commit()
print("Orders table created successfully!")

# Close the connection when done
conn.close()
print("Database connection closed!")
```

**What this does:**

- **Connects** to (or creates) a database file named 'example.db'.
- **Creates** the `customers` table with mandatory fields and constraints.
- **Creates** the `orders` table, showing how to enforce relationships using foreign keys.
- Finally, it **commits** the transactions and **closes** the connection.

### 5. Beyond CREATE TABLE

While creating tables is the cornerstone of designing your database, the **CREATE** statement can also be used for:

- **CREATE INDEX:** To improve query performance.
- **CREATE VIEW:** To generate virtual tables based on select queries.
- **CREATE DATABASE:** To instantiate a new database in systems that support multiple databases.

Each of these variants builds on the concept of defining database objects and ensuring your data logic is robust and efficient.

---

## SELECT Statement:

### 1. The Role of SELECT in SQL

At its simplest, a **SELECT** statement gathers data from one or more tables in your database. Think of it as defining your “projection” from the table(s)—you decide which columns (or derived expressions) you want to see. 

For data analysts, this is the starting point of every query, whether you’re checking raw data for errors or extracting insights for reporting.

### 2. Basic Structure and Components

The canonical form of a SELECT statement looks like this:

```sql
SELECT [DISTINCT] <select_list>
FROM <table_reference>
[WHERE <condition>]
[GROUP BY <grouping_columns>]
[HAVING <group_condition>]
[ORDER BY <sorting_columns> [ASC|DESC]]
[LIMIT <number> [OFFSET <number>]];
```

Even if you only need a simple query, understanding these components is key.

### Components Breakdown

1. **SELECT clause**
    - **What it does:** Specifies the columns or expressions to be returned.
    - **Details:**
        - You can list column names directly, use arithmetic operations, call functions (e.g., `COUNT()`, `SUM()`, `UPPER()`), or even include constant values.
        - The `DISTINCT` keyword (if placed right after `SELECT`) ensures that duplicate rows are eliminated.
    - **Example:**
    This retrieves unique combinations of `name` and `age` from the **customers** table.
        
        ```sql
        SELECT DISTINCT name, age FROM customers;
        ```
        
2. **FROM clause**
    - **What it does:** Tells the database which table(s) to pull data from.
    - **Details:**
        - You can specify single or multiple tables. When more than one table is involved, you often include joins to tell the database how the tables relate.
    - **Example:**
        
        ```sql
        FROM customers;
        ```
        
3. **WHERE clause**
    - **What it does:** Filters rows based on specified conditions.
    - **Details:**
        - Conditions can use equality, inequality, pattern matching (like `LIKE`), range checking (`BETWEEN`), etc.
    - **Example:**
    This filters the rows to only include customers older than 30.
        
        ```sql
        WHERE age > 30;
        ```
        
4. **GROUP BY clause**
    - **What it does:** Aggregates rows that share common values in one or more columns.
    - **Details:**
        - Typically used with aggregate functions (like `COUNT()`, `SUM()`, `AVG()`).
        - Only columns in the `GROUP BY` or aggregates can go in your `SELECT` list.
    - **Example:**
    This groups all rows by distinct ages so you can perform calculations on each group.
        
        ```sql
        GROUP BY age;
        ```
        
5. **HAVING clause**
    - **What it does:** Filters groups created by `GROUP BY` conditions.
    - **Details:**
        - Similar to the `WHERE` clause, but applies after grouping.
    - **Example:**
    This keeps only those groups that have more than one row (or entry).
        
        ```sql
        HAVING COUNT(*) > 1;
        ```
        
6. **ORDER BY clause**
    - **What it does:** Defines the order of the returned rows.
    - **Details:**
        - You can sort on one or multiple columns and specify ascending (`ASC`, the default) or descending (`DESC`) order.
    - **Example:**
    This sorts the results so that the oldest customers appear first.
        
        ```sql
        ORDER BY age DESC;
        ```
        
7. **LIMIT and OFFSET clauses**
    - **What they do:** Control how many rows are returned and from which row the result starts.
    - **Details:**
        - `LIMIT` restricts the number of rows, and `OFFSET` is used to skip a number of rows before beginning to return rows.
    - **Example:**
    This skips the first 5 rows and then returns the next 10 rows.
        
        ```sql
        LIMIT 10 OFFSET 5;
        ```
        

### 3. The Logical Processing Order

Although the SELECT statement is written in the order we just saw, SQL processes the statement in a different logical sequence:

1. **FROM & JOIN:** SQL first establishes the data source. If multiple tables are involved, the joins are executed here.
2. **WHERE:** The filtering conditions are applied next, eliminating rows that don’t meet the criteria.
3. **GROUP BY:** Rows that passed the WHERE clause are grouped together.
4. **HAVING:** Groups are then filtered based on the conditions applied to aggregates.
5. **SELECT:** Now the actual columns or expressions are computed.
6. **ORDER BY:** Finally, the results are sorted and then the row limit (if any) is applied.

Understanding this order matters when you’re diagnosing a query’s behavior or optimizing its performance.

### 4. Advanced SELECT Topics

### a. Using Expressions and Functions

You’re not limited to pulling raw columns from your table. You can perform calculations or manipulate data as needed:

```sql
SELECT
    name,
    age,
    age * 12 AS age_in_months,
    UPPER(name) AS uppercase_name
FROM customers;
```

- Here, `age * 12` calculates a derived value, and `UPPER(name)` makes the name capitalized. The `AS` keyword is used for aliasing to give these expressions readable names.

### b. Filtering with WHERE

The `WHERE` clause comes in many powerful forms:

- **Simple condition:**
    
    ```sql
    WHERE age > 25;
    ```
    
- **Multiple conditions:**
    
    ```sql
    WHERE age > 25 AND city = 'Bengaluru';
    ```
    
- **Pattern matching with LIKE:**
    
    ```sql
    WHERE name LIKE 'A%';  -- Names that start with A
    ```
    
- **Range filtering with BETWEEN:**
    
    ```sql
    WHERE age BETWEEN 20 AND 30;
    ```
    

### c. Aggregation with GROUP BY and HAVING

Aggregation functions allow you to summarize data. For example, if you wanted to know how many customers there are for each age:

```sql
SELECT age, COUNT(*) AS customer_count
FROM customers
GROUP BY age;
```

If you then wanted only groups having more than a certain number:

```sql
SELECT age, COUNT(*) AS customer_count
FROM customers
GROUP BY age
HAVING COUNT(*) > 1;
```

### d. Sorting with ORDER BY

Sorting is crucial for reports. You can sort by a single column or multiple columns:

```sql
SELECT name, age
FROM customers
ORDER BY age ASC, name DESC;
```

This query sorts first by age (smallest to largest) and then, for customers with the same age, orders the names in descending order.

### e. Limiting Results

When testing queries or dealing with large datasets, you might not want to fetch every row:

```sql
SELECT *
FROM customers
ORDER BY id
LIMIT 5;
```

This returns only the first five rows.

### 5. Real-World Application: Putting SELECT to Use

Imagine you’re working with a **customers** table that has millions of records. Your analyses might include:

- **Fetching Customer Snapshots:**
    
    Every day, you might run a query to see the most recent customer sign-ups:
    
    ```sql
    SELECT id, name, created_at
    FROM customers
    ORDER BY created_at DESC
    LIMIT 10;
    ```
    
- **Segmenting Data for Insights:**
    
    To understand your customer base, you might group customers by age or region:
    
    ```sql
    SELECT state, COUNT(*) AS total_customers, AVG(age) AS avg_age
    FROM customers
    GROUP BY state;
    ```
    
- **Data Validation:**
    
    If you need to check for unusual data entries, you might use:
    
    ```sql
    SELECT *
    FROM customers
    WHERE age < 0 OR age > 120;
    ```
    
    This helps ensure data quality by flagging improbable values.
    
- **Subqueries for Comparative Metrics:**
    
    A common advanced pattern is using subqueries:
    
    ```sql
    SELECT name, age
    FROM customers
    WHERE age > (SELECT AVG(age) FROM customers);
    ```
    
    This query returns customers older than the average age, blending aggregation and row-level filtering.
    

### 6. Hands-On Exercise in Python with SQLite

To get some practical experience, try this in a Jupyter Notebook or VS Code with SQLite:

```python
import sqlite3

# Connect to a test database (or create it if not exists)
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# Create a simple customers table
cursor.execute('''
CREATE TABLE IF NOT EXISTS customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    age INTEGER,
    city TEXT,
    created_at TEXT DEFAULT (datetime('now'))
)
''')
conn.commit()

# Insert some sample data
customers_data = [
    ("Alice", 30, "Bengaluru"),
    ("Bob", 25, "Mumbai"),
    ("Charlie", 35, "Delhi"),
    ("Anita", 28, "Bengaluru"),
    ("David", 22, "Hyderabad")
]

cursor.executemany('''
INSERT INTO customers (name, age, city) VALUES (?, ?, ?)
''', customers_data)
conn.commit()

# Basic SELECT: Retrieve all customer records
cursor.execute('SELECT * FROM customers')
print("All customers:")
for row in cursor.fetchall():
    print(row)

# Advanced SELECT: Fetch customers from Bengaluru older than 25, ordered by age descending
query = '''
SELECT name, age, city
FROM customers
WHERE city = 'Bengaluru' AND age > 25
ORDER BY age DESC
'''
cursor.execute(query)
print("\\nFiltered customers (Bengaluru, age > 25):")
for row in cursor.fetchall():
    print(row)

# Aggregate function: Count customers by city
query_agg = '''
SELECT city, COUNT(*) AS total_customers
FROM customers
GROUP BY city
HAVING total_customers > 0
ORDER BY total_customers DESC
'''
cursor.execute(query_agg)
print("\\nNumber of customers by city:")
for row in cursor.fetchall():
    print(row)

conn.close()
```

**What this exercise does:**

- **Creates** a simple table to simulate customer data.
- **Inserts** multiple records.
- **Queries** all records, then filters for specific conditions.
- **Aggregates** data with grouping and ordering.

Running these examples helps you see firsthand how different SELECT statement features work together to produce useful insights.

---

## **COUNT**, **DISTINCT**, and **LIMIT**

### 1. COUNT

### **What It Is:**

- **COUNT** is an aggregate function that tallies the number of rows (or distinct non-null values) in a result set. It’s one of the most common ways to summarize data.

### **Usage & Variants:**

1. **COUNT(*)**
    - **Purpose:** Counts every row in the specified table or result set, regardless of whether the columns hold `NULL` values.
    - **Example:**
    This query will return the total number of customer records.
        
        ```sql
        SELECT COUNT(*) AS total_customers
        FROM customers;
        ```
        
2. **COUNT(column_name)**
    - **Purpose:** Counts only the non-null values in a specific column.
    - **Example:**
    This returns the number of customers that have a value in the email column (ignoring any `NULL`).
        
        ```sql
        SELECT COUNT(email) AS total_emails
        FROM customers;
        ```
        
3. **COUNT(DISTINCT column_name)**
    - **Purpose:** Counts the number of distinct non-null values in a column. This is useful when duplicates might exist.
    - **Example:**
    This tells you how many unique cities are represented in your customer data.
        
        ```sql
        SELECT COUNT(DISTINCT city) AS unique_cities
        FROM customers;
        ```
        

### **Real-World Application:**

Imagine you run an e-commerce business and want to know how many orders were made during a sale period. Using `COUNT(*)` gives you a quick summary of total orders, whereas if you want to know the number of customers who placed orders, you might use `COUNT(DISTINCT customer_id)`. This helps in tailoring business strategies based on customer engagement and order volume.

### 2. DISTINCT

### **What It Is:**

- **DISTINCT** is a keyword that filters out duplicate rows in your query results, ensuring that each row is unique for the columns selected.

### **Usage & Considerations:**

1. **Basic DISTINCT on a Single Column:**
    
    ```sql
    SELECT DISTINCT city
    FROM customers;
    ```
    
    - **Explanation:** This query returns a list of different cities from the `customers` table, eliminating duplicates.
2. **DISTINCT on Multiple Columns:**
    
    ```sql
    SELECT DISTINCT state, city
    FROM customers;
    ```
    
    - **Explanation:** When used with more than one column, the combination of values is considered. Only unique combinations of `state` and `city` are returned.
3. **Combining DISTINCT with Aggregate Functions:**
    - You can use DISTINCT within aggregate functions such as COUNT to avoid counting duplicates:
        
        ```sql
        SELECT COUNT(DISTINCT product_id) AS unique_products_sold
        FROM orders;
        ```
        
    - **Explanation:** Here, the query counts only the unique product IDs, which is essential when one product appears in multiple orders.

### **Real-World Application:**

If you want to generate a mailing list or analyze customer locations without repetition, using DISTINCT helps you derive a clean, distinct set of values. For example, knowing the different cities your customers live in can assist in regional marketing or logistics planning.

### 3. LIMIT

### **What It Is:**

- **LIMIT** constrains the number of rows returned by a query. This is particularly useful when dealing with large datasets or when you want to preview a subset of results.

### **Usage & Examples:**

1. **Basic LIMIT:**
    
    ```sql
    SELECT *
    FROM customers
    LIMIT 5;
    ```
    
    - **Explanation:** This query returns only the first 5 rows from the `customers` table.
2. **LIMIT with OFFSET:**
    - **Purpose:** The **OFFSET** clause skips a specified number of rows before starting to return rows.
    
    ```sql
    SELECT *
    FROM customers
    ORDER BY id
    LIMIT 5 OFFSET 10;
    ```
    
    - **Explanation:** This query bypasses the first 10 rows and then returns the next 5 rows. It’s especially helpful for pagination in user interfaces.
3. **Combining LIMIT with ORDER BY:**
    - When you use LIMIT, it's common to pair it with ORDER BY to ensure that the subset of rows returned is consistent and meaningful.
    
    ```sql
    SELECT name, created_at
    FROM customers
    ORDER BY created_at DESC
    LIMIT 10;
    ```
    
    - **Explanation:** This returns the 10 most recent customer records, which you might use to check new sign-ups.

### **Real-World Application:**

In web applications, you'd often use LIMIT and OFFSET for paginating results (e.g., displaying pages in a customer dashboard). In data analysis, this allows you to test queries quickly without waiting for a huge dataset to load completely.

### Putting It All Together

### **Example Query Combining COUNT, DISTINCT, and LIMIT:**

Imagine you want to know the number of unique cities represented in your customer data, but you’re only interested in reviewing a small sample of your full dataset at a time:

```sql
SELECT DISTINCT city
FROM customers
ORDER BY city
LIMIT 10;
```

- **What this does:**
    - **DISTINCT city:** Retrieves unique city names.
    - **ORDER BY city:** Sorts them alphabetically (or you can sort by popularity, depending on your metric).
    - **LIMIT 10:** Shows you the first 10 unique cities.

And if you wanted to count them all:

```sql
SELECT COUNT(DISTINCT city) AS unique_city_count
FROM customers;
```

This query returns a single number—the number of unique cities in your table.

---

## INSERT statement

### 1. What is the INSERT Statement?

The **INSERT** statement is used to add one or more new rows to a table in a database. Think of it as "feeding" your database with new pieces of information. For a data analyst or a developer, this is an everyday operation when working with data pipelines, data cleaning tasks, or even populating initial test data.

### 2. Basic Syntax

The simplest form of an INSERT statement looks like this:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

### **Key Points:**

- **`table_name`:** The name of the table where you want to insert data.
- **`(column1, column2, ...)`:** The list of columns that you are providing values for.
    - You can omit the column list if you are inserting a value into every column of the table—in the exact order they were created—but it’s safer and clearer to specify them.
- **`VALUES (value1, value2, ...)`:** The list of values corresponding to each column listed.

### 3. Variations and Advanced Uses

### **A. Inserting Into Specific Columns**

By specifying the columns, you're giving a clear mapping between each value and its corresponding column. This is especially useful when some columns have default values or allow `NULL`.

```sql
INSERT INTO customers (name, email, age)
VALUES ('Alice', 'alice@example.com', 30);
```

This statement:

- Inserts a new row into the `customers` table,
- Sets the `name` to "Alice", the `email` to "[alice@example.com](mailto:alice@example.com)", and `age` to 30.

### **B. Inserting Multiple Rows**

You can insert multiple rows with one single INSERT command, which is more efficient than running multiple separate INSERT statements:

```sql
INSERT INTO customers (name, email, age)
VALUES
  ('Bob', 'bob@example.com', 25),
  ('Charlie', 'charlie@example.com', 35),
  ('Diana', 'diana@example.com', 28);
```

This command adds three rows into the `customers` table in one go.

### **C. Default and Auto-Increment Columns**

Many tables have columns like an auto-incrementing primary key. When inserting data, you typically leave these out, as the RDBMS takes care of them automatically:

```sql
INSERT INTO customers (name, email, age)
VALUES ('Eve', 'eve@example.com', 32);

```

If your table is defined with an auto-incrementing column (say `id`), you don’t need to specify it in your column list.

### **D. Using Prepared Statements for Safety**

When incorporating user input, it is best practice to use parameterized queries or prepared statements. This protects against SQL injection and ensures your data is correctly formatted. For example, using Python’s SQLite library:

```python
import sqlite3

# Connect to the database
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# A prepared statement with placeholders (?)
sql = "INSERT INTO customers (name, email, age) VALUES (?, ?, ?)"
values = ("Frank", "frank@example.com", 40)

cursor.execute(sql, values)
conn.commit()

print("Record inserted successfully!")
conn.close()
```

Here:

- `?` placeholders indicate where each value should be inserted.
- This method ensures that your data is safely inserted without risking SQL injection.

### 4. Practical Use Case Example

Imagine you’re populating your customer database with initial data for an online store. This might be the first step before you run any analysis, such as calculating the average age of your customers or segmenting them by location.

### Step-by-Step in Python (Using SQLite)

1. **Create a table:**
    
    You first ensure your table is set up.
    
    ```python
    import sqlite3
    
    conn = sqlite3.connect('example.db')
    cursor = conn.cursor()
    
    cursor.execute('''
    CREATE TABLE IF NOT EXISTS customers (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        email TEXT NOT NULL,
        age INTEGER
    )
    ''')
    conn.commit()
    print("Table created successfully!")
    ```
    
2. **Insert a Single Record:**
    
    ```python
    cursor.execute('''
    INSERT INTO customers (name, email, age)
    VALUES ('Alice', 'alice@example.com', 30)
    ''')
    conn.commit()
    print("Single record inserted!")
    ```
    
3. **Insert Multiple Records:**
    
    ```python
    customers = [
        ('Bob', 'bob@example.com', 25),
        ('Charlie', 'charlie@example.com', 35),
        ('Diana', 'diana@example.com', 28)
    ]
    
    cursor.executemany('''
    INSERT INTO customers (name, email, age)
    VALUES (?, ?, ?)
    ''', customers)
    conn.commit()
    print("Multiple records inserted!")
    ```
    
4. **Final Step: Close the Connection**
    
    ```python
    conn.close()
    print("Database connection closed!")
    ```
    

This hands-on example helps you understand:

- How to structure INSERT statements,
- How to add data safely,
- And how to manage database transactions in a programming environment.

---

## UPDATE and DELETE statement:

### 1. UPDATE Statement

### **What It Is**

The **UPDATE** statement is used to modify existing records in a table. Whether you're correcting an error, adjusting a value, or applying a calculated change (like a salary raise), UPDATE lets you change one or more columns in one or more rows.

### **Basic Syntax**

The canonical syntax to update data is:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

- **`table_name`**: The name of the table where you want to update data.
- **`SET` clause**: Specifies each column and the new value. You can update one or several columns simultaneously.
- **`WHERE` clause**: Determines which rows to update. **Without a WHERE clause, every row in the table will be updated**, which is rarely desired.

### **Detailed Examples**

### **Example 1: Updating a Single Column**

Imagine a **customers** table where you need to update Bob's email address:

```sql
UPDATE customers
SET email = 'bob.new@example.com'
WHERE name = 'Bob';
```

- **What’s happening:**
Bob’s record gets modified so that his email field is set to the new value. The WHERE clause assures that only Bob’s record is altered.

### **Example 2: Updating Multiple Columns**

If you need to update more than one aspect of a record, you can list several column assignments:

```sql
UPDATE customers
SET email = 'charlie.new@example.com', age = 36
WHERE name = 'Charlie';
```

- **What’s happening:**
Charlie’s email and age fields get updated in one go.

### **Example 3: Updating Without a WHERE Clause (Caution!)**

```sql
UPDATE customers
SET status = 'active';
```

- **Caution:**
This query will update the `status` field to 'active' for **every** row in the `customers` table. Always double-check your WHERE clause unless your intent is to update the entire table.

### **Using UPDATE in a Practical Environment**

Here’s how you might run an UPDATE in Python using SQLite:

```python
import sqlite3

# Connect (or create) an example database
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# Suppose we have our customers table already created and populated.
# Example: Update Bob's email address.
cursor.execute('''
UPDATE customers
SET email = ?
WHERE name = ?
''', ('bob.new@example.com', 'Bob'))

conn.commit()
print("Record updated successfully!")
conn.close()
```

- **Explanation:**
Using a prepared statement (with `?` placeholders) ensures safety (avoiding SQL injection) and neatly maps the new data for Bob's record.

### 2. DELETE Statement

### **What It Is**

The **DELETE** statement removes one or more records from a table. You might use DELETE to remove outdated, irrelevant, or erroneous data from your dataset.

### **Basic Syntax**

The DELETE statement is straightforward:

```sql
DELETE FROM table_name
WHERE condition;
```

- **`table_name`**: The table from which you want to delete rows.
- **`WHERE` clause**: Specifies which records to delete. **Without a WHERE clause, every row in the table is removed,** effectively emptying the table.

### **Detailed Examples**

### **Example 1: Deleting a Specific Record**

Imagine you want to remove the record for a customer named "Charlie":

```sql
DELETE FROM customers
WHERE name = 'Charlie';
```

- **What’s happening:**
Only the rows where the name is "Charlie" will be deleted.

### **Example 2: Deleting with Multiple Conditions**

You can delete records that meet more than one criterion. For example, if you want to remove customers from a specific city who haven't been active:

```sql
DELETE FROM customers
WHERE city = 'Mumbai' AND last_active < '2024-01-01';
```

- **What’s happening:**
This ensures that only outdated records from Mumbai are removed.

### **Example 3: Deleting All Records (Use with Extreme Caution!)**

```sql
DELETE FROM customers;
```

- **Caution:**
Running this without a WHERE clause will delete every record in the `customers` table. Always verify that you really want to clear the whole table.

### **Using DELETE in a Practical Environment**

Let’s see how DELETE might be implemented in Python with SQLite:

```python
import sqlite3

# Connect to the database
conn = sqlite3.connect('example.db')
cursor = conn.cursor()

# Example: Delete a customer named "Charlie"
cursor.execute('''
DELETE FROM customers
WHERE name = ?
''', ('Charlie',))

conn.commit()
print("Record(s) deleted successfully!")
conn.close()
```

- **Explanation:**
The prepared statement deletes only the record(s) that match the criterion provided—securely handling the input and ensuring only the intended row(s) are removed.

### 3. Good Practices and Final Thoughts

- **Always Use a WHERE Clause:**
    
    Both UPDATE and DELETE can drastically change your dataset if used without a condition. It’s a good habit to do a SELECT first to verify which rows match your condition before executing the command.
    
- **Backup Your Data:**
    
    Before running mass updates or deletes on important data, ensure you have backups or use transactions where you can roll back if something goes wrong.
    
- **Testing:**
    
    When practicing these commands, especially in a learning or development environment, use a test database. This way, you can safely experiment without the risk of corrupting real data.
    
- **Transactions:**
    
    Remember that many RDBMS support transactions, which allow you to commit or rollback your changes. This can be invaluable when making multiple related changes.
    

---