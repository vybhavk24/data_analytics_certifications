# IBM_c3_m2

## **Treemaps**, **Scatter Charts**, and **Histograms**

### **1️⃣ Treemaps**

### **What Are Treemaps?**

- **Purpose:** Treemaps display data that has a hierarchical structure as a set of nested rectangles.
- **How they work:** Each rectangle represents a category, and its size corresponds to a numerical value (for example, total sales). They’re especially useful when you want to compare parts within a whole.
- **Real-World Use:** If chocolate dataset has categories like **Chocolate Brand (Product)** with associated **Sales Amounts**, a treemap will show you which brands dominate the market by the size of the rectangle.

### **How to Create a Treemap in Excel (MacBook-Specific Steps)**

1. **Prepare your data:**
    
    Make sure your dataset has at least two columns—for example, `"Product"` and `"Total Sales Amount"`.
    
2. **Select your data:**
    
    Click and drag to select the range containing your chocolate brands and their corresponding sales amounts.
    
3. **Insert the Treemap:**
    - Go to the **Insert** tab.
    - Look for the **Hierarchy Charts** group.
    - Click on the **Treemap** icon.
4. **Customize your Treemap:**
    - Click on the chart to bring up **Chart Design** options.
    - Add **Data Labels** (via **Chart Design → Add Chart Element → Data Labels**) to show sales figures.
    - Edit the **Chart Title** by clicking on it and typing a new title (e.g., "Chocolate Sales by Brand").

### **2️⃣ Scatter Charts**

### **What Are Scatter Charts?**

- **Purpose:** Scatter charts (or scatter plots) are used to show the relationship between two numerical variables by displaying data as a collection of points.
- **How they work:** Each point represents a pair of values—for instance, the **Unit Price** and **Sales Amount (Amount and boxes shipped)** of a chocolate product. This helps you see if there’s a correlation (positive, negative, or none) between the two.
- **Real-World Use:** You can use a scatter chart to ask, “Do higher-priced chocolates tend to generate more sales revenue?” It visually reveals clusters, trends, or outliers.

### **How to Create a Scatter Chart in Excel (MacBook-Specific Steps)**

1. **Prepare your data:**
    
    For example, ensure your dataset has columns like `"Amount"` and `"Boxes shipped"`.
    
2. **Select your data:**
    
    Click and drag to select the numeric ranges for `Amount` (as the X-axis) and `Boxes shipped` (as the Y-axis).
    
3. **Insert the Scatter Chart:**
    - Go to the **Insert** tab.
    - In the **Charts** group, click on the **Scatter Chart** icon.
    - Choose the first option (Scatter with only Markers).
4. **Customize your Scatter Chart:**
    - Click on the chart to display the **Chart Design** and **Format** tabs.
    - Add **Axis Titles** via **Chart Design → Add Chart Element → Axis Titles**. For example, label the X-axis as "Unit Price" and the Y-axis as "Sales Amount."
    - Modify colors or add a trendline if needed to better visualize the relationship.

### **3️⃣ Histograms**

### **What Are Histograms?**

- **Purpose:** Histograms show the frequency distribution of a single numerical variable. They group data into bins (ranges) and display how many observations fall within each bin.
- **How they work:** Instead of plotting individual data points, a histogram aggregates data so you can see, for example, how many chocolate sales fall within certain price ranges.
- **Real-World Use:** Use a histogram to understand the distribution of **Sales Amounts**. Are most chocolate sales clustered in a particular range? This can provide insights into customer buying patterns.

### **How to Create a Histogram in Excel (MacBook-Specific Steps)**

1. **Prepare your data:**
    
    Ensure you have a numerical column such as `"Sales Amount"` in your Chocolate Sales Dataset.
    
2. **Select your data:**
    
    Click and drag to select the column with your sales figures.
    
3. **Insert the Histogram:**
    - Go to the **Insert** tab.
    - Look for the **Histogram** chart in the **Recommended Charts** or **Insert Statistic Chart** group.
    - Click on the **Histogram** icon.
4. **Customize your Histogram:**
    - Click on the chart to open the **Chart Design** options.
    - Adjust the **Bin Width** by right-clicking on the horizontal axis and selecting **Format Axis**. You can set a specific interval that makes sense for your sales figures.
    - Add **Data Labels** as needed for clarity.

### **Summary**

- **Treemaps:** Best for showing hierarchical data—visualize chocolate brands and their share of total sales.
- **Scatter Charts:** Ideal for exploring relationships between two variables—like unit price vs. sales amount.
- **Histograms:** Perfect for showing frequency distributions—understand the spread of chocolate sales amounts.

---

## **Filled Map Charts** and **Sparklines**

### **1. Filled Map Charts**

### **Concept Overview**

- **What They Are:**
    
    Filled Map Charts use geographic data (such as country or state names) to color‐shade regions on a map. The intensity or color of each region reflects the value of a numerical field—such as total sales or profit.
    
- **Why They Matter:**
    
    They provide a quick geographic overview of how your data varies by location. For example, you can instantly spot which countries or regions generate the highest sales, which is incredibly useful for strategic planning and regional performance analysis. In real‑world practice, managers use these maps to identify market strengths and geographic areas that may require more attention.
    

### **Practical Steps to Create a Filled Map Chart**

1. **Prepare Your Data:**
    - Ensure your dataset has a column with geographic information—in this example, the **Country** column.
    - Also verify there is a numerical column (like **Amount**) you want to visualize.
2. **Summarize Your Data (Optional but Recommended):**
    
    For a clear map, you may want to aggregate your data. For example, you can sum up the **Amount** for each country:
    
    - Create a **Pivot Table**:
        
        a. Click anywhere in your dataset.
        b. Go to **Insert → Pivot Table** and choose **New Worksheet**.
        c. In the PivotTable Fields pane, drag **Country** to the **Rows** and **Amount** to the **Values** (ensure it’s set to Sum).
        
3. **Insert the Filled Map Chart:**
    - With your summary (or original data) selected, go to the **Insert** tab.
    - Look for the **Map Chart** options. On modern Excel for Mac (Office 365 and later), you should see an option for **Filled Map**.
    - Click the **Filled Map** icon. Excel will generate a map and automatically color‑shade the geographic regions (based on the total sales for each country).
4. **Customize Your Filled Map Chart:**
    - Click on the **Chart Title** to edit it (e.g., "Total Sales by Country").
    - Use **Chart Design → Add Chart Element** to include or format elements such as the Legend or Data Labels.
    - If needed, adjust the colors by selecting **Chart Design → Change Colors** to ensure that differences between regions are clearly visible.

### **2. Sparklines**

### **Concept Overview**

- **What They Are:**
    
    Sparklines are tiny, word‑wrapped charts that fit entirely within a single cell. They give a quick, unobtrusive visual summary of data trends—such as upward or downward movements over time—without taking up much space.
    
- **Why They Matter:**
    
    They allow you to spot trends, spikes, or dips at a glance. For example, a sales manager could use sparklines next to each row of data in a table to observe the trend in monthly sales without having to create a full‑sized chart. This is especially powerful on dashboards where space is at a premium.
    

### **Practical Steps to Create Sparklines**

For this practice example, let’s assume you have aggregated monthly sales figures for a particular sales person (or you’ve arranged several cells in a row that represent a time‑series of data, such as sales figures for January through December).

1. **Prepare Your Data:**
    - Suppose you create a summary row (or use an existing one) with monthly sales figures.
    - For example, cells B2:M2 might contain the sales for each month for a given Sales Person.
2. **Insert the Sparkline:**
    - Select an empty cell where you’d like the sparkline to appear (say, cell N2).
    - Go to the **Insert** tab on the Ribbon.
    - In the **Sparklines** group, choose the type of sparkline you want—commonly **Line**, **Column**, or **Win/Loss**.
        - **Line Sparklines** are ideal for showing trends over time.
        - **Column Sparklines** can compare values across the period.
        - **Win/Loss Sparklines** work well when you only need to show performance as positive or negative.
    - In the dialog box that appears:
        - Under **Data Range**, select the range with your time‑series data (for example, `B2:M2`).
        - Ensure **Location Range** is set to the cell you selected (e.g., N2).
    - Click **OK**.
3. **Customize Your Sparkline:**
    - Once generated, select the sparkline cell (N2) and go to the **Sparkline Tools Design** tab.
    - Here you can change the style, adjust marker options (like highlighting high points, low points, or zeros), and modify the color.
    - If desired, drag the fill handle to copy the sparkline to additional rows if you have multiple rows of time‑series data.

---

## Summary of all charts:

| **Chart Type** | **Data Type/Kind** | **What It Represents** | **When/Where to Use It** |
| --- | --- | --- | --- |
| **Column Chart** | Categorical & numerical | Vertical bars that show the magnitude for each category | Comparing values (e.g., total sales by product category) |
| **Bar Chart** | Categorical & numerical | Horizontal bars; ideal for long category names | Comparing data across categories where labels are lengthy (e.g., sales by state or region) |
| **Line Chart** | Time series or continuous numeric data | Data points connected by straight or smooth lines to show trends over time | Visualizing trends over time (e.g., monthly or yearly sales trends) |
| **Pie Chart** | Parts of a whole (categorical percentages) | A circle divided into slices to depict proportional data | Showing percentage distribution (e.g., market share of different payment modes) |
| **Doughnut Chart** | Parts of a whole | Similar to a pie chart but with a hole in the center; can show multiple data series layers | Comparing proportions with a more modern look (e.g., multiple product category breakdowns) |
| **Area Chart** | Time series or continuous numeric data | Filled area under a line; highlights magnitude as well as trend | Emphasizing the volume of change over time or cumulative totals (e.g., cumulative sales over months) |
| **Scatter Chart** | Paired numeric values | Dots plotted along X and Y axes to reveal relationships or correlations | Investigating correlations (e.g., relationship between unit price and units sold) |
| **Bubble Chart** | Three-dimensional numeric data (X, Y, size value) | A variant of a scatter chart where the size of each marker represents a third variable | Visualizing multivariable relationships (e.g., unit price, quantity sold, and profit margin all in one visualization) |
| **Histogram** | Single numerical variable (continuous data) | Bars representing frequency counts across numeric bins | Analyzing the distribution or frequency of values (e.g., distribution of order amounts or sales figures) |
| **Treemap** | Hierarchical data with numeric values | Nested rectangles of varying sizes representing parts-to-whole relationships | Visualizing hierarchical data such as sales breakdown by brand and sub-category in a compact view |
| **Sunburst Chart** | Hierarchical data | Concentric rings displaying multi-level hierarchies | Showing multi-level category breakdowns (e.g., continent > country > state, or product category > sub-category > item) |
| **Waterfall Chart** | Sequential numeric data (with positive/negative variations) | Bars that show progressive increases and decreases | Financial data analysis (e.g., profit/loss changes over a period) or to illustrate step-by-step changes in values |
| **Funnel Chart** | Sequential data with decreasing values | A tapered chart representing a process where values shrink at each stage | Visualizing process pipelines or conversions (e.g., stages of a sales funnel) |
| **Map Chart (Filled Map)** | Geographical data paired with numeric values | A color-coded geographical map where regions are filled according to numeric intensity | Displaying regional, country, or state-based performance (e.g., sales by country) |
| **Stock Chart** | Financial time series (e.g., high, low, open, close prices) | Specialized charts (candlestick, line, high-low) for representing stock market data | Analyzing financial market trends such as stock prices or commodity prices |
| **Radar Chart** | Multivariate numeric data | A circular chart with spokes representing different variables; data plotted relative to a center point | Comparing multiple quantitative variables for a single item (e.g., performance metrics across different products) |
| **Combo Chart** | Mixed data types (multiple series with different scales) | Combines two or more chart types (e.g., line and column) in one chart to show relationships | When variables differ widely or to illustrate different aspects together (e.g., combining sales volume and profit margin trends in one chart) |
| **Box and Whisker Chart** | Statistical distribution data | Displays medians, quartiles, and outliers in a box-and-whisker format | Analyzing statistical spread, variability, and outliers in data (e.g., spread of order amounts or profit margins) |
| **Sparklines** | Time series data presented in a single cell | Miniature charts (line, column, win/loss) that show trends within a cell | Quick, compact trend visualization within tables or dashboards (e.g., showing the monthly sales trend for each sales representative in a summary table) |

**How to Use This Table:**

- **Data Type/Kind:** Indicates the nature of data required by each chart type.
- **What It Represents:** Explains the visual output and insight each chart provides.
- **When/Where to Use It:** Offers ideas on scenarios or business cases where the chart is most applicable.

---