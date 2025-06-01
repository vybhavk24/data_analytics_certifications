# IBM_c3_m1

For this module we’re using Chocolate sales dataset and it’s included in IBM_c2_m1_practice.xlxs → Uploaded in practice folders.

## Introduction to charts

Charts are **visual tools** that help present data in an easy-to-understand format. Instead of analyzing thousands of rows manually, charts **highlight trends, patterns, and comparisons** at a glance. In data analysis, charts are **essential for effective decision-making** because they simplify complex datasets and make insights accessible.

### **1️⃣ Why Are Charts Important in Data Analysis?**

Charts **convert numerical data into meaningful visuals** that make patterns easier to identify. Some benefits include:

✔ **Identify Trends** → Spot seasonal sales patterns or growth over time.

✔ **Compare Categories** → See which product, region, or salesperson performs best.

✔ **Detect Anomalies** → Find outliers in sales or customer behavior.

✔ **Improve Data Communication** → Stakeholders understand visual insights better than tables.

✅ **Example:**

Imagine a sales report showing **monthly revenue figures**—instead of reading a long table, a **line chart instantly reveals if sales are increasing or declining**.

### **2️⃣ Types of Charts and When to Use Them**

Each chart type serves a different analytical purpose. Choosing the right one enhances clarity.

### **A. Bar Chart (Comparisons)**

✔ **Best for:** Comparing quantities across categories (e.g., revenue per product).

✔ **Use case:** Which **state** had the highest sales?

✔ **Appearance:** Vertical or horizontal bars representing values.

### **B. Line Chart (Trends Over Time)**

✔ **Best for:** Tracking changes over time (e.g., monthly revenue trends).

✔ **Use case:** Are **sales increasing or declining over months?**

✔ **Appearance:** A continuous line showing data points.

### **C. Pie Chart (Proportions)**

✔ **Best for:** Showing percentage distributions (e.g., payment mode breakdown).

✔ **Use case:** What **share of sales comes from online payments?**

✔ **Appearance:** A circular graph divided into slices.

### **D. Scatter Plot (Correlations)**

✔ **Best for:** Identifying relationships between variables (e.g., sales amount vs. boxes shipped).

✔ **Use case:** Does **shipping more boxes lead to higher revenue?**

✔ **Appearance:** Dots plotted on X-Y axes to reveal patterns.

### **E. Histogram (Data Frequency)**

✔ **Best for:** Analyzing data distribution (e.g., most common order amount range).

✔ **Use case:** What **price range do most sales fall into?**

✔ **Appearance:** Bars showing data frequency across intervals.

✅ **Example:**

A **bar chart compares sales across product categories**, while a **line chart tracks sales growth monthly**.

### **3️⃣ Practical Hands-On Exercise (Using Your Sales Dataset)**

### **A. Bar Chart (Sales Amount by Country)**

✔ **Steps:**

1️⃣ Open **your dataset in Excel**.

2️⃣ Select columns: `"Country"` and `"Amount"`.

3️⃣ Go to **Insert → Column Chart → Clustered Bar Chart**.

4️⃣ Customize:

- Click bars → Change colors for clarity.
- Add labels (**Chart Design → Add Chart Element → Data Labels**).
- Rename title (**Chart Title → Edit**).

5️⃣ Excel now visually shows **which country generated the highest revenue → You can see this in chart.**

### **B. Line Chart (Sales Over Time)**

✔ **Steps:**

1️⃣ Select `"Date"` and `"Amount"`.

2️⃣ Go to **Insert → Line Chart → Smooth Line Chart**.

3️⃣ Format axes (**Right-click → Format Axis**) to display dates properly.

4️⃣ Add a **trendline** (**Chart Design → Add Chart Element → Trendline**).

5️⃣ Observe peaks and dips in **sales trends**.

✅ **Key Insight:**

A **trendline helps forecast future revenue trends**.

### **C. Scatter Plot (Boxes Shipped vs. Amount)**

✔ **Steps:**

1️⃣ Select `"Boxes Shipped"` and `"Amount"`.

2️⃣ Go to **Insert → Scatter Chart → Scatter with Straight Lines**.

3️⃣ Format points for clarity.

4️⃣ Observe **correlation**—does shipping more boxes result in higher sales?

✅ **Key Insight:**

This visualization helps **detect patterns between shipments and revenue**, optimizing supply chain strategies.

---

## Intro to pivot tables

A **Pivot Table** is one of Excel’s most powerful features for **summarizing, analyzing, and exploring large datasets**. 

Instead of manually sorting and filtering, a pivot table **automatically organizes data** into meaningful summaries—making your analysis **faster, more dynamic, and insightful**.

### **1️⃣ Why Use Pivot Tables?**

Pivot tables **solve common challenges in data analysis**, making it easy to **extract insights without complex formulas**.

✔ **Summarize Large Data Quickly** → Calculate **totals, averages, and rankings** instantly.

✔ **Dynamic Exploration** → Rearrange categories **without changing the raw dataset**.

✔ **Efficient Filtering** → Drill down into specific segments (e.g., **sales per salesperson or region**).

✔ **Interactive Reports** → Works seamlessly with **Pivot Charts for visualization**.

✅ **Example:**

If your dataset contains **"Sales Amount," "Product Name," and "Region,"** a pivot table can **instantly show total sales by product and region**—helping businesses identify top-performing categories.

### **2️⃣ How to Create a Pivot Table in Excel on MacBook**

Let’s create a Pivot Table **step-by-step** using your **sales dataset**.

### **✅ Steps to Create a Pivot Table**

1️⃣ **Open Your Sales Dataset in Excel**.

2️⃣ Select any cell inside your dataset.

3️⃣ Go to **Insert → Pivot Table**.

4️⃣ Choose **New Worksheet** (recommended) or **Existing Worksheet** for placement.

5️⃣ Click **OK**, and Excel will insert a blank Pivot Table.

✅ **You now have a Pivot Table ready for customization!**

### **3️⃣ Customizing the Pivot Table**

Once created, you’ll see the **Pivot Table Fields Panel** on the right, where you can **drag fields to different sections**:

| **Section** | **Purpose** |
| --- | --- |
| **Rows** | Groups data by categories (e.g., "Product Name"). |
| **Values** | Performs calculations (e.g., total "Sales Amount"). |
| **Columns** | Creates side-by-side comparisons (e.g., sales per "Country"). |
| **Filters** | Enables easy data filtering (e.g., view only sales from 2025). |

### **Example: Analyzing Sales by Product**

✔ Drag **"Product Name"** into **Rows**.

✔ Drag **"Sales Amount"** into **Values** → Excel automatically calculates the **total sales for each product**.

✔ Apply **Sorting** (**Right-click → Sort → Largest to Smallest**) to rank top-selling items.

✅ **Key Insight:**

Instead of manually calculating **total sales per product**, the Pivot Table does it **instantly.**

(So the dataset will have repeated values like “99% Dark & Pure” → It’ll be consider as on and all sales related to this comes in only one row!

### **4️⃣ Adding Filters to Refine Analysis**

Pivot Tables allow dynamic filtering, making reports **interactive and precise**.

### **✅ Steps to Add a Filter**

1️⃣ Drag `"Region"` into the **Filters section**.

2️⃣ Click the **dropdown arrow** in the Pivot Table.

3️⃣ Select `"India"`, and Excel updates the table to **only show India sales → see it**

✅ **Key Insight:**

Easily drill down into **specific locations, dates, or product categories**.

### **5️⃣ Sorting & Formatting for Clearer Insights**

✔ **Sort Data Automatically** → Click **Values dropdown → Sort Largest to Smallest** (rank top products).

✔ **Format Numbers** → Click on any number in the Pivot Table → **Number Format → Currency**.

✔ **Apply Conditional Formatting** → Highlight top-performing products with **Data Bars or Colors**.

✅ **Key Insight:**

Well-formatted Pivot Tables **make reports easier to interpret and visually appealing**.

### **6️⃣ Hands-On Exercise With Your Kaggle Sales Dataset**

Try these **MacBook-specific** steps:

✔ **Summarize total sales per category** using Pivot Tables.

✔ **Rank the top 5 products based on revenue**.

✔ **Filter the table to analyze sales only from 2025**.

✔ **Create a Pivot Chart to visualize trends.**

---

## **Excel PivotChart: Visualizing Data Dynamically**

A **PivotChart** is a powerful feature in Excel that helps **visualize Pivot Table data interactively**.

Unlike regular charts, PivotCharts allow you to **filter, sort, and drill down into data dynamically** without modifying the original dataset.

### **1️⃣ Why Use PivotCharts?**

✔ **Instantly visualize Pivot Table summaries**—no need to manually create separate charts.

✔ **Dynamic filtering**—adjust data views with slicers and filters.

✔ **Flexible analysis**—group and compare categories on the fly.

✔ **Works seamlessly with Pivot Tables**—updates automatically when Pivot Table data changes.

✅ **Example:**

Instead of manually creating **a chart for total sales per region**, a PivotChart automatically **updates when filters change**, giving you a **clear view** of different regional performances.

### **2️⃣ Creating a PivotChart in Excel (MacBook Steps)**

### **✅ Steps to Create a PivotChart**

1️⃣ Open your **Sales Dataset in Excel**.

2️⃣ Ensure you have an existing **Pivot Table** (If not, create one: **Insert → Pivot Table**).

3️⃣ Click **any cell in the Pivot Table** to activate it.

4️⃣ Go to **Pivot Table Analyze → Pivot Chart**.

5️⃣ Choose a **chart type** (Bar, Line, Pie, etc.) based on your analysis needs.

6️⃣ Click **OK**, and Excel generates the PivotChart.

✅ **Key Feature:**

Since PivotCharts link directly to **Pivot Tables**, **changing filters automatically updates the chart**.

### **3️⃣ Customizing Your PivotChart**

PivotCharts offer various customization options to enhance clarity.

For all these → Click on chart → Go to design tab (besides analyse)

✔ **Change Chart Type** → Click on the chart → **Design → Change Chart Type**.

✔ **Add Labels & Titles** → Click **Chart Elements → Data Labels** for better readability.

✔ **Modify Colors** → Click **Chart Design → Change Colors** to highlight trends.

✔ **Adjust Filters Dynamically** → Click slicers to **interact with the chart (below)**

✅ **Example:**

If analyzing **monthly sales trends**, a **line PivotChart with a trendline** makes forecasts more intuitive.

### **4️⃣ Using Slicers with PivotCharts**

PivotCharts work **perfectly with slicers**, allowing interactive filtering.

### **✅ Steps to Add a Slicer**

1️⃣ Click **inside the Pivot Table**.

2️⃣ Go to **Pivot Table Analyze → Insert Slicer**.

3️⃣ Select a filtering category (e.g., “products”.)

4️⃣ Click **OK**, and a slicer appears.

5️⃣ Click slicer buttons (any products) to **instantly filter the PivotChart**.

✅ **Key Insight:**

With slicers, you can **analyze trends by region or category** without modifying the dataset.

### **5️⃣ Hands-On Exercise with Your Sales Dataset**

✔ **Create a PivotTable summarizing total sales by product category.**

✔ **Generate a PivotChart to visualize the top-performing products.**

✔ **Add a slicer to filter sales trends by country.**

✔ **Customize the chart title, colors, and labels for clarity.**

By practicing these steps, you'll gain **real-world experience in dynamic data visualization.**

---