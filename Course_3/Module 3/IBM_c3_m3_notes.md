# IBM_c3_m3

## IBM cognos analytics

IBM Cognos Analytics is a **business intelligence (BI) and data analytics platform** that enables organizations to **collect, analyze, visualize, and share insights** from their data. 

It combines **AI-powered analytics, interactive dashboards, and enterprise-grade reporting** to help businesses make informed decisions.

### **1️⃣ What is IBM Cognos Analytics?**

IBM Cognos Analytics is a **self-service BI tool** that allows users to:
✔ **Connect to multiple data sources** (databases, cloud services, spreadsheets).

✔ **Prepare and clean data** before analysis.

✔ **Create interactive dashboards and reports** with AI-driven insights.

✔ **Perform predictive analytics** using machine learning models.

✔ **Collaborate and share insights** securely across teams.

It is designed for **both technical and non-technical users**, making it accessible for business analysts, executives, and data professionals.

### **2️⃣ Key Features of IBM Cognos Analytics**

IBM Cognos Analytics offers a wide range of features that enhance **data exploration, visualization, and reporting**.

### **🔹 AI-Powered Insights**

✔ **Natural Language Querying:** Users can ask questions in plain language, and Cognos generates relevant visualizations.

✔ **Automated Data Discovery:** AI suggests trends, anomalies, and patterns in datasets.

✔ **Predictive Analytics:** Machine learning models help forecast future trends.

### **🔹 Interactive Dashboards**

✔ **Drag-and-Drop Interface:** Easily create dashboards without coding.

✔ **Customizable Visualizations:** Choose from charts, maps, and tables.

✔ **Real-Time Data Updates:** Dashboards refresh automatically with new data.

### **🔹 Advanced Reporting**

✔ **Enterprise-Grade Reports:** Generate detailed reports with complex calculations.

✔ **Scheduled Reports:** Automate report generation and distribution.

✔ **Multi-Format Export:** Export reports in PDF, Excel, or HTML formats.

### **🔹 Data Integration & Preparation**

✔ **Connect to Multiple Data Sources:** Supports databases, cloud storage, and spreadsheets.

✔ **Data Cleaning & Transformation:** Prepare raw data for analysis.

✔ **Data Modeling:** Create relationships between datasets for deeper insights.

### **🔹 Security & Governance**

✔ **Role-Based Access Control:** Restrict data access based on user roles.

✔ **Data Encryption:** Ensures secure data storage and transmission.

✔ **Audit Trails:** Track changes and user activities for compliance.

### **3️⃣ How IBM Cognos Analytics Works**

IBM Cognos Analytics follows a **structured workflow** for data analysis:

### **Step 1: Data Connection**

✔ Import data from **databases, cloud services, or spreadsheets**.

✔ Use **ETL (Extract, Transform, Load) tools** to clean and structure data.

### **Step 2: Data Exploration**

✔ Use **AI-powered insights** to detect trends and anomalies.

✔ Apply **filters and aggregations** to refine datasets.

### **Step 3: Visualization & Reporting**

✔ Create **interactive dashboards** using drag-and-drop tools.

✔ Generate **detailed reports** with custom calculations.

### **Step 4: Sharing & Collaboration**

✔ Publish dashboards for **team-wide access**.

✔ Schedule **automated report distribution**.

---

## Creating a **simple dashboard in IBM Cognos Analytics**

I’m using Sales Dataset.csv - uploaded in practice folder

### **🔰 STEP 1: Log into Cognos Analytics**

1. Open Cognos Analytics in your browser.
2. **Sign in** with your credentials.

### **📥 STEP 2: Upload Your Dataset**

If not already done:

1. Click the **“+ New”** button (top right).
2. Select **“Upload files”**.
3. Choose your **Sales Dataset (Excel or CSV)**.
4. Once uploaded, click **“Check” icon** or **“Open”**.

### **📊 STEP 3: Create a New Dashboard**

1. From the homepage, click **“+ New” → “Dashboard”**.
2. Choose a layout → 3 column layout
3. Click **“Select source”** and choose your uploaded file (your dataset).
4. Wait a few seconds until the data loads.

### **📋 STEP 4: Add KPIs (Tiles)**

Let’s show **Total Sales and Total Profit**.

### **➤ Large Tile:**

1. From the left panel, **drag a “Profit”, “Category” and “State”** onto your dashboard.
2. Drag “Quantity” to second tile.
3. Drag “Amount” to first tile
4. Cognos will auto-summarize it to a total.

**Now you’ve a simple dash-board.**

### **📦 STEP 5: Add Bar Chart – Sales by Category**

1. Drag a **“Bar chart”** widget into the dashboard area.
2. Drag **Category** into the **X-axis**.
3. Drag **Amount** into the **Y-axis**.
4. You’ll now see Sales for each Category.

### **📆 STEP 6: Add Line Chart – Monthly Sales Trend**

1. Drag a **Line chart** widget into the dashboard.
2. Drag **Year-Month** into the **X-axis** (use this instead of full Order Date).
3. Drag **Amount** into the **Y-axis**.
4. This shows how sales change month-by-month.

### **💳 STEP 7: Add Pie Chart – Payment Modes**

1. Drag a **Pie chart** widget onto the dashboard.
2. Drag **PaymentMode** into the **Slices (Group)**.
3. Drag **Amount** into the **Values**.
4. You’ll see the share of sales per payment method.

### **🧼 STEP 8: Tidy Up and Save**

1. Add titles to each chart (click → Edit Title).
2. Resize charts if needed by dragging the corners.
3. Click **“Save”** (top right corner).
    - Name it something like **“Sales Dashboard”**

You can explore the data by selecting particular bars in main column → where you’ve dragged: Profit, Categories and State.

Link to simple dashboard:

```tsx
https://us1.ca.analytics.ibm.com/bi/?perspective=dashboard&pathRef=.my_folders%2FSimple%2Bdashboard&action=view&mode=dashboard&subView=model000001972b02e3a6_00000000
```

---

## Advanced capabilities in Cognos Analytics

Below is a comprehensive, step-by-step guide to building an advanced analytics dashboard in IBM Cognos Analytics. 

In this guide, we’ll assume you’ve already uploaded your sales dataset (with fields such as Order ID, Amount, Profit, Quantity, Category, Sub-Category, PaymentMode, Order Date, CustomerName, State, City, Year-Month) and are now ready to add advanced interactivity. We’ll cover the following tasks:

- **Task A:** Create Calculations
- **Task B:** Keep/Exclude Data Points from a Visualization
- **Task C:** Set Top/Bottom on a Visualization
- **Task D:** Create and Leverage Navigation Paths
- **Task E:** Filter Data in the Current Tab

### **Getting Started: Create a New Dashboard**

1. **Log In and Create a Dashboard:**
    - Open IBM Cognos Analytics in your browser and log in.
    - Click the **“New”** button (usually at the top-left).
    - Select **“Dashboard”** from the list.
    - Choose a template (you may start with a **Blank** template for full control) and click **“OK.”**
2. **Attach Your Sales Dataset:**
    - In the new dashboard canvas, click **“Add a Source”** on the left.
    - Select your uploaded sales dataset.
    - The tool will then display your dataset fields for use.

Now you’re ready to add advanced elements.

### **Task A: Create Calculations**

**Objective:** Add a new calculated field (for example, Profit Margin) that computes the profit as a percentage of Amount.

**Steps:**

1. **Open the Data Panel:**
    - On the left-hand side of the dashboard editor, locate the list of available fields from your dataset.
2. **Create a New Calculation:**
    - Click on the **“Create Calculation”** or **“Add Calculation”** option (often represented by a “+” icon near measures).
    - Name your new field. For example: **Profit Margin (%)**.
    - In the calculation editor, enter the formula. A typical formula might be:
    (Ensure that you use the field names exactly as they appear in your dataset.)
        
        ```
        ([Profit] / [Amount]) * 100
        
        ```
        
3. **Save and Validate:**
    - Click **“Save”** (or **“Apply”**) to create the calculated field.
    - You should now see **Profit Margin (%)** in your field list, and you can drag it into any visualization.

### **Task B: Keep/Exclude Data Points from a Visualization**

**Objective:** Refine a chart by including only certain data points (e.g., excluding outliers or focusing on a specific category).

**Steps:**

1. **Insert a Visualization:**
    - For example, create a bar chart by dragging the **Category** field to the X-axis and the **Amount** to the Y-axis.
2. **Open Visualization’s Filter Options:**
    - Click on the chart to select it.
    - Locate the **“Filter”** button or the **“Properties”** pane for the visualization. In Cognos Analytics, you’ll usually see an option labeled **“Add Filter”**.
3. **Set Your Inclusion or Exclusion Criteria:**
    - To **keep** only certain data points, choose the field you want to filter on. For example, select **“Category”**.
    - Choose the condition (e.g., **“is equal to”** or **“is not equal to”**) and then specify the category value(s) you want to include or exclude.
    - For instance, you might set a filter to **include only** “Electronics” and “Furniture” and exclude all others.
4. **Apply and Validate:**
    - Apply the filter. The chart will now update to display only the selected data points.
    - If you wish to remove a filter later, you can clear or adjust the conditions in the filter pane.

### **Task C: Set Top/Bottom on a Visualization**

**Objective:** Limit your visualization to only show the top or bottom entries (e.g., Top 5 categories by Amount).

**Steps:**

1. **Insert or Select an Existing Chart:**
    - Let’s continue with our bar chart showing **Category** vs. **Amount**.
2. **Access Sorting/Filtering Options:**
    - Click on the chart and open the chart’s settings or properties.
    - Look for a section labeled something like **"Sort & Filter"** or **"Value Filters"**.
3. **Define the Top/Bottom Filter:**
    - Choose the option such as **“Show Top/Bottom Items.”**
    - Select **“Top”** (or **“Bottom”**) and specify the number of items, e.g., **5**.
    - Set the measure by which you want to rank the items; in this case, select **Amount**.
4. **Apply the Filter:**
    - Confirm your selection. The bar chart will now display only the top 5 categories by sales Amount.
    - This technique helps emphasize the most significant contributors in your data.

### **Task D: Create and Leverage Navigation Paths**

**Objective:** Build a guided user flow so viewers can drill down from summary to detailed views.

**Steps:**

1. **Plan Your Navigation:**
    - Decide which visualizations will serve as summary (e.g., an overall sales bar chart) and which will be detailed (e.g., sales by region within a selected category).
2. **Configure Drill-Through Actions:**
    - Click on a visualization (for example, the bar representing “Electronics” in your sales by Category chart).
    - In the properties pane, look for **“Add Action”** or **“Drill-Through” Options.**
    - Set up the drill-through:
        - **Source:** Your summary chart.
        - **Target:** A detailed dashboard or report page that shows, for instance, sales by individual product within "Electronics."
    - Define any parameters needed (e.g., passing the selected category value to the target report).
3. **Add Navigation Aids (Breadcrumbs/Buttons):**
    - On your detailed page, include a “Back” button or breadcrumb navigation:
        - Insert a button (using the **“Insert Control”** option) and link it to the previous dashboard page.
        - Alternatively, enable a breadcrumb feature if your tool supports it.
4. **Test Your Navigation Path:**
    - Click on the chart’s data point to ensure it correctly drills through to the detailed view.
    - Use the back button to confirm you can easily return to the summary view.

### **Task E: Filter Data in the Current Tab**

**Objective:** Implement filters on your dashboard page that let users interactively limit the data displayed (e.g., by State or Year-Month).

**Steps:**

1. **Insert Filter Controls:**
    - On the dashboard, locate the **“Add Control”** or **“Insert”** menu.
    - Select **“Filter”** or **“Slicer.”**
2. **Assign a Field to the Filter:**
    - Choose a field from your dataset that you want to enable filtering on. For example, select the **“State”** field.
    - A filter control will appear on the dashboard that lists all states.
3. **Configure the Filter:**
    - You may customize whether users can single- or multi-select values.
    - Resize and position the filter control as desired on your dashboard.
4. **Link the Filter to Dashboard Visuals:**
    - Ensure the filter is applied to all relevant visualizations on the current tab. In Cognos Analytics, filters typically propagate to connected objects automatically.
    - Test the filter by selecting different states and verifying that all charts update to reflect the chosen criteria.

### **Recap**

- **Creating Calculations** (Task A) to enhance your data with custom metrics.
- **Keeping/Excluding Data Points** (Task B) to ensure only relevant data is shown.
- **Setting Top/Bottom Filters** (Task C) to emphasize key parts of the dataset.
- **Creating and Leveraging Navigation Paths** (Task D) for a guided, drill-down user experience.
- **Filtering Data** (Task E) in the current tab to provide interactive, on-the-fly data exploration.

---