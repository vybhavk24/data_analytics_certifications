# IBM_c2_m2

## Viewing, editing and entering data

### 1. **Viewing Data Efficiently**

When dealing with large datasets, knowing how to navigate and view data quickly is essential.

### **Key Techniques:**

- **Scrolling & Zooming:**
    - Use the trackpad or scroll bar to navigate through rows and columns.
    - Zoom in/out using **⌘ + plus (`+`) or minus ()** for better readability.
- **Freeze Panes (Keeping Headers Visible):**
    
    If you have a large dataset with column headers, keeping them visible while scrolling is crucial.
    
    - Go to **View** → **Freeze Panes** → **Freeze Top Row** (keeps the header visible as you scroll).
    - **Use Case:** When analyzing monthly sales, keeping column names visible prevents confusion.
        - Select the row below and freeze it → It freezes the above row.
- **Search and Find Data:**
    - Press **⌘ + F** to open the **Find** tool.
    - Type a keyword (e.g., "John") to locate specific entries quickly.
    - Use **⌘ + H** to **Replace** values, ideal for bulk updates.

### 2. **Entering Data into Cells**

Data entry is the first step in working with spreadsheets. Whether typing manually or importing from external sources, accuracy is key.

### **Basic Data Entry:**

1. Click on the desired cell and start typing.
2. Press **Enter** to move to the cell below or **Tab** to move to the right.
3. To enter numbers as text (e.g., a phone number starting with `0`), prefix them with an apostrophe (`'0123456789`).

### **Bulk Data Entry Techniques:**

- **Autofill:**
    - Enter data in one cell, then drag the **fill handle** (bottom-right corner of the cell) to populate adjacent cells.
    - Example: Type "Monday" in A1, drag down to automatically fill "Tuesday," "Wednesday," etc.
- **Using Lists for Quick Entry:**
    - If you're entering repeated categories (e.g., "Electronics," "Clothing"), use **Excel’s Data Validation** to create a dropdown list for faster input.

**Mac Shortcut for Fast Data Entry:**

- **Ctrl + Shift + " (quotation mark)** → Copies value from the cell above.

### 3. **Editing Data in Excel**

Once data is entered, modifying it efficiently is crucial.

### **Editing Techniques:**

- **Direct Editing:**
    - Double-click a cell to edit its content directly.
    - Alternatively, click the cell and modify text in the **Formula Bar**.
- **Replacing & Clearing Data:**
    - **⌘ + F** → Find & Replace values across the worksheet.
    - Select cells and press **Delete** to erase content while keeping formatting intact.
- **Batch Editing with Flash Fill (Smart Auto-Correction):**
    - Suppose you have a column of names like "john doe" but need them properly capitalized.
    - Type "John Doe" in the next column, press **Enter**, then use **⌘ + E** (Flash Fill) to auto-correct the entire list.

### 4. **Hands-On Exercise to try on MacBook Air**

Practice viewing, entering, and editing data with this exercise:

1. **Open Excel and Create a Simple Table:**
    - Column A: `Name`
    - Column B: `Age`
    - Column C: `Department`
    - Fill in a few rows with sample data.
2. **Try These Editing Techniques:**
    - Change a name using the **Formula Bar**.
    - Use **Find & Replace (⌘ + H)** to update a department name.
    - Use **Flash Fill (⌘ + E)** to fix inconsistent capitalization.
    - Apply **Freeze Panes** to keep headers visible.
3. **Experiment with Viewing Tools:**
    - Zoom in and out (**⌘ + `+` /** ).
    - Sort data by `Age` (**Home → Sort & Filter → Sort Ascending**).
    - Search for a specific entry using **⌘ + F**.

---

## **Copying, filling, and formatting cells and data**

### **1. Copying and Pasting Data**

Copying and pasting are fundamental actions that allow you to duplicate or move data within Excel.

### **Basic Copy & Paste:**

- **Copy:** Select a cell or range, press **⌘ + C**.
- **Paste:** Click the destination cell and press **⌘ + V**.
- **Cut & Paste:** Press **⌘ + X** to remove and relocate data instead of copying.
- **Paste Special:**
    - Sometimes, you don’t want to paste everything—maybe just values, formulas, or formatting.
    - Select a cell → **⌘ + Control + V** → Choose options like **Values**, **Formats**, or **Formulas**.

✅ **Real-World Example:**

Imagine you're analyzing monthly sales data and need to copy totals from one sheet to another. Instead of re-entering the figures manually, copying and pasting ensures accuracy and saves time.

### **2. Filling Cells with Data**

Excel provides powerful ways to quickly extend data across multiple rows or columns.

### **Autofill:**

Autofill intelligently fills a pattern based on the selected cells.

- Enter a value in a cell (e.g., "Monday" in A1).
- Click on the fill handle (small square at the cell’s bottom-right corner).
- Drag down or across to fill the series (`Monday → Tuesday → Wednesday`...).

### **Fill Series for Numbers:**

- Enter `1` in A1, `2` in A2.
- Select both, drag the fill handle down—the sequence continues (`3, 4, 5...`).

### **Flash Fill (Quick Pattern Recognition):**

- If Excel detects a pattern (e.g., separating first names from full names), use **⌘ + E** to auto-fill an entire column.

✅ **Real-World Example:**

A marketing analyst might use Autofill to extend a series of promotional discounts across several months.

### **3. Formatting Data for Better Readability**

Formatting makes your spreadsheet easier to read and visually appealing.

### **Essential Formatting Tools:**

- **Bold, Italic, Underline:**
    - **⌘ + B** (Bold) | **⌘ + I** (Italic) | **⌘ + U** (Underline).
- **Cell Colors:**
    - Select cells → Click **Fill Color** (paint bucket icon in the toolbar).
- **Text Alignment:**
    - Use **⌘ + Option + Left/Right/Center Align** to adjust positioning.
- **Number Formatting:**
    - Highlight a range → Press **⌘ + 1** → Select formats (Currency, Percentage, etc.)
    - Select any cell (range) → Right click → Format cells → select any option → And whenever you enter a number → it converts into that (eg: % or decimal etc)
- **Borders:**
    - Click **Borders** in the toolbar to define cell outlines.

✅ **Real-World Example:**

A financial analyst preparing a report might use currency formatting (`$`), conditional formatting (highlighting values above a target threshold), and clear column headers to ensure clarity.

### **4. Hands-On Practice on MacBook Air**

1. **Create a Small Dataset:**
    - Column A: `Employee Name`
    - Column B: `Department`
    - Column C: `Salary`
2. **Copy and Paste Data:**
    - Copy one row and paste it below.
    - Use **Paste Special** to paste only values.
3. **Use Autofill:**
    - Type "Sales" in B2, drag down to fill the same department in multiple rows.
4. **Apply Formatting:**
    - Bold column headers.
    - Format `Salary` as **Currency**.
    - Add **Borders** to improve readability.

---

## Intro to formulas

You can get these in the formula tab on your worksheet.

### **1. What Is a Formula in Excel?**

A formula in Excel is an **expression** that performs calculations based on values in cells. Every formula starts with an **equal sign (`=`)**.

### **Example:**

If you type the following formula into a cell:

```
=A1 + B1
```

Excel will add the values in cells A1 and B1 and display the result.

**Formula Anatomy:**

- `=` → Signals that you’re entering a formula.
- `A1 + B1` → The operation you want to perform.
- `Enter` → Executes the formula.

### **2. Basic Mathematical Operators**

Excel allows you to perform simple and complex mathematical operations using formulas.

### **Essential Operators:**

| Operator | Meaning | Example (`=A1`) |
| --- | --- | --- |
| `+` | Addition | `=A1 + B1` |
| `-` | Subtraction | `=A1 - B1` |
| `*` | Multiplication | `=A1 * B1` |
| `/` | Division | `=A1 / B1` |
| `^` | Exponentiation | `=A1 ^ 2` (Squares A1) |

✅ **Real-World Example:**

Imagine tracking monthly expenses. If `A1` contains rent cost and `B1` contains utilities, `=A1 + B1` gives the **total cost**, helping with budgeting.

### **3. Using Cell References**

Instead of hardcoding numbers, Excel formulas reference **cells**, making calculations **dynamic**.

### **Types of Cell References:**

- **Relative Reference (`A1`)**: Adjusts dynamically when copied.
- **Absolute Reference (`$A$1`)**: Stays fixed when copied.
- **Mixed Reference (`A$1` or `$A1`)**: Partially locked reference.

✅ **Example Exercise:**

1. Type a value in **A1** and another in **B1**.
2. Enter `=A1 + B1` in **C1**.
3. Copy the formula downwards—**notice how Excel adjusts it**.

### **4. Common Excel Functions**

Functions are **pre-built formulas** that simplify common tasks.

### **Must-Know Functions:**

| Function | Purpose | Example |
| --- | --- | --- |
| `SUM()` | Adds a range | `=SUM(A1:A5)` |
| `AVERAGE()` | Finds mean | `=AVERAGE(A1:A5)` |
| `MAX()` | Finds max value | `=MAX(A1:A5)` |
| `MIN()` | Finds min value | `=MIN(A1:A5)` |

✅ **Example:**

Calculate **total sales** for a month using `=SUM(B2:B31)`, saving time compared to manual addition.

### **5. Hands-On Exercise on MacBook Air**

1. **Create a small dataset:**
    - Column A: `Sales`
    - Column B: `Cost`
    - Column C: `Profit`
2. **Enter values into `A2:A6` and `B2:B6`.**
3. **In `C2`, enter `=A2 - B2`**, then **drag down** to apply the formula across rows.

You’ll see profit values update dynamically—a powerful feature for analytics!

---

## Intro to functions

### **1. What Is a Function in Excel?**

A function is a predefined formula designed to perform a specific calculation based on inputs (called **arguments**). Instead of manually writing a long formula, you can use functions to simplify the process.

### **Basic Structure of a Function:**

Every function follows a consistent format:

```
=FUNCTION_NAME(argument1, argument2, ...)
```

For example:

```
=SUM(A1:A10)
```

This function adds up all the values in **A1 to A10**.

✅ **Why Use Functions?**

- Speeds up data processing
- Reduces manual errors
- Makes calculations dynamic and scalable

### **2. Categories of Functions**

Excel functions fall into different categories, each serving a unique purpose.

### **1️⃣ Mathematical & Statistical Functions**

Used for numerical calculations.

| Function | Purpose | Example |
| --- | --- | --- |
| `SUM()` | Adds numbers | `=SUM(A1:A10)` |
| `AVERAGE()` | Computes mean | `=AVERAGE(A1:A10)` |
| `MAX()` | Returns highest value | `=MAX(A1:A10)` |
| `MIN()` | Returns lowest value | `=MIN(A1:A10)` |
| `COUNT()` | Counts numeric values | `=COUNT(A1:A10)` |

✅ **Use Case:** A financial analyst calculating total revenue or average monthly expenses.

### **2️⃣ Logical Functions**

Used to make decisions based on conditions.

| Function | Purpose | Example |
| --- | --- | --- |
| `IF()` | Returns different values based on a condition | `=IF(A1>50, "Pass", "Fail")` |
| `AND()` | Checks if multiple conditions are **true** | `=AND(A1>50, B1<100)` |
| `OR()` | Checks if at least one condition is **true** | `=OR(A1>50, B1<100)` |

✅ **Use Case:** A business analyst determining if sales targets have been met (`IF sales > target → "Achieved", else → "Pending"`).

### **3️⃣ Text Functions**

Used to manipulate text and clean data.

| Function | Purpose | Example |
| --- | --- | --- |
| `LEN()` | Counts number of characters in a string | `=LEN(A1)` |
| `LEFT()` | Extracts part of a text string (from left) | `=LEFT(A1, 3)` |
| `RIGHT()` | Extracts part of a text string (from right) | `=RIGHT(A1, 5)` |
| `CONCAT()` | Joins multiple text strings together | `=CONCAT(A1, B1)` |

✅ **Use Case:** A data analyst cleaning messy datasets where names, product codes, or descriptions need standardization.

### **4️⃣ Date & Time Functions**

Used for working with dates and timestamps.

| Function | Purpose | Example |
| --- | --- | --- |
| `TODAY()` | Returns today’s date | `=TODAY()` |
| `NOW()` | Returns current date & time | `=NOW()` |
| `DAY()` | Extracts the day from a date | `=DAY(A1)` |
| `MONTH()` | Extracts the month from a date | `=MONTH(A1)` |
| `YEAR()` | Extracts the year from a date | `=YEAR(A1)` |

✅ **Use Case:** An HR analyst tracking employee attendance or an accountant working on financial reports based on specific dates.

### **3. Hands-On Exercise on MacBook Air**

Try these functions step by step:

1️⃣ **SUM Function:**

- In column **A**, enter numbers: `10, 20, 30, 40, 50`.
- In **B1**, type `=SUM(A1:A5)`.
- Press **Enter**—Excel calculates the total instantly!

2️⃣ **IF Function**

- In **C1**, type `=IF(A1>25, "Above Average", "Below Average")`.
- Drag it down across rows—observe how results change dynamically.

3️⃣ **LEFT Function:**

- In **D1**, type a name like `"Vybhav"` and use `=LEFT(D1, 3)`.
- It extracts `"Vyb"`—useful for breaking names or codes into segments.

By trying these exercises, you’ll see how functions work in real time, reinforcing your understanding.

---

## Data referencing in formulas

### **1. What Is Data Referencing in Formulas?**

Referencing data means using **cell addresses** instead of static values in a formula. This allows Excel to automatically update results when the referenced data changes.

For example, instead of manually typing:

You would use:

```
=A1 + B1
```

If the values in **A1** or **B1** change, the formula automatically recalculates—making your analysis more efficient.

### **2. Types of Cell References**

### **A. Relative References (Default)**

A **relative reference** adjusts automatically when copied to another location.

Example:

```
=A1 + B1
```

If copied down from row **1** to row **2**, it becomes:

```
=A2 + B2
```

✅ **Use Case:** Best for formulas that should adjust dynamically, like calculating totals across multiple rows.

### **B. Absolute References (Fixed)**

An **absolute reference** remains unchanged when copied. It’s denoted by `$` before column and row identifiers.

Example:

```
=$A$1 + B1
```

If copied down, **$A$1** remains fixed, but **B1** adjusts.

✅ **Use Case:**

- **Fixed values** (e.g., tax rates, fixed percentages).
- **Lookup formulas** where a reference must remain constant.

### **C. Mixed References (Partial Lock)**

A **mixed reference** locks either the row or the column.

| Type | Example | Behavior |
| --- | --- | --- |
| Lock column | `$A1` | Column **A** stays fixed, row changes. |
| Lock row | `A$1` | Row **1** stays fixed, column changes. |

✅ **Use Case:**

- **Column locking** in formulas for calculations across different rows.
- **Row locking** when data needs to vary across columns.

### **3. Practical Examples for Data Analysts**

Let’s apply these references in real-world scenarios.

### **Example 1: Calculating Tax (Absolute Reference)**

Suppose:

- **Column A** contains sales figures.
- **Cell B1** holds a fixed **tax rate** of **10%**.
- You want **Column B** to show the tax for each sale.

Formula for B2:

```
=A2 * $B$1
```

Copying this down will ensure **$B$1 remains constant**, applying the same tax rate to all rows.

### **Example 2: Dynamic Growth Analysis (Relative Reference)**

Suppose:

- **Column A** holds last year’s revenue.
- **Column B** holds projected revenue growth percentages.
- **Column C** needs to calculate next year’s expected revenue.

Formula for **C2**:

```
=A2 * (1 + B2)
```

If copied down, **A2 and B2** dynamically adjust row by row.

✅ **Benefit:** Quick scenario analysis across multiple rows.

### **4. Hands-On Exercise for MacBook Air**

Try this step-by-step:

1️⃣ **Enter Data in Excel:**

- **A1:** `Product`
- **B1:** `Price`
- **C1:** `Tax Rate` (`Fixed at 5% in C2`)
- **D1:** `Final Price`

2️⃣ **Enter Sample Data:**

- `A2-A6`: Product names (`Apple, Banana, Cherry...`)
- `B2-B6`: Prices (`10, 15, 20...`)
- `C2`: `5%`

3️⃣ **Apply an Absolute Reference Formula:**

- In **D2**, type:
    
    ```
    =B2 * (1 + $C$2)
    ```
    
- Drag it down using the **fill handle** to see dynamic updates.

---

## Error handling

### **1. Common Errors in Excel**

Excel returns specific error messages when something goes wrong in a formula. Here are the most common ones:

| Error Code | Meaning & Cause |
| --- | --- |
| `#DIV/0!` | Trying to divide by zero or an empty cell. |
| `#VALUE!` | Using the wrong type of data (e.g., adding text to a number). |
| `#NAME?` | Excel doesn’t recognize the function name (maybe misspelled). |
| `#REF!` | A cell reference is broken (perhaps deleted or moved). |
| `#N/A` | Lookup functions (e.g., `VLOOKUP()`) couldn’t find a match. |
| `#NUM!` | Invalid numeric calculations (like square root of a negative number). |
| `#NULL!` | Incorrectly using ranges or missing intersection points. |

✅ **Why It Matters:**

If an error isn’t handled correctly, it can affect downstream calculations, leading to inaccurate reports or incorrect insights.

### **2. Fixing & Preventing Errors**

Here’s how you can troubleshoot and prevent errors:

### **A. Handling Division by Zero (`#DIV/0!`)**

Problem:

If a formula divides a number by zero or an empty cell, Excel throws a `#DIV/0!` error.

✅ **Fix:**

Use `IFERROR()` or `IF()` to handle it gracefully:

```
=IF(B1=0, "N/A", A1/B1)

```

This formula replaces errors with `"N/A"` instead of breaking your spreadsheet.

### **B. Correcting Text vs. Numbers (`#VALUE!`)**

Problem:

If Excel tries to add a number to text, you'll see `#VALUE!`.

✅ **Fix:**

- Ensure all inputs are correctly formatted as numbers.
- Use `ISTEXT()` or `ISNUMBER()` to check:

```
=IF(ISNUMBER(A1), A1*2, "Invalid input")

```

### **C. Fixing Broken References (`#REF!`)**

Problem:

If referenced cells are deleted or moved, Excel returns `#REF!`.

✅ **Fix:**

- Avoid deleting referenced cells.
- Instead of hardcoded references (`=A1+B1`), use **structured tables** or **named ranges**.

### **D. Handling Missing Lookup Values (`#N/A`)**

Problem:

If a lookup function (`VLOOKUP()`, `MATCH()`, etc.) can't find a match, it returns `#N/A`.

✅ **Fix:**

Use `IFNA()` to replace missing values with a message:

```
=IFNA(VLOOKUP(A1, B2:D10, 2, FALSE), "Not Found")

```

This ensures your formulas don’t break when a lookup fails.

### **E. Checking for Numeric Errors (`#NUM!`)**

Problem:

Occurs when a calculation isn’t mathematically valid (e.g., square root of a negative number).

✅ **Fix:**

Use `IF()` to catch invalid inputs:

```
=IF(A1<0, "Error", SQRT(A1))

```

### **3. Debugging With Error Checking Tools**

✅ **Trace Errors:**

- Go to **Formulas** → **Error Checking** → **Trace Error**.
- Excel highlights problematic cells, helping you identify mistakes.

✅ **Evaluate Formula Step-by-Step:**

- Select a formula → Click **Evaluate Formula** (under the Formulas tab).
- See how Excel calculates each step—useful for debugging complex expressions.

✅ **Use Conditional Formatting:**

- Highlight cells with potential errors (like missing data or outliers).
- Example: **Home → Conditional Formatting → Highlight Cells Rules**.

### **4. Hands-On Exercise on MacBook Air**

Practice handling errors with this step-by-step exercise:

1️⃣ **Set Up a Table:**

| A | B | C |
| --- | --- | --- |
| 100 | 10 | `=A1/B1` |
| 200 | 0 | `=A2/B2` |
| Text | 5 | `=A3*B3` |
|  |  | `=VLOOKUP(50, A1:B3, 2, FALSE)` |

2️⃣ **Apply Error Handling Formulas:**

- **Prevent division errors:** Modify C2 to `=IF(B2=0, "Error", A2/B2)`.
- **Fix text input errors:** Use `=IF(ISNUMBER(A3), A3*B3, "Invalid")`.
- **Handle lookup failures:** Change the last formula to `=IFNA(VLOOKUP(50, A1:B3, 2, FALSE), "Not Found")`.

Try modifying the table and observe how Excel manages errors effectively!

---