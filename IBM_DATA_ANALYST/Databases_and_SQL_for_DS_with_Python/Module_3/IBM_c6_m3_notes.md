# IBM_c6_m3

## Before moving to module

I've uploaded a SalesDataset (csv format) into SQLite to perform the operations:

(Please select column names as first line while uploading)

**Initial Exploration:**

- **Verification:** Running `SELECT * FROM SalesDataset;`  quickly shows you that all the columns and rows have been loaded correctly.
- **Inspection:** Look at the column names, data types, and any unexpected values. This step helps you identify if there are any issues with missing data or misformatted values before you dive into more detailed queries.

**Refining the Results:**

The module likely covers how to extract meaningful insights by filtering and transforming your data. Some common techniques include:

- **Filtering Rows:**
Using the `WHERE` clause to focus on specific parts of your dataset. For example:
This gives you a clear view of a subset of your sales data.
    
    ```sql
    SELECT * FROM SalesDataset
    WHERE City = 'Miami'
    ```
    
- **Sorting:**
Using `ORDER BY` to arrange your data, such as by sale amount or date.
    
    ```sql
    SELECT * FROM SalesDataset
    ORDER BY amount DESC;
    ```
    
- **Aggregation:**
Using `GROUP BY` and aggregate functions like `SUM()`, `AVG()`, or `COUNT()` to summarize data for insights.
    
    ```sql
    SELECT state, COUNT(*) AS amount, SUM(profit) AS total_revenue
    FROM SalesDataset
    GROUP BY city;
    ```
    
- **Limiting Results:**
Often handy when the dataset is huge. For example:
    
    ```sql
    SELECT * FROM SalesDataset
    ORDER BY Profit DESC
    LIMIT 10;
    ```
    

---

## Using string patterns and ranges

SalesDataset table that has the following columns:

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

### 1. String Pattern Matching

**What It Is:**

SQL lets you filter textual data using string patterns, which is especially useful when you don’t need an exact match. The primary operator here is `LIKE`, and some databases (such as PostgreSQL) offer `ILIKE` for case-insensitive matching. In SQLite—and many others—`LIKE` typically behaves in a case-insensitive manner for ASCII text.

### Wildcards and Their Meaning

- **% (percent):**
    
    Matches zero or more characters.
    
    *Example:*
    
    ```sql
    WHERE CustomerName LIKE 'A%'
    ```
    
    Retrieves rows where the CustomerName starts with the letter “A” (followed by any number of characters).
    
- **_ (underscore):**
    
    Matches exactly one character.
    
    *Example:*
    
    ```sql
    WHERE City LIKE 'N_w%'
    ```
    
    Could match “New” or “Nor…”, depending on exact data—this pattern finds any City where the second letter is exactly one character after N, then followed by “w” and any other characters.
    

### Practical Examples Using SalesDataset

1. **Finding Customers by Name Pattern:**
    
    Suppose you want to list all orders for customers whose names start with "A":
    
    ```sql
    SELECT Order_Id, CustomerName, Order_date, Amount
    FROM SalesDataset
    WHERE CustomerName LIKE 'A%';
    ```
    
    *Explanation:*
    
    - The pattern `'A%'` means any customer name beginning with A.
2. **Filtering by Sub-category:**
    
    You might want to narrow down orders involving electronics, such as products with "Phone" in the sub-category.
    
    ```sql
    SELECT Order_Id, [Sub-category], Amount, Profit
    FROM SalesDataset
    WHERE [Sub-category] LIKE '%Phone%';
    ```
    
    *Explanation:*
    
    - The `%Phone%` pattern finds any sub-category that contains the word "Phone" anywhere in the string.
3. **Combining Multiple Pattern Matches:**
    
    Suppose you want to filter sales records where the PaymentMode is "Credit Card" and the State begins with the letter "N":
    
    ```sql
    SELECT Order_Id, CustomerName, State, PaymentMode, Order_date
    FROM SalesDataset
    WHERE PaymentMode = 'Credit Card'
      AND State LIKE 'N%';
    ```
    
    *Explanation:*
    
    - The condition on `State` ensures that only states beginning with "N" are returned (e.g., "New York", "New Jersey").

**Tips for String Patterns:**

- **Case Sensitivity:** If you need to ensure case-insensitive comparisons, consider using functions like `UPPER()` or `LOWER()`:
    
    ```sql
    SELECT Order_Id, CustomerName
    FROM SalesDataset
    WHERE UPPER(CustomerName) LIKE 'A%';
    ```
    
- **Regular Expressions:** Some databases provide regex support (`REGEXP`) for more complex matching. (SQLite can support regex through custom extensions.)

### 2. Range-Based Filtering

Range filtering is used when you want to select records that fall within a specific interval—common for numbers and dates, but also usable with strings that have an inherent order (like Year-Month formatted as `"YYYY-MM"`).

### The BETWEEN Operator

- **Usage:**`BETWEEN` is inclusive, meaning it includes both the start and end values.
    
    ```sql
    column BETWEEN value1 AND value2
    ```
    

### Practical Examples Using SalesDataset

1. **Filtering by Numeric Range (Amount):**
    
    Suppose you want to see orders with amounts between $500 and $1000:
    
    ```sql
    SELECT Order_Id, Amount, CustomerName, Order_date
    FROM SalesDataset
    WHERE Amount BETWEEN 500 AND 1000;
    ```
    
    *Explanation:*
    
    - This selects orders where the Amount is 500, 1000, or any value in between.
2. **Filtering by Date Range (Order_date):**
    
    To view sales made in January 2024:
    
    ```sql
    SELECT Order_Id, Order_date, Amount, Profit
    FROM SalesDataset
    WHERE Order_date BETWEEN '2024-01-01' AND '2024-01-31';
    ```
    
    *Explanation:*
    
    - The query retrieves orders within the defined date range.
3. **Filtering by String Range (Year-Month):**
    
    If `Year-Month` is stored as a string in the format `"YYYY-MM"`, you can also use a range to filter months. For example, to get data from March 2024 to May 2024:
    
    ```sql
    SELECT Order_Id, [Year-Month], Amount, Profit
    FROM SalesDataset
    WHERE [Year-Month] BETWEEN '2024-03' AND '2024-05';
    ```
    
    *Explanation:*
    
    - Because the dates are in lexicographical order as `"YYYY-MM"`, using BETWEEN works as expected.
4. **Combining String Patterns and Ranges:**
    
    You could also combine filtering techniques. For example, to find orders in which the CustomerName starts with “J” and the Amount falls within a specific range:
    
    ```sql
    SELECT Order_Id, CustomerName, Amount, Order_date
    FROM SalesDataset
    WHERE CustomerName LIKE 'J%'
      AND Amount BETWEEN 200 AND 800;
    ```
    
    *Explanation:*
    
    - This query returns orders that meet both the string pattern condition for the CustomerName and the numeric range condition for the Amount.

### Summary:

Using string patterns and ranges together allows you to refine your SQL queries significantly:

- **String Patterns:**
    
    Let you search for data that follows a specific pattern using wildcards. This is extremely helpful for textual data like names, categories, and sub-categories.
    
- **Range Filtering:**
    
    Gives you the power to narrow down numeric values and dates, ensuring you only look at the data that is relevant to your question.
    

---

## Sorting result sets

### 1. Why Sorting Is Important

- **Improved Readability:**
    
    A sorted dataset makes it easier to see trends, spot outliers, and quickly locate records of interest (e.g., the highest profit orders, the most recent transactions, or alphabetical customer lists).
    
- **Data Analysis:**
    
    Sorting helps in presenting data for reporting or visualization. For example, sorting sales by date can reveal seasonal trends, and sorting by profit can help you identify the most profitable categories.
    
- **Effective Pagination:**
    
    When you display results over multiple pages (e.g., in a web application), it’s crucial to have a consistent order.
    

### 2. Basic Syntax and Components

The core syntax for sorting in SQL is:

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column_name [ASC|DESC], another_column [ASC|DESC];
```

### Elements Explained

- **ORDER BY Clause:**
    
    This clause indicates which column(s) should be used to order the result set.
    
- **ASC (Ascending):**
    
    Sorts the data in increasing order. This is the default if no order is specified.
    
    *Example:*
    
    ```sql
    ORDER BY Order_date ASC;
    ```
    
    This sorts orders from the earliest to the latest date.
    
- **DESC (Descending):**
    
    Sorts the data in decreasing order.
    
    *Example:*
    
    ```sql
    ORDER BY Profit DESC;
    ```
    
    This sorts orders by profit so that the highest profit orders appear first.
    
- **Multiple Columns:**
    
    You can sort by more than one column. The sorting is applied left-to-right:
    
    ```sql
    ORDER BY State ASC, City ASC;
    ```
    
    This first sorts all records by State in ascending order. For rows with the same State, it then sorts by City in ascending order.
    

### 3. Examples Using SalesDataset

### Example 1: Sorting by Date

To see the most recent sales orders first:

```sql
SELECT Order_Id, Order_date, Amount, CustomerName
FROM SalesDataset
ORDER BY Order_date DESC;
```

*Explanation:*

- This query retrieves key columns and orders the results from latest to earliest order date.

### Example 2: Sorting by Profit

To identify the most profitable orders:

```sql
SELECT Order_Id, Profit, CustomerName, Category
FROM SalesDataset
ORDER BY Profit DESC;
```

*Explanation:*

- Orders are sorted in descending order by Profit, so the highest profit records appear at the top.

### Example 3: Sorting by Multiple Columns

Suppose you want to analyze orders within each state, then order them by the order amount in ascending order:

```sql
SELECT Order_Id, State, Amount, Order_date
FROM SalesDataset
ORDER BY State ASC, Amount ASC;
```

*Explanation:*

- This query first groups orders by State alphabetically, then within each state, orders are sorted by Amount.

### Example 4: Sorting on a Computed Column

You might sometimes want to sort by an expression. For instance, if you want to sort orders by profit margin (Profit divided by Amount):

```sql
SELECT Order_Id, Amount, Profit, CustomerName,
       (Profit * 1.0 / Amount) AS ProfitMargin
FROM SalesDataset
ORDER BY ProfitMargin DESC;
```

*Explanation:*

- Here, we compute a column alias called `ProfitMargin` and then sort the result set with the highest margin orders first.
- Multiplying by 1.0 ensures that the division returns a decimal result.

### 4. Advanced Sorting Considerations

### Sorting with Null Values

- SQL handles `NULL` values differently, depending on your RDBMS.
- You might need an explicit clause in some databases to specify how to order `NULL`s (e.g., `NULLS FIRST` or `NULLS LAST`).

### Case Sensitivity

- In some databases, sorting strings can be case-sensitive.
- You might want to convert text to all upper or lower case to ensure consistent ordering:
    
    ```sql
    SELECT Order_Id, CustomerName
    FROM SalesDataset
    ORDER BY UPPER(CustomerName) ASC;
    ```
    

### Collations

- Collation settings determine how strings are compared and sorted. This is useful in international applications or when dealing with accented characters.

---

## Grouping Result Sets

### 1. The Essence of GROUP BY

When you write a query with a GROUP BY, you’re instructing SQL to:

- **Divide the Result Set:**
    
    Partition the rows into groups based on one or more columns. For instance, grouping by the "Category" column creates one group for each distinct category.
    
- **Aggregate Data within Each Group:**
    
    Once rows are grouped, you can perform operations such as:
    
    - **Counting:** How many orders are in each category.
    - **Summing:** Total sales or profit for each group.
    - **Averaging:** The average order amount per group.

**Key Rule:**

All columns in your `SELECT` statement must either be included in the GROUP BY clause or be used with an aggregate function (unless your SQL dialect permits otherwise).

### 2. Using Aggregate Functions with GROUP BY

Some common aggregate functions used with GROUP BY include:

- **COUNT(*) or COUNT(column):**
Counts the number of rows or non-null values in a group.
- **SUM(column):**
Adds up all the values in a numeric column.
- **AVG(column):**
Calculates the average value.
- **MIN(column)/MAX(column):**
Gives the minimum or maximum value in a group.

### 3. Examples Using SalesDataset

### Example 1: Grouping by **Category**

To get a summary of orders by category—such as the total number of orders and the total sales amount—you can write:

```sql
SELECT
    Category,
    COUNT(Order_Id) AS TotalOrders,
    SUM(Amount) AS TotalSales
FROM SalesDataset
GROUP BY Category;
```

*Explanation:*

- **GROUP BY Category:** Groups the data along the Category column.
- **COUNT(Order_Id):** Counts the orders per category.
- **SUM(Amount):** Sums up the amount values for each category.

### Example 2: Grouping by **State**

You might want to see how the sales perform per state. For example:

```sql
SELECT
    State,
    COUNT(Order_Id) AS OrdersCount,
    SUM(Profit) AS TotalProfit
FROM SalesDataset
GROUP BY State;
```

*Explanation:*

- This query aggregates sales data for each state—counting the orders and summing the profit.

### Example 3: Grouping by **Year-Month** for Trend Analysis

If your Year-Month column is formatted as "YYYY-MM", you can analyze monthly performance:

```sql
SELECT
    [Year-Month],
    COUNT(Order_Id) AS OrdersCount,
    SUM(Amount) AS TotalSales
FROM SalesDataset
GROUP BY [Year-Month]
ORDER BY [Year-Month] ASC;
```

*Explanation:*

- **GROUP BY [Year-Month]:** Groups the data by the time period.
- **ORDER BY [Year-Month] ASC:** Sorts the results chronologically.

### Example 4: Grouping by Multiple Columns

You can group by more than one column. For instance, to see the combination of Category and PaymentMode:

```sql
SELECT
    Category,
    PaymentMode,
    COUNT(Order_Id) AS OrdersCount,
    AVG(Profit) AS AvgProfit
FROM SalesDataset
GROUP BY Category, PaymentMode;
```

*Explanation:*

- This groups the data first by Category and then by PaymentMode, allowing you to see how each combination performs.

### Example 5: Filtering Groups with HAVING

The **HAVING** clause is used to filter groups based on aggregate values. For example, to display only categories with more than 50 orders:

```sql
SELECT
    Category,
    COUNT(Order_Id) AS TotalOrders,
    SUM(Amount) AS TotalSales
FROM SalesDataset
GROUP BY Category
HAVING COUNT(Order_Id) > 50;
```

*Explanation:*

- **HAVING COUNT(Order_Id) > 50:** Filters out groups where the number of orders is 50 or fewer.

### 4. Why Grouping Matters

- **Efficient Summary:**
    
    Grouping turns a massive dataset into digestible summaries, making it easier to see trends and patterns.
    
- **Data Insights:**
    
    It helps answer key business questions such as:
    
    - Which category generates the most revenue?
    - How do sales vary by region or month?
    - What is the average profit per order by payment mode?
- **Foundation for Further Analysis:**
    
    The aggregated results often serve as inputs for dashboards or further predictive analysis.
    

---

## Built-in database functions

### 1. Aggregate Functions

Aggregate functions operate on sets of rows to return a single summary value. They’re particularly useful for generating reports or summarizing sales data.

- **COUNT(column)**
    
    Counts non-null values; use `COUNT(*)` to count all rows.
    
    *Example:*
    
    ```sql
    SELECT Category, COUNT(*) AS TotalOrders
    FROM SalesDataset
    GROUP BY Category;
    ```
    
    *This returns the total number of orders for each product category.*
    
- **SUM(column)**
    
    Adds up all numeric values.
    
    *Example:*
    
    ```sql
    SELECT Category, SUM(Amount) AS TotalSales
    FROM SalesDataset
    GROUP BY Category;
    ```
    
    *This query sums the order amounts per category.*
    
- **AVG(column)**
    
    Calculates the average value.
    
    *Example:*
    
    ```sql
    SELECT PaymentMode, AVG(Profit) AS AverageProfit
    FROM SalesDataset
    GROUP BY PaymentMode;
    ```
    
    *This computes the average profit for each payment mode.*
    
- **MIN(column)** and **MAX(column)**
    
    Return the smallest and largest values, respectively.
    
    *Example:*
    
    ```sql
    SELECT MIN(Amount) AS SmallestOrder, MAX(Amount) AS LargestOrder
    FROM SalesDataset;
    ```
    
    *This returns the smallest and largest amounts across all orders.*
    

### 2. String Functions

String functions allow you to manipulate text columns such as CustomerName, Category, or City.

- **UPPER() / LOWER()**
    
    Convert text to uppercase or lowercase.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, UPPER(CustomerName) AS CustomerName_Upper
    FROM SalesDataset;
    ```
    
    *Transforms customer names into uppercase.*
    
- **SUBSTR() / SUBSTRING()**
    
    Extracts a portion of a string. (SQLite uses `SUBSTR`.)
    
    *Example:*
    
    ```sql
    SELECT Order_Id, SUBSTR(CustomerName, 1, 3) AS NamePrefix
    FROM SalesDataset;
    ```
    
    *Extracts the first three characters of the customer name.*
    
- **LENGTH()**
    
    Returns the number of characters in a string.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, CustomerName, LENGTH(CustomerName) AS NameLength
    FROM SalesDataset;
    ```
    
    *Shows how many characters long each customer’s name is.*
    
- **CONCAT()** (or using `||` in SQLite)
    
    Concatenates two or more strings.
    
    *Example (SQLite style):*
    
    ```sql
    SELECT Order_Id, CustomerName || ' (' || City || ')' AS CustomerInfo
    FROM SalesDataset;
    ```
    
    *This combines customer names with their city, separated by parentheses.*
    

### 3. Date and Time Functions

Date functions help you manipulate dates and times in columns like Order_date or the Year-Month field.

- **DATE() and DATETIME()**
    
    Extract or format dates.
    
    *Example (SQLite):*
    
    ```sql
    SELECT Order_Id, DATE(Order_date) AS OrderDate
    FROM SalesDataset;
    ```
    
    *This will extract the date part (YYYY-MM-DD) from Order_date.*
    
- **strftime()** (SQLite specific)
    
    Allows advanced date and time formatting.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, strftime('%Y', Order_date) AS OrderYear
    FROM SalesDataset;
    ```
    
    *Extracts the year from the Order_date.*
    
- **CURRENT_DATE / CURRENT_TIMESTAMP**
    
    Returns the current date and date-time respectively.
    
    *Example:*
    
    ```sql
    SELECT CURRENT_DATE AS Today, CURRENT_TIMESTAMP AS Now;
    ```
    
    *Useful for comparing order dates or setting default values.*
    

### 4. Numeric Functions

Numeric functions work on numeric data like Amount, Profit, and Quantity.

- **ROUND()**
    
    Rounds a number to the specified number of decimal places.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, Amount, ROUND(Amount, 2) AS RoundedAmount
    FROM SalesDataset;
    ```
    
    *Rounds the Amount to two decimal places.*
    
- **ABS()**
    
    Returns the absolute value.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, Profit, ABS(Profit) AS AbsProfit
    FROM SalesDataset;
    ```
    
    *Ensures you capture profit magnitude regardless of sign (if negative values mean loss).*
    
- **CEILING() / FLOOR()**
    
    Ceiling returns the smallest integer greater than or equal to the number; floor returns the largest integer less than or equal to the number. (Not all databases natively support these; SQLite might require custom functions.)
    
    *Example (in systems that support them):*
    
    ```sql
    SELECT Order_Id, Amount, CEILING(Amount) AS CeilAmount, FLOOR(Amount) AS FloorAmount
    FROM SalesDataset;
    ```
    

### 5. Conditional and Conversion Functions

These functions help you handle nulls, perform conditional logic, or convert data types.

- **COALESCE()**
    
    Returns the first non-null value.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, COALESCE(Profit, 0) AS ProfitSafe
    FROM SalesDataset;
    ```
    
    *Ensures that if Profit is NULL, it defaults to zero.*
    
- **CASE WHEN ... THEN ... ELSE ... END**
    
    Lets you perform conditional logic inline.
    
    *Example:*
    
    ```sql
    SELECT Order_Id,
           CASE
               WHEN Profit >= 100 THEN 'High Profit'
               WHEN Profit BETWEEN 50 AND 99 THEN 'Medium Profit'
               ELSE 'Low Profit'
           END AS ProfitCategory
    FROM SalesDataset;
    ```
    
    *Categorizes each order based on its profit.*
    
- **CAST()** and **CONVERT()**
    
    Used for changing data types.
    
    *Example:*
    
    ```sql
    SELECT Order_Id, CAST(Amount AS TEXT) AS AmountText
    FROM SalesDataset;
    ```
    
    *Converts the numeric Amount into text for concatenation or formatting purposes.*
    

### Example

Imagine you want to generate a report summarizing orders by Year-Month with various details:

```sql
SELECT
    [Year-Month],
    COUNT(Order_Id) AS OrderCount,
    SUM(Amount) AS TotalSales,
    AVG(Profit) AS AvgProfit,
    ROUND(AVG(Profit), 2) AS AvgProfitRounded,
    MAX(Amount) AS HighestOrder,
    MIN(Amount) AS LowestOrder,
    UPPER(State) AS StateName  -- converting state names to uppercase for consistency
FROM SalesDataset
GROUP BY [Year-Month], UPPER(State)
ORDER BY [Year-Month] ASC;
```

**Explanation:**

- **Aggregation:** Using COUNT, SUM, AVG, MAX, and MIN to summarize sales per month.
- **Rounding and String Conversion:** Rounding the average profit and converting state names to uppercase.
- **Grouping:** The query groups by both Year-Month and the uppercase state name to break down the results.
- **Ordering:** Sorted chronologically by Year-Month.

---

## Sub-queries and Nested queries

### 1. What Are Sub-Queries and Nested Queries?

- **Sub-query:**
A sub-query (or inner query) is a query nested inside another query. The outer query uses the result returned by the sub-query.
- **Nested Query:**
This is another term for a sub-query, emphasizing that the query is "nested" inside a larger one.
- **Why They Matter:**
    - They let you break complex logic into simpler, manageable parts.
    - They allow filtering, aggregation, or transformation based on data that is not directly available in the main table.
    - They help in scenarios where you need to compare against aggregate values or perform conditional operations.

### 2. Types of Sub-Queries

### A. Non-Correlated Sub-Queries

- **Definition:**
These sub-queries run independently of the outer query. They are executed once and their result is used in the outer query.
- **Example Use Cases:**
You might use a non-correlated sub-query to fetch an aggregate value that the outer query then uses as a filter.

**Example:**

Find all orders in your SalesDataset where the order amount is above the average amount across all orders:

```sql
SELECT Order_Id, Amount, CustomerName
FROM SalesDataset
WHERE Amount > (SELECT AVG(Amount) FROM SalesDataset);
```

*Explanation:*

- The sub-query `(SELECT AVG(Amount) FROM SalesDataset)` computes the average amount.
- The outer query then selects orders whose Amount is greater than this average.

### B. Correlated Sub-Queries

- **Definition:**
These sub-queries reference columns from the outer query. They are evaluated once for each row processed by the outer query.
- **Example Use Cases:**
When you need to compare each row with a value calculated from related rows, or when filtering based on a dynamic condition.

**Example:**

Suppose you want to list orders along with a flag indicating whether the order’s amount is above the average amount for that specific category:

```sql
SELECT s.Order_Id, s.Amount, s.Category,
       CASE
           WHEN s.Amount > (
               SELECT AVG(Amount)
               FROM SalesDataset
               WHERE Category = s.Category
           )
           THEN 'Above Average'
           ELSE 'Below Average'
       END AS AmountFlag
FROM SalesDataset s;
```

*Explanation:*

- For each order (alias `s`) in the outer query, the sub-query calculates the average order amount for that order's category.
- The CASE statement then labels the order as 'Above Average' if its Amount exceeds the category average or 'Below Average' otherwise.

### 3. Practical Examples and Techniques

### Example 1: Using a Non-Correlated Sub-Query in the WHERE Clause

**Scenario:**

You want to see orders whose Amount is greater than the overall average, as shown earlier.

```sql
SELECT Order_Id, Amount, CustomerName
FROM SalesDataset
WHERE Amount > (SELECT AVG(Amount) FROM SalesDataset);
```

*Tip:*

This is a common pattern when you need a fixed aggregate value (like overall average sales) applied to every row.

### Example 2: Using a Correlated Sub-Query to Compare Group Averages

**Scenario:**

For each order, determine if its profit is higher than the average profit for orders from the same payment mode.

```sql
SELECT Order_Id, PaymentMode, Profit,
       CASE
           WHEN Profit > (
               SELECT AVG(Profit)
               FROM SalesDataset s2
               WHERE s2.PaymentMode = s1.PaymentMode
           )
           THEN 'Above Average'
           ELSE 'Below Average'
       END AS ProfitPerformance
FROM SalesDataset s1;
```

*Explanation:*

- For each row (aliased as `s1`), the sub-query calculates the average profit for that particular payment mode (using `s2.PaymentMode = s1.PaymentMode`).
- The outer query then categorizes each order based on whether its profit exceeds that average.

### Example 3: Sub-Query in the FROM Clause

Sub-queries (or derived tables) can also be used in the `FROM` clause. This allows you to work with temporary result sets as if they were tables.

**Scenario:**

You want to prepare a summary of sales per category in a sub-query and then filter or further sort it in an outer query.

```sql
SELECT Category, TotalSales, OrderCount
FROM (
    SELECT Category,
           SUM(Amount) AS TotalSales,
           COUNT(Order_Id) AS OrderCount
    FROM SalesDataset
    GROUP BY Category
) AS CategorySummary
WHERE TotalSales > 5000
ORDER BY TotalSales DESC;
```

*Explanation:*

- The inner query aggregates sales data by category.
- The outer query then filters those groups to include only categories with total sales above 5000 and orders them in descending order.

### 4. Best Practices and Considerations

- **Performance:**
Correlated sub-queries can be resource-intensive, as they execute for each row of the outer query. For large datasets, consider using JOINs or temporary tables if possible.
- **Readability:**
Break down complex queries into sub-queries to keep your logic clear. However, avoid nesting too many layers, which can make the query hard to read and maintain.
- **Indexes:**
Ensure proper indexing. Sub-queries that are used in filtering or in join conditions can benefit significantly from well-planned indexes on the columns referenced.

---

## Working with multiple tables

You can create multiple datasets, upload it to SQLite and work with them.

### 1. Why Work with Multiple Tables?

In a well-designed relational database, related information is split into different tables following normalization principles. For example, in a sales scenario:

- **SalesDataset:** May store order-related data (Order_Id, Amount, Profit, etc.).
- **Customers:** A separate table might contain customer details (Customer_Id, CustomerName, State, City, etc.).
- **Products:** Another table could list products with details like Product_Id, Category, Sub-category, etc.

**Advantages:**

- **Reduces Redundancy:** Each real-world entity is stored only once.
- **Improves Data Integrity:** Changes to a customer’s details or product information happen in only one place.
- **Optimizes Queries:** Smaller, focused tables can improve performance and make it easier to update data.

**Key Concepts:**

- **Primary Key:** Uniquely identifies records in a table.
- **Foreign Key:** Links records between tables by referencing the primary key in another table.
- **Data Relationships:**
    - *One-to-Many:* One customer can have many orders.
    - *Many-to-Many:* Products and orders often have a many-to-many relationship, which is resolved with join tables.

### 2. Types of SQL JOINs

To work with multiple tables, you typically use JOIN operations. These specify how records from two (or more) tables are combined:

### A. **INNER JOIN**

- **Definition:** Retrieves rows that have matching values in both tables.
- **When to Use:** When you want only the records that have a relationship in both tables.

**Example:**

Imagine a `Customers` table defined as:

- **Customers:** Customer_Id, CustomerName, State, City

And our **SalesDataset** has a CustomerName column that ideally corresponds to Customers.CustomerName (for demonstration purposes; in practice, you might use a unique Customer_Id). To see the orders along with customer's state:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Profit,
    s.Order_date,
    c.CustomerName,
    c.State
FROM SalesDataset s
INNER JOIN Customers c
    ON s.CustomerName = c.CustomerName;
```

*Explanation:*

Only orders with a matching customer record in the Customers table appear.

### B. **LEFT (OUTER) JOIN**

- **Definition:** Retrieves all rows from the left (first) table, and the matched rows from the right table. If there’s no match, the result is NULL on the right side.
- **When to Use:** To include all records from one table regardless of whether a corresponding row exists in the other table.

**Example:**

To list all orders (even if some orders don’t have customer details):

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Profit,
    s.Order_date,
    c.CustomerName,
    c.State
FROM SalesDataset s
LEFT JOIN Customers c
    ON s.CustomerName = c.CustomerName;
```

*Explanation:*

All orders from SalesDataset are returned; for orders where a matching customer isn’t found, the CustomerName and State fields will be NULL.

### C. **RIGHT (OUTER) JOIN and FULL OUTER JOIN**

- **RIGHT JOIN:** Returns all rows from the right table, and the matching rows from the left; not all database systems (like SQLite) support RIGHT JOIN directly.
- **FULL OUTER JOIN:** Returns rows when there is a match in one of the tables; that is, all rows from both tables with NULLs where there’s no match.

*Note:* For SQLite, which is common in online environments, RIGHT and FULL OUTER JOIN aren’t directly supported; you might mimic them with UNIONs or use another system that supports the syntax.

### D. **CROSS JOIN**

- **Definition:** Returns the Cartesian product of the two tables (i.e., every row in the first table combined with every row in the second table).
- **When to Use:** Rarely needed for typical relationships—but useful in generating combinations, such as reporting every possible pairing.

**Example:**

```sql
SELECT s.Order_Id, c.CustomerName
FROM SalesDataset s
CROSS JOIN Customers c;
```

*Explanation:*

Every order is paired with every customer.

### E. **Self-Join**

- **Definition:** A self-join is when a table is joined with itself. This is useful when you have hierarchical or recursive relationships.
- **When to Use:** For example, if you have a table of employees with a Manager_Id that references Employee_Id within the same table.

While our SalesDataset isn’t a typical candidate for a self-join, it’s a powerful technique for other scenarios.

### 3. Multiple Table Example with Hypothetical Related Tables

Imagine we have three tables now:

- **SalesDataset:** Order_Id, Amount, Profit, Order_date, CustomerName, [Year-Month], etc.
- **Customers:** Customer_Id, CustomerName, State, City
- **Products:** Product_Id, Category, Sub-category

### Example Query 1: Joining SalesDataset and Customers

To produce a report with orders and corresponding customer details:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Profit,
    s.Order_date,
    s.[Year-Month],
    c.CustomerName,
    c.State,
    c.City
FROM SalesDataset s
INNER JOIN Customers c
    ON s.CustomerName = c.CustomerName;
```

*Explanation:*

- This query uses an INNER JOIN to ensure only orders with matching customers are displayed.

### Example Query 2: Joining with Multiple Tables

Suppose you want to generate a detailed sales report that includes product information. Assume SalesDataset has a column Product_Id that matches Products.Product_Id:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Profit,
    s.Order_date,
    s.[Year-Month],
    c.CustomerName,
    c.State,
    p.Category,
    p.[Sub-category]
FROM SalesDataset s
INNER JOIN Customers c
    ON s.CustomerName = c.CustomerName
INNER JOIN Products p
    ON s.Product_Id = p.Product_Id;
```

*Explanation:*

- Here, two joins are used: one to connect sales to customers and another to connect sales to product details. This illustrates how you can build a rich, multi-table query.

### 4. Tips and Best Practices

- **Use Explicit JOIN Syntax:**
Always use `INNER JOIN`, `LEFT JOIN`, etc. This improves readability and clarity.
- **Aliases:**
Use table aliases (like `s`, `c`, `p`) to keep your queries short, especially when working with multiple tables.
- **Filtering After Joins:**
Apply your `WHERE` clause after your JOINs to filter the final result set.
- **Indexing:**
Ensure that the key fields used for joins (foreign keys and primary keys) are indexed. This greatly improves performance.
- **Check Nulls:**
Consider how NULL values should be handled, especially with outer joins.
- **Plan Your Schema:**
A good schema with properly defined relationships and constraints (using primary key and foreign key relationships) sets the stage for effective multi-table queries.

---

## Multiple tables - Implicit joins and Sub-queries

It is already defined and worked in examples above.

### 1. Implicit Joins

### **What They Are**

In an implicit join, you list multiple tables in the `FROM` clause separated by commas and define the relationship with a condition in the `WHERE` clause. For example, if you have a **SalesDataset** table and a **Customers** table, and they share a common column like `CustomerName`, you can join them implicitly.

### **Example: Implicit Join Between SalesDataset and Customers**

Assume we have these two tables with the following simplified columns:

- **SalesDataset:**
    - Order_Id
    - Amount
    - Profit
    - Order_date
    - CustomerName
    - … (other columns such as Category, Year-Month, etc.)
- **Customers:**
    - CustomerName
    - State
    - City

An implicit join to combine sales orders with customer information might look like this:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Order_date,
    s.CustomerName,
    c.State,
    c.City
FROM
    SalesDataset s,
    Customers c
WHERE
    s.CustomerName = c.CustomerName;
```

**Explanation:**

- The `FROM` clause lists both **SalesDataset** (aliased as *s*) and **Customers** (aliased as *c*).
- The `WHERE` clause defines the join condition: matching `CustomerName` in both tables.
- This query returns only the orders that have matching customer information.

### 2. Sub-Queries with Multiple Tables

### **Using Sub-Queries**

A sub-query (or nested query) sits inside a main (outer) query. When working with multiple tables, sub-queries can let you filter the outer query based on conditions computed from another table. You don't always need to join explicitly; sometimes, you check membership or aggregate values from another table.

### **Example 1: Filtering Sales Based on Customer State Using a Sub-Query**

Suppose you want to show orders for which the customer is located in a specific state (say, "California"). Instead of joining, you can rely on a sub-query to get the list of customer names in California:

```sql
SELECT
    Order_Id,
    Amount,
    Order_date,
    CustomerName
FROM
    SalesDataset
WHERE
    CustomerName IN (
        SELECT CustomerName
        FROM Customers
        WHERE State = 'California'
    );
```

**Explanation:**

- The sub-query `(SELECT CustomerName FROM Customers WHERE State = 'California')` retrieves all customers from California.
- The outer query selects orders from **SalesDataset** where the `CustomerName` appears in that list.
- This approach keeps the main query simpler when the join itself isn’t needed for additional columns.

### **Example 2: Correlated Sub-Query to Categorize Orders**

Now, consider you want to flag each order as "Above Average" if its Amount exceeds the average amount for that customer’s city. This requires a sub-query that is executed for each order row:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.CustomerName,
    s.Order_date,
    c.City,
    CASE
        WHEN s.Amount > (
            SELECT AVG(s2.Amount)
            FROM SalesDataset s2, Customers c2
            WHERE s2.CustomerName = c2.CustomerName
              AND c2.City = c.City
        )
        THEN 'Above Average'
        ELSE 'Below Average'
    END AS SalesPerformance
FROM
    SalesDataset s, Customers c
WHERE
    s.CustomerName = c.CustomerName;
```

**Explanation:**

- Here, the outer query uses an implicit join between **SalesDataset** (*s*) and **Customers** (*c*) matching on `CustomerName`.
- The correlated sub-query inside the `CASE` expression calculates the average order Amount for the city of the current order row (as referenced by `c.City`).
- Based on this average, the order is flagged as 'Above Average' or 'Below Average'.

### 3. Combining Implicit Joins and Sub-Queries

Sometimes, you might want to use both techniques in one query. For example, you may perform an implicit join to bring together related table columns and then use a sub-query to further filter or categorize the results.

### **Example: Detailed Order Performance Report**

Imagine you want a report that shows order details along with customer city and then flags orders that are above the total average sales of that city. Here’s how you might write it:

```sql
SELECT
    s.Order_Id,
    s.Amount,
    s.Order_date,
    s.CustomerName,
    c.City,
    -- Compare each order's amount against the city’s overall average
    CASE
        WHEN s.Amount > (
            SELECT AVG(s3.Amount)
            FROM SalesDataset s3, Customers c3
            WHERE s3.CustomerName = c3.CustomerName
              AND c3.City = c.City
        )
        THEN 'Above City Average'
        ELSE 'Below City Average'
    END AS PerformanceFlag
FROM
    SalesDataset s, Customers c
WHERE
    s.CustomerName = c.CustomerName;
```

**Explanation:**

- The implicit join (using the comma-separated syntax) links the **SalesDataset** with the **Customers** table on `CustomerName`.
- For every row, the correlated sub-query calculates the average Amount for that city.
- The `CASE` expression compares the current order’s Amount to this city average, providing a flag.
- The result is a detailed performance report that uses both techniques.

---