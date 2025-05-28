# IBM_c2_m4

## Working with real-world data

1. Go to Kaggle → Search “Sales data” (or any data you want).
2. Download it in .csv 
3. Open it in Excel → Data → Get data → Import from text/csv.
4. Now you’ve real-world data you can practise in excel.

I’ve uploaded the used data set in the practice folder.

---

## Intro to Data analysis using spreadsheets

### **1. Understanding Your Data Before Analysis**

Before diving into analysis, start by **exploring** the dataset.

### **✅ Steps to Review the Dataset in Excel on macOS:**

1️⃣ **Open Your Spreadsheet in Excel.**

2️⃣ **Check the column headers** (they define your dataset categories).

3️⃣ **Scroll through the rows** to understand data patterns and identify missing or incorrect values.

4️⃣ **Freeze the header row for easier navigation** (Go to **View → Freeze Panes → Freeze Top Row**).

5️⃣ **Enable filters:**

- Select the header row.
- Go to **Data → Filter** (or press **⌘ + Shift + L**).
- This will allow you to sort and filter data for easier analysis.

✅ **Real-World Example:**

If your dataset contains **"Product Name," "Sales Amount," "Date," and "Region,"** filtering by **Region** helps you analyze regional sales trends.

---

### **2. Sorting & Filtering Data for Quick Insights**

Sorting and filtering help you focus on relevant sections of your dataset.

### **✅ Sorting Your Data**

1️⃣ Click **any cell in the column** you want to sort (e.g., "Sales Amount").

2️⃣ Go to **Data → Sort**.

3️⃣ Choose **Ascending** (lowest to highest) or **Descending** (highest to lowest).

4️⃣ Click **OK**—your data is now sorted!

### **✅ Filtering for Specific Data**

1️⃣ Click on the **filter dropdown** in the column header → Profit.

2️⃣ Select the values you want to see (Change the choose one to greater than and enter 1500).

- So you see data whose profit are only above $1500

3️⃣ Click **OK**, and Excel will hide the irrelevant rows.

✅ **Real-World Example:**

Filtering **"Profit" > 1500** helps you identify **high-value transactions**.

---

### **3. Using Pivot Tables for Quick Summarization**

Pivot tables allow you to **aggregate and summarize large datasets** effortlessly.

### **✅ Creating a Pivot Table (MacBook Steps)**

1️⃣ Select any **cell in your dataset**.

2️⃣ Go to **Insert → Pivot Table**.

3️⃣ Choose **New Worksheet** for the table placement → Click OK

4️⃣ Drag fields to the Pivot Table **rows, columns, values, and filters**:

- Rows → Drag the column you want to group by (eg: customer name, profit)
    - Drag **"Customer Name"** to Rows.
- Columns → Splits data across columns
- Values → Drag a numeric field → excel auto-summarizes.
    - Drag **"Profit"** to Values (Excel will automatically sum the values).
- Filters → Drag a field here to filter the entire table.

5️⃣ Customize with filters and sorting to refine insights.

✅ **Real-World Example:**

A pivot table summarizing **total sales per product** helps identify **top-selling items**.

**Go back to your original worksheet:**

- Look at the bottom of the worksheet.
- You’ll find all your opened sheets here.
- Switch to your worksheet.

---

### **4. Creating Charts & Visualizations**

Charts help turn raw numbers into **easy-to-understand insights**.

### **✅ Steps to Create a Sales Trend Chart**

1️⃣ Select your **sales data range** (e.g., "Order Date" & "Amount").

- Use cmd to select non-adjacent multiple columns.
- Cmd + shift + downarrow (selects one column)
    - Don’t leave cmd button (leave other two) → select next column
    - Anyway cmd is pressed → select shift + down-arrow again.
    - Two desired non adjacent columns are selected.
- If dataset is too large → filter it, then do the charts.

2️⃣ Go to **Insert → Charts** and choose **a Line Chart**.

3️⃣ Customize the chart using **Chart Design** options.

4️⃣ Add **trendlines** (Click on the chart → Select Trendline).

✅ **Real-World Example:**

A sales trend chart shows **seasonal fluctuations**, helping businesses optimize inventory.

---

## Useful functions for data analysis

**How and where to use functions:**

1. Profit column already exits.
2. Go to the bottom or select a new cell anywhere (empty cell)
3. Type the functions and press enter!

Eg:

- You have data from A-L
- Go to M1 column and apply any formula → =IF(C2>100, "High Profit", "Low Profit") → Enter
- Applies to all rows automatically.

### **1. Statistical & Summarization Functions**

These functions help calculate totals, averages, and other key metrics.

✔ **SUM()** → Adds values in a range.

```
=SUM(B2:B1000)   → (Total Sales Amount)
```

✔ **AVERAGE()** → Computes the mean of a range.

```
=AVERAGE(C2:C1000)   → (Average Profit)
```

✔ **COUNT()** → Counts numeric values.

```
=COUNT(D2:D1000)   → (Total Orders Processed)
```

✔ **MAX() / MIN()** → Finds the highest or lowest value.

```
=MAX(B2:B1000)   → (Highest Sale Amount)
=MIN(B2:B1000)   → (Lowest Sale Amount)
```

✅ **Use Case:**

Quickly determine **total revenue, average profit, and number of orders** in your dataset.

### **2. Conditional & Logical Functions**

These functions help classify and filter data dynamically.

✔ **IF()** → Returns different results based on conditions.

```
=IF(C2>100, "High Profit", "Low Profit")
Apply in M1 -> Enter -> applies to all rows automatically.
```

✔ **IFS()** → Handles multiple conditions.

```
=IFS(C2>500, "Excellent", C2>100, "Good", TRUE, "Average")
```

✔ **AND() / OR()** → Checks multiple conditions.

```
=AND(B2>500, D2>10)   → (True if high-value order)
=OR(E2="Electronics", E2="Furniture")   → (True if key categories)
```

✅ **Use Case:**

Classify **sales as high or low profit**, filter **key categories**, or identify **bulk orders**.

### **3. Lookup & Reference Functions**

These functions help retrieve data dynamically.

✔ **VLOOKUP()** → Finds a value in a table (useful for matching data).

```
=VLOOKUP("Laptop", E2:F1000, 2, FALSE)
```

✔ **XLOOKUP()** → More flexible lookup (for latest Excel versions).

```
=XLOOKUP("Laptop", E2:E1000, F2:F1000)
```

✔ **MATCH()** → Finds the position of a value in a range.
✔ **INDEX()** → Retrieves the value at a specific row/column.

✅ **Use Case:**

Search for **customer orders**, **product details**, or **specific sales records**.

### **4. Date & Time Functions**

Analyzing trends based on **Order Date** and **Year-Month**.

✔ **YEAR() / MONTH() / DAY()** → Extracts specific parts of the date.

```
=YEAR(G2)   → (Extracts Order Year)
=MONTH(G2)  → (Extracts Order Month)
```

✔ **TEXT()** → Converts dates into a readable format.

```
=TEXT(G2, "MMM YYYY")   → (Displays as "May 2025")
```

✔ **DATEDIF()** → Calculates differences between dates.

```
=DATEDIF(G2, TODAY(), "D")   → (Days since order)
```

✅ **Use Case:**

Analyze **monthly or yearly trends** and check **time gaps between orders**.

### **5. Data Cleaning & Transformation**

How and where to use it?

- Go to new column → M1
- Enter the formula → =TRIM(I2) → Enter → applies to all → new column is created
- Copy it → select the original column → paste specials → values
- Delete the helper column.

✔ **TRIM()** → Removes extra spaces.
✔ **CLEAN()** → Removes unwanted characters.
✔ **PROPER()** → Formats text correctly.
✔ **TEXT-TO-COLUMNS** → Splits combined data into separate columns.

✅ **Use Case:**

Standardize **customer names, product categories, and payment modes**.

**How to move to top row and bottom row immediately:**

- You can type A2 on the top left and press enter (if you’ve frozen top row)
- cmd + down arrow → works even when you’ve frozen top row!
- Unfreeze it:
    - cmd + down arrow
    - cmd + up arrow

---

## VLOOKUP, HLOOKUP, COUNTIFS, SUMIFS, XLOOKUP

### **1️⃣ VLOOKUP: Vertical Lookup for Searching Data**

**Use Case:** Find a **customer's order details** or locate a **product price** from your dataset.

### **✅ How to Use VLOOKUP**

```
=VLOOKUP(lookup_value, table_array, col_index_number, [range_lookup])
```

✔ `lookup_value` → The value you want to find.

✔ `table_array` → The data range where the lookup happens.

✔ `col_index_number` → Column number where the matching value should be returned.

✔ `[range_lookup]` → `FALSE` for an exact match, `TRUE` for approximate.

### **MacBook Steps for VLOOKUP:**

1️⃣ Select any empty cell where you want the result.

2️⃣ Type:

```
=VLOOKUP("Laptops", F2:G1000, 2, FALSE)
```

(This searches for `"Laptops"` in **Column E** and returns the value from **Column G**.)

3️⃣ Press **Enter**, and Excel will display the result.

✅ **Example Use:**

Find the **payment mode** used for a specific **Order ID**.

### **2️⃣ HLOOKUP: Horizontal Lookup for Finding Data in Rows**

**Use Case:** Retrieve **monthly total sales** from a row-based dataset.

### **✅ How to Use HLOOKUP**

```
=HLOOKUP(lookup_value, table_array, row_index_number, [range_lookup])
```

✔ Works **like VLOOKUP**, but searches **horizontally** in a row instead of a column.

### **MacBook Steps for HLOOKUP:**

1️⃣ Click any empty cell.

2️⃣ Type:

```
=HLOOKUP("May", A1:M2, 2, FALSE)
```

(This searches for `"May"` in Row **A1:M1** and returns the value from Row **2**.)

3️⃣ Press **Enter**, and Excel will return the sales for May.

✅ **Example Use:**

Find **total profit for a given month** from a row-based dataset.

### **3️⃣ COUNTIFS: Counting Data That Meets Multiple Conditions**

**Use Case:** Count the number of **orders above $500** from a specific **category**.

### **✅ How to Use COUNTIFS**

```
=COUNTIFS(criteria_range1, criteria1, criteria_range2, criteria2)
```

✔ **Supports multiple conditions** (unlike `COUNTIF`, which allows only one).

### **MacBook Steps for COUNTIFS:**

1️⃣ Click an empty cell.

2️⃣ Type:

```
=COUNTIFS(B2:B1000, ">500", E2:E1000, "Electronics")
```

(This counts the number of orders where **Amount > 500** and **Category = Electronics**.)

3️⃣ Press **Enter**, and Excel will display the count.

✅ **Example Use:**

Find the number of **high-value transactions** per product category.

### **4️⃣ SUMIFS: Summing Data That Meets Multiple Conditions**

**Use Case:** Calculate the **total profit** for **Furniture** sales.

### **✅ How to Use SUMIFS**

```
=SUMIFS(sum_range, criteria_range1, criteria1, criteria_range2, criteria2)
```

✔ Adds up values **only** when multiple conditions are met.

### **MacBook Steps for SUMIFS:**

1️⃣ Click an empty cell.

2️⃣ Type:

```
=SUMIFS(C2:C1000, E2:E1000, "Furniture")
```

(This sums **Profit (Column C)** only for rows where **Category (Column E) = Furniture**.)

3️⃣ Press **Enter**, and Excel will display the total profit.

✅ **Example Use:**

Calculate total revenue for **orders above $500** in a specific **state**.

### **5️⃣ XLOOKUP: A More Advanced Lookup Function (Better Than VLOOKUP)**

**Use Case:** Find a **customer's city** based on their **Order ID**.

### **✅ How to Use XLOOKUP**

```
=XLOOKUP(lookup_value, lookup_array, return_array, [if_not_found], [match_mode], [search_mode])
```

✔ **More flexible than VLOOKUP & HLOOKUP** (works in any direction).

✔ **Can return an exact match or closest value**.

✔ **Supports an "If Not Found" option** to avoid errors.

### **MacBook Steps for XLOOKUP:**

1️⃣ Click an empty cell.

2️⃣ Type:

```
=XLOOKUP(A2, A2:A1000, K2:K1000, "Not Found")
```

(This searches **Order ID (A2)** in Column **A** and returns the matching **City (Column K)**.)

3️⃣ Press **Enter**, and Excel will display the city.

✅ **Example Use:**

Retrieve a customer’s **payment mode** based on **Order ID**.

---

## Pivot tables

A **Pivot Table** is one of Excel’s most powerful tools for **summarizing, analyzing, and exploring large datasets quickly**. 

Instead of manually sorting and filtering, a pivot table **automatically organizes data** into meaningful summaries based on categories, totals, averages, or comparisons.

✔ **Think of it like a dynamic report generator**—you can **drag and drop columns** to rearrange your view instantly.

### **Why Do We Use Pivot Tables?**

Pivot tables solve common challenges in data analysis, making it easier to **extract insights** from raw datasets.

### **Key Benefits:**

✔ **Summarizes Large Data Efficiently:** Quickly calculates totals, averages, and comparisons.

✔ **Dynamic Data Exploration:** Rearrange categories without needing new formulas.

✔ **Automatic Grouping & Filtering:** Instantly drill down into specific segments.

✔ **Data Visualization:** Works seamlessly with Pivot Charts for quick insights.

✅ **Example:**

If your **sales dataset** has 1000 rows, a pivot table can **instantly summarize total sales by product, region, or payment mode**, helping you spot top-performing areas.

### **How Pivot Tables Work in Excel?**

✔ **Rows:** The categories for grouping (e.g., Product Names, Months).

✔ **Values:** The calculations (e.g., Total Sales, Average Profit).

✔ **Filters:** Allow dynamic filtering of specific subsets (e.g., show only 2025 sales).

✔ **Columns:** Organize data into side-by-side comparisons.

✅ **Example Use Cases With Your Kaggle Sales Data:**

✔ **Total Sales by Category** → Summarize `"Sales Amount"` based on `"Product Category"`.

✔ **Top 5 States with Highest Profits** → Rank `"State"` by `"Profit"`.

✔ **Monthly Sales Trends** → Group `"Order Date"` by `"Year-Month"`.

---

## Pivot table features

### **1️⃣ Dynamic Data Summarization**

Pivot tables let you group and summarize large datasets without manually sorting or filtering.

✔ **Summarize Sales by Category:**

- Drag **"Category"** to Rows.
- Drag **"Sales Amount"** to Values → Excel automatically totals sales per category.

✔ **Summarize Profits by State:**

- Drag **"State"** to Rows.
- Drag **"Profit"** to Values → View total profit per state instantly.

✅ **Use Case:**

Get a quick overview of **which product categories or regions generate the most revenue**.

### **2️⃣ Auto-Filtering & Grouping**

Pivot tables allow dynamic filtering for **instant insights**.

✔ **Enable Filters:**

- Click **Pivot Table → Filter dropdown** → Select specific regions or products.
- Example: Filter **only sales above $500**.

✔ **Group Data Automatically:**

- Right-click a **date column** → Select **Group** → Choose **Months or Years**.
- Example: Group `"Order Date"` into **Monthly trends**.

✅ **Use Case:**

Quickly view **monthly sales**, filter **top-performing categories**, or analyze **profit trends per region**.

### **3️⃣ Custom Calculations (Calculated Fields)**

Pivot tables allow **custom formulas within summaries**, eliminating the need for manual calculations.

✔ **Create a Profit Percentage Metric:**

- Click **Pivot Table → Analyze → Fields, Items & Sets → Calculated Field**.
- Enter:
    
    ```
    =(Profit / Sales Amount) * 100
    ```
    
- Now, see **profit margins automatically**.

✅ **Use Case:**

Instantly compute **profit percentages** per category or state.

### **4️⃣ Sorting & Ranking**

✔ **Sort Data Automatically:**

- Click **Values dropdown** → Choose **Sort Largest to Smallest** (e.g., highest sales first).

✔ **Find Top 5 Products:**

- Click **Filter → Value Filters → Top 5** → View **only top-selling items**.

✅ **Use Case:**

Rank **top-performing products or customers based on revenue**.

### **5️⃣ Interactive Pivot Charts**

Pivot tables work seamlessly with **Pivot Charts** for dynamic visualization.

✔ **Steps to Insert a Pivot Chart:**

1️⃣ Click **Pivot Table → Pivot Chart**.

2️⃣ Select **Bar, Line, or Pie Chart**.

3️⃣ Modify filters → Charts update **instantly**.

✅ **Use Case:**

Visualize **monthly sales trends** or **regional profit comparisons**.

### **6️⃣ Hands-On Exercise With the Sales Dataset**

Try these **MacBook-specific** steps:

✔ **Summarize total sales by category.**

✔ **Group order dates by months for trend analysis.**

✔ **Calculate profit percentage per region.**

✔ **Sort & filter the top 10 profitable products.**

✔ **Create a Pivot Chart for visual insights.**

For your dataset → Do this:

- Drag customer name into rows
- Order date into columns
- Profits / amounts into Values

And observe the table created!

---

## **Slicers, Filters, and Timelines in Pivot Tables**

### **1️⃣ Filters: Refining Pivot Table Data**

Filters allow you to **display only the data you need**, instead of viewing the entire dataset.

### **✅ How to Apply Pivot Table Filters (MacBook Steps)**

1️⃣ Click **inside the Pivot Table** to activate the PivotTable Fields panel.

2️⃣ Drag any field (e.g., `"State"`) into the **Filters section**.

3️⃣ Click the **dropdown arrow** next to the filter in the Pivot Table.

4️⃣ Select specific items (e.g., filter to show only `"California"` sales).

5️⃣ Click **OK**, and the table updates instantly.

✅ **Use Case:**

Filter the **Pivot Table to display sales only from 2025** or limit analysis to a **specific product category**.

### **2️⃣ Slicers: Interactive Filtering with Buttons**

Slicers provide **visual buttons** to filter Pivot Table data **instantly**, making them more user-friendly than standard filters.

### **✅ How to Insert Slicers in Your Pivot Table**

1️⃣ Click **inside the Pivot Table**.

2️⃣ Go to **Pivot Table Analyze → Insert Slicer**.

3️⃣ Select the field you want to filter by (e.g., `"Category"` or `"State"`).

4️⃣ Click **OK**, and Excel will create a slicer with clickable buttons.

5️⃣ Click on a button (e.g., `"Electronics"`) to instantly filter your table.

✅ **Use Case:**

View **sales trends per category** by clicking different slicer buttons instead of using dropdown filters.

### **3️⃣ Timelines: Filtering Data by Date**

Timelines are slicers designed for **date-based filtering**—perfect for analyzing **monthly or yearly sales trends**.

### **✅ How to Use Timelines in Pivot Tables**

1️⃣ Click **inside the Pivot Table**.

2️⃣ Go to **Pivot Table Analyze → Insert Timeline**.

3️⃣ Select the **"Order Date"** field.

4️⃣ Click **OK**, and Excel creates an interactive timeline slider.

5️⃣ Drag the slider to **filter data by months, quarters, or years**.

✅ **Use Case:**

Track **monthly revenue trends** or **compare quarterly profit.**

---