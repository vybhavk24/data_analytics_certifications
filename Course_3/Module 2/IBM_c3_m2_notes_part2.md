# IBM_c3_m2_part2

## Introduction to Dashboards

A **dashboard** is a centralized visual display that brings together multiple charts, tables, and key metrics in one place. Think of it as the cockpit for your business data—providing an at-a-glance view of a business's performance. 

For a data analyst, a dashboard is an invaluable tool that consolidates critical insights so that decision-makers can quickly understand trends, monitor performance, and identify areas that may need attention.

### **1. What is a Dashboard?**

- **Centralized Data Display:**
A dashboard compiles data from one or multiple sources, presenting it through visuals like charts, pivot tables, and gauges.
- **Real-Time Monitoring:**
Dashboards often update automatically (or can be refreshed easily) so that you always have the most current insights.
- **Interactive:**
Modern dashboards include interactive features like slicers, filters, and drill-down capabilities. This enables users to explore data dynamically and tailor insights to their specific needs.

### **2. Why Are Dashboards Important?**

- **Quick Decision-Making:**
    
    Instead of navigating through multiple spreadsheets or reports, business leaders can view key performance indicators (KPIs) on a dashboard and make rapid, data-informed decisions.
    
- **Consolidated Insights:**
    
    A good dashboard brings together different aspects of the business—from sales trends and profit margins to customer behavior and operational metrics—in a single view. This holistic perspective can reveal relationships and correlations that might be missed when data is siloed.
    
- **Improved Communication:**
    
    Dashboards provide a clear, visual summary of information that’s easier to interpret than raw data. They help communicate complex insights in a way that is accessible to both technical and non-technical stakeholders.
    
- **Accountability and Monitoring:**
    
    By continuously displaying key metrics, dashboards help teams track progress against targets and maintain accountability.
    

### **3. Key Components of a Dashboard**

- **Charts and Graphs:**
    
    Include various types such as bar charts, line charts, pie charts, and treemaps to represent data visually.
    
- **Pivot Tables:**
    
    Summarize large volumes of data and allow you to drill down into specific areas of interest.
    
- **Interactive Filters and Slicers:**
    
    Enable users to interact with the data (e.g., filter by region, by category, or by time period) and view insights from different perspectives.
    
- **KPIs and Metrics:**
    
    Often, dashboards include cards or gauges that highlight critical metrics like total sales, average profit, or conversion rates.
    
- **Textual Annotations and Titles:**
    
    Clear labels, titles, and annotations are important to guide users on what each visualization represents and to provide context.
    

### **4. How to Create a Basic Dashboard in Excel - General idea**

Imagine you have a sales dataset with these headers:

`Order ID, Amount, Profit, Quantity, Category, Sub-Category, PaymentMode, Order Date, CustomerName, State, City, Year-Month`.

Here’s a practical, step-by-step approach:

### **Step 1: Organize Your Data**

- Ensure your dataset is clean and formatted consistently.
- Create a separate worksheet for your dashboard.

### **Step 2: Build Summaries**

- **Pivot Tables:**
    
    Create Pivot Tables to summarize key metrics, for example:
    
    - **Total Sales by Category:** Drag `Category` to Rows and `Amount` to Values.
    - **Monthly Sales Trend:** Drag `Year-Month` to Rows and `Amount` to Values.
    - **Profit by State:** Drag `State` to Rows and `Profit` to Values.
- **Key Metrics Cards:**
    
    Use cells to display aggregated values like total revenue or average profit. You can use formulas such as `=SUM(Amount)`.
    

### **Step 3: Insert Visuals**

- **Charts:**
    
    For each Pivot Table or data summary, insert corresponding charts:
    
    - Use a **Bar Chart** for Total Sales by Category.
    - Use a **Line Chart** for the Monthly Sales Trend.
    - Use a **Pie Chart** for Payment Mode Distribution (if applicable).
- **Interactive Elements:**
    
    Insert slicers to make your dashboard interactive:
    
    - Click on your Pivot Table, then go to **PivotTable Analyze → Insert Slicer**, and select fields like `State` or `Category`.

### **Step 4: Layout and Design**

- Arrange your Pivot Tables, charts, slicers, and key metric cells within the dashboard worksheet.
- Use Excel’s drawing tools (like shapes and text boxes) to add titles, labels, and clear separations.
- Ensure a consistent color scheme and formatting style to create a visually appealing and easy-to-read dashboard.

### **Step 5: Test and Refine**

- Once everything is set up, interact with your dashboard by filtering different slicers or updating data.
- Make adjustments to improve clarity and ensure that all key metrics are visible at a glance.

---

## **✅ Step-by-Step Guide to Create a Dashboard - Sales dataset.**

The dataset is included in the practice worksheet.

### **Step 1: Prepare the Data**

### **1.1 Open Excel**

- Paste your data into a new Excel sheet (or import the CSV file if you have it).
- Name the sheet RawData.

### **1.2 Format as Table**

- Select any cell in your data.
- Press **Ctrl + T** → Tick “My table has headers” → Click OK.
- This will help in structured referencing.

Rename the table:

- Click on the table → Go to **Table Design** → Rename it to SalesData.

### **Step 2: Create a Data Summary Sheet**

We’ll use **Pivot Tables** to summarize key metrics like:

- Total Sales (Amount)
- Total Profit
- Orders by Category
- Monthly Sales Trend
- Top Cities/States

### **2.1 Insert Pivot Table**

- Create a new sheet → name it Summary.
- Click anywhere in the SalesData table → Go to **Insert > PivotTable**
- Choose: “New Worksheet” → Click OK.

### **📊 Let’s Create the Following Pivot Tables:**

### **2.2 Total Sales by Category**

- Drag **Category** to Rows.
- Drag **Amount** to Values (ensure it says “Sum of Amount”).

### **2.3 Total Profit by Sub-Category**

- Drag **Sub-Category** to Rows.
- Drag **Profit** to Values.

### **2.4 Monthly Sales Trend**

- Use **Year-Month** in Rows.
- Use **Amount** in Values.
- Right-click a date > Sort → Oldest to Newest.

### **2.5 Sales by State**

- State → Rows.
- Amount → Values.

### **2.6 Orders by Payment Mode**

- Payment Mode → Rows.
- Order ID → Values → Change it to “**Count**” of Order ID.

### **Step 3: Create the Dashboard Sheet**

Now we’ll visualize these Pivot Tables in a dashboard.

### **3.1 Create a New Sheet**

- Name it Dashboard.

### **3.2 Insert Pivot Charts**

Go back to each Pivot Table and:

- Select it → Insert > Recommended Charts (Column, Bar, Pie as needed)
- Example:
    - Category Sales: Bar Chart
    - Profit by Sub-Category: Column Chart
    - Monthly Trend: Line Chart
    - Orders by Payment Mode: Pie Chart

Move each chart to the Dashboard sheet:

- Right-click chart → Move Chart → Object in: Dashboard

### **Step 4: Add Slicers (Filters)**

Make your dashboard interactive.

### **4.1 Insert Slicers**

Click any Pivot Table > PivotTable Analyze > Insert Slicer

- Choose filters like:
    - Category
    - State
    - Year-Month

Arrange them neatly on your dashboard.

To make slicers control all charts:

- Click Slicer → **Report Connections** → Tick all related PivotTables

### **Step 5: Design the Dashboard**

Now give it a polished look:

### **🖌️ Tips:**

- Add a title: Insert > Text Box > “📊 Sales Dashboard”
- Use shapes and colors to divide sections.
- Remove chart titles (if you’re adding custom text boxes).
- Align charts neatly using the **Format > Align** options.

---

### **Real-World Impact of Dashboards**

- **Business Monitoring:**
    
    Dashboards are used by managers to track sales performance, monitor market trends, and adjust strategies in real time. For example, a retail manager might use a dashboard to spot a sudden drop in sales in a particular region and take corrective action immediately.
    
- **Operational Efficiency:**
    
    In logistics, dashboards help monitor factors such as delivery times and inventory levels, enabling quick responses to potential issues.
    
- **Data-Driven Culture:**
    
    A dashboard encourages regular review of business metrics, fostering a culture where decisions are based on data rather than intuition.