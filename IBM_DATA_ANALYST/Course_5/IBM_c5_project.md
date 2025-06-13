# IBM_c5_Project

Notebook - IBM_c5_project

```tsx
!pip install yfinance
!pip install bs4
!pip install nbformat
!pip install --upgrade plotly
```

### **!pip install yfinance**

📦 Installs the yfinance library, which allows you to:

- Download historical stock prices
- Get real-time stock info
- Access data from Yahoo Finance easily

🔧 Example:

```
import yfinance as yf
apple = yf.Ticker("AAPL")
```

### **!pip install bs4**

📦 Installs **BeautifulSoup4**, a library used for **web scraping** HTML content.

You use this when you want to:

- Parse HTML pages
- Extract table data or text from tags like <table>, <div>, <p>, etc.

## **!pip install nbformat**

📦 Installs nbformat, a tool used for **working with Jupyter Notebook files** programmatically.

It allows Python code to:

- Create .ipynb files
- Read and write cells
- Modify notebook structure

You don’t often use it directly unless you’re writing code that handles .ipynb files.

## **!pip install --upgrade plotly**

📦 Installs or **updates** Plotly — a **powerful graphing library** for interactive charts and dashboards.

You use it for:

- Line charts
- Bar charts
- Interactive plots
- Dashboards (like the one in this stock analysis project!)

🔧 Example:

```
import plotly.express as px
px.line(data, x="Date", y="Close")
```

---

```tsx
import plotly.io as pio
pio.renderers.default = "iframe"
```

### **import plotly.io as pio**

- plotly.io is Plotly’s **input/output** module.
- It gives you control over how and where **plots get shown** (e.g., in notebook, browser, file, etc.).
- pio is just a short name for it, so you don’t have to type plotly.io every time.

### **pio.renderers.default = "iframe"**

This sets the **default renderer** to "iframe".

### **✅ What does this mean?**

When you make a Plotly chart, it needs to know **how to show the chart**. Options include:

- "notebook" – shows inline in a Jupyter notebook
- "browser" – opens chart in your web browser
- "iframe" – embeds chart in a little scrollable frame

By setting it to "iframe":

- All charts will display inside a mini embedded HTML frame.
- This is useful in environments where regular notebook rendering might not work.

### **🧪 Example:**

```
import plotly.express as px
fig = px.line(x=[1, 2, 3], y=[10, 20, 15])
fig.show()  # This will now open in an iframe
```

### **✅ Summary**

| **Line** | **What it does** |
| --- | --- |
| import plotly.io as pio | Loads Plotly’s rendering controls |
| pio.renderers.default = "iframe" | Sets display style to iframe (embedded view) |

---

```tsx
import warnings
# Ignore all warnings
warnings.filterwarnings("ignore", category=FutureWarning)
```

### **import warnings**

This imports Python’s built-in **warnings module**.

- This module lets you **control or ignore warning messages** that appear during code execution.
- Warnings are not errors — they just inform you that something might change or be risky in the future.

### **warnings.filterwarnings("ignore", category=FutureWarning)**

This tells Python:

> “Please ignore any warning that is a
> 
> 
> **FutureWarning**
> 

### **🔸 What is a FutureWarning ?**

A FutureWarning usually means:

- “This feature might change or stop working in the future version of Python or a library.”
- For example: *“In future versions of pandas, this function will behave differently.”*

### **🧠 Why ignore it?**

- These warnings don’t affect your project **right now**.
- They’re often **annoying clutter** in your output.
- Hiding them makes your notebook look **cleaner and easier to read**, especially when presenting or submitting.

### **✅ Summary**

| **Line** | **Meaning** |
| --- | --- |
| import warnings | Access warning control tools |
| warnings.filterwarnings("ignore", category=FutureWarning) | Hide any future-related warning messages |

---

```tsx
def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"), vertical_spacing = .3)
    stock_data_specific = stock_data[stock_data.Date <= '2021-06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), y=stock_data_specific.Close.astype("float"), name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), y=revenue_data_specific.Revenue.astype("float"), name="Revenue"), row=2, col=1)
    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
    fig.update_layout(showlegend=False,
    height=900,
    title=stock,
    xaxis_rangeslider_visible=True)
    fig.show()
    from IPython.display import display, HTML
    fig_html = fig.to_html()
    display(HTML(fig_html))
```

### **🔧 Function Name and Inputs**

```
def make_graph(stock_data, revenue_data, stock):
```

This defines a **function** called make_graph that takes in:

1. stock_data: stock price data (like from yfinance)
2. revenue_data: revenue data (usually scraped or downloaded)
3. stock: a string like "Apple" or "Tesla" to use as the title

### **🎯 Create Subplots**

```
fig = make_subplots(
    rows=2, cols=1,
    shared_xaxes=True,
    subplot_titles=("Historical Share Price", "Historical Revenue"),
    vertical_spacing = .3
)
```

This creates a Plotly chart with **2 rows, 1 column**, and **shared X-axis** (time):

- Row 1 → Share Price
- Row 2 → Revenue
- vertical_spacing adjusts space between the two plots

### **🧹 Filter Data**

```
stock_data_specific = stock_data[stock_data.Date <= '2021-06-14']
revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
```

You’re slicing the data:

- Only keep stock data **before June 14, 2021**
- Only keep revenue data **before April 30, 2021**

This ensures both datasets are aligned for a fair visual comparison.

### **📈 Add Stock Price Line Plot**

```
fig.add_trace(
    go.Scatter(
        x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True),
        y=stock_data_specific.Close.astype("float"),
        name="Share Price"
    ),
    row=1, col=1
)
```

This adds a **line chart** of the closing stock price to **Row 1**:

- Converts date strings to actual datetime objects
- Converts closing price values from text to float numbers

### **💰 Add Revenue Line Plot**

```
fig.add_trace(
    go.Scatter(
        x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True),
        y=revenue_data_specific.Revenue.astype("float"),
        name="Revenue"
    ),
    row=2, col=1
)
```

This adds another line plot to **Row 2** using the revenue data.

### **🏷️ Axis Titles**

```
fig.update_xaxes(title_text="Date", row=1, col=1)
fig.update_xaxes(title_text="Date", row=2, col=1)
fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
```

- Adds appropriate axis labels to both subplots for clarity

### **🎨 Final Layout Settings**

```
fig.update_layout(
    showlegend=False,
    height=900,
    title=stock,
    xaxis_rangeslider_visible=True
)
```

- showlegend=False hides legends (can simplify look)
- height=900 makes the plot tall enough to see clearly
- title=stock sets the title using the company name
- xaxis_rangeslider_visible=True adds a cool interactive range slider under the graph

### **🖼️ Show the Plot + Export HTML**

```
fig.show()
from IPython.display import display, HTML
fig_html = fig.to_html()
display(HTML(fig_html))
```

- fig.show() displays the graph inside your notebook
- fig.to_html() converts the chart into HTML format
- display(HTML(...)) renders it so it looks beautiful in the notebook

### **✅ Summary**

| **Part** | **What it Does** |
| --- | --- |
| make_subplots | Creates 2-row chart: Stock + Revenue |
| add_trace | Adds each plot line |
| update_xaxes/yaxes | Adds axis labels |
| update_layout | Customizes chart appearance |
| fig.show() | Displays interactive dashboard |

---

Using the Ticker function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is TSLA.

```tsx
tesla = yf.Ticker("TSLA")
```

Using the ticker object and the function history extract stock information and save it in a dataframe named tesla_data. Set the period parameter to "max" so we get information for the maximum amount of time.

```tsx
tesla_data = tesla.history(period="max")
```

Reset the index using the reset_index(inplace=True) function on the tesla_data DataFrame and display the first five rows of the tesla_data dataframe using the head function. 

Take a screenshot of the results and code from the beginning of Question 1 to the results below.

```tsx
tesla_data.reset_index(inplace=True)

tesla_data.head()
```

---

Use the requests library to download the webpage:

[https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm) 

Save the text of the response as a variable named html_data.

```tsx
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
response = requests.get(url)
html_data = response.text
```

Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`.

```tsx
soup = BeautifulSoup(html_data, "html.parser")
```

Using `BeautifulSoup` or the `read_html` function extract the table with `Tesla Revenue` and store it into a dataframe named `tesla_revenue`. 

The dataframe should have columns `Date` and `Revenue`.

```tsx
# Extract all tables from the soup object
tables = pd.read_html(str(soup))  # Convert soup back to string

# Look for the Tesla Revenue table
for table in tables:
    if "Tesla Quarterly Revenue" in table.columns or table.columns[0] == "Date":
        tesla_revenue = table
        break

# Rename columns (if needed)
tesla_revenue.columns = ["Date", "Revenue"]
```

Using BeautifulSoup or the read_html function extract the table with Tesla Revenue and store it into a dataframe named tesla_revenue. The dataframe should have columns Date and Revenue.

Here are the step-by-step instructions:

1. Create an Empty DataFrame
2. Find the Relevant Table
3. Check for the Tesla Quarterly Revenue Table
4. Iterate Through Rows in the Table Body
5. Extract Data from Columns
6. Append Data to the DataFrame

Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab

soup.find_all("tbody")[1]

If you want to use the read_html function the table is located at index 1

We are focusing on quarterly revenue in the lab.

```tsx
import pandas as pd
from bs4 import BeautifulSoup

# Step 1: Create an empty DataFrame
tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])

# Step 2: Find all <tbody> tags and choose the second one, which contains the Tesla revenue table
table_body = soup.find_all("tbody")[1]

# Step 3–6: Loop through each row and extract the data
for row in table_body.find_all("tr"):
    columns = row.find_all("td")
    
    # Check if there are exactly 2 columns (Date and Revenue)
    if len(columns) == 2:
        date = columns[0].text.strip()
        revenue = columns[1].text.strip()
        
        # Step 6: Append to DataFrame
        tesla_revenue = pd.concat([tesla_revenue, pd.DataFrame({"Date": [date], "Revenue": [revenue]})], ignore_index=True)
```

Display the last 5 row of the tesla_revenue dataframe using the tail function.

Take a screenshot of the results.

```tsx
tesla_revenue.tail()
```

---

Using the Ticker function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is GME.

```tsx
gme = yf.Ticker("GME")
```

Using the ticker object and the function history extract stock information and save it in a dataframe named gme_data. Set the period parameter to "max" so we get information for the maximum amount of time.

```tsx
gme_data = gme.history(period="max")
```

Reset the index using the reset_index(inplace=True) function on the gme_data DataFrame and display the first five rows of the gme_data dataframe using the head function. 

Take a screenshot of the results and code from the beginning of Question 3 to the results below.

```tsx
gme_data.reset_index(inplace=True)

gme_data.head()
```

Use the requests library to download the webpage:

 [https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html). 

Save the text of the response as a variable named html_data_2.

```tsx
# URL of the GameStop revenue data page
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"

# Download the page content and store as text
html_data_2 = requests.get(url).text
```

Parse the html data using beautiful_soup using parser i.e html5lib or html.parser.

```tsx
soup_2 = BeautifulSoup(html_data_2, "html.parser")
```

Using BeautifulSoup or the read_html function extract the table with GameStop Revenue and store it into a dataframe named gme_revenue.

The dataframe should have columns Date and Revenue. Make sure the comma and dollar sign is removed from the Revenue column.

```tsx
import pandas as pd

# Step 1: Create an empty DataFrame
gme_revenue = pd.DataFrame(columns=["Date", "Revenue"])

# Step 2: Locate the table (2nd <tbody> — index 1)
table_body = soup_2.find_all("tbody")[1]

# Step 3: Loop through each row in the table
for row in table_body.find_all("tr"):
    cols = row.find_all("td")
    if len(cols) == 2:  # Ensure the row has both Date and Revenue
        date = cols[0].text.strip()
        revenue = cols[1].text.strip()

        # Step 4: Clean the revenue data — remove '$' and ',' 
        revenue = revenue.replace('$', '').replace(',', '')

        # Step 5: Append to DataFrame
        gme_revenue = pd.concat(
            [gme_revenue, pd.DataFrame({"Date": [date], "Revenue": [revenue]})],
            ignore_index=True
        )
```

Display the last five rows of the gme_revenue dataframe using the tail function

```tsx
gme_revenue.tail()
```

---

Use the make_graph function to graph the Tesla Stock Data, also provide a title for the graph. Note the graph will only show data upto June 2021.

```tsx
make_graph(tesla_data, tesla_revenue, 'Tesla')
```

Gives an error coz $ sign is still visible in Revenue of Tesla:

Cleaning the graph before plotting.

```tsx
def make_graph(stock_data, revenue_data, stock):
    # Clean Revenue column: remove '$' and ',' and drop rows with missing data
    revenue_data["Revenue"] = revenue_data["Revenue"].str.replace("$", "").str.replace(",", "")
    revenue_data.dropna(inplace=True)
    
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"), vertical_spacing=0.3)
    
    stock_data_specific = stock_data[stock_data.Date <= '2021-06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']

    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date), y=stock_data_specific.Close.astype("float"), name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date), y=revenue_data_specific.Revenue.astype("float"), name="Revenue"), row=2, col=1)

    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)

    fig.update_layout(showlegend=False, height=900, title=stock, xaxis_rangeslider_visible=True)
    fig.show()
```

```tsx
make_graph(tesla_data, tesla_revenue, 'Tesla')
```

Use the make_graph function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the make_graph function is make_graph(gme_data, gme_revenue, 'GameStop'). Note the graph will only show data upto June 2021.

```tsx
make_graph(gme_data, gme_revenue, 'GameStop')
```

---