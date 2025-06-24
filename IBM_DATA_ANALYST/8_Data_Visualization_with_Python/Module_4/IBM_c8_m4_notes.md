# IBM_c8_m4

## Dashboarding overview

### 1. What Is Dashboarding?

A **dashboard** is an organized, interactive user interface that consolidates data visualizations, metrics, and information from multiple sources in one place. Think of it as a command center that provides a bird’s-eye view of performance indicators and trends.

- **Components:**
Dashboards typically include charts (line, bar, pie, scatter, etc.), tables, key performance indicator (KPI) tiles, and sometimes even maps or gauges.
- **Interactivity:**
Modern dashboards allow users to filter data, change time ranges, drill down into details, and update visualizations on the fly.
- **Purpose:**
The goal is to empower users with the ability to quickly understand complex data and make informed decisions.

### 2. Why Use Dashboards?

- **Data Consolidation:**
Dashboards aggregate data from multiple sources (e.g., databases, CSV files, APIs) to provide a centralized overview.
- **Real-Time Updates:**
They can connect to live data streams to ensure that monitoring and analysis reflect the latest information.
- **Trend Monitoring:**
With integrated visualizations, dashboards help detect trends, seasonal patterns, and anomalies that might otherwise go unnoticed.
- **Enhanced Communication:**
Dashboards distill complex data into easily digestible visuals, making it simpler to communicate insights to stakeholders or team members.

### 3. Key Dashboard Design Principles

- **Simplicity and Clarity:**
A dashboard should be uncluttered. Use a minimalist layout, clear labels, and intuitive controls.
- **Relevance:**
Choose metrics and visualizations that directly support decision-making. Tailor the content to your audience’s needs.
- **Consistency:**
Use consistent color schemes, fonts, and layout patterns to avoid confusing users.
- **Interactivity:**
Incorporate filters, date pickers, and drill-down capabilities to enable users to explore the data in depth.
- **Responsive Design:**
Consider how your dashboard will look on various devices—desktop, tablet, or mobile.

### 4. Popular Dashboarding Tools & Frameworks

There are many dashboarding tools available, each with its own strengths:

### Commercial & Self-Service Tools

- **Tableau:**
Renowned for its robust, interactive dashboard capabilities and ease of use.
- **Power BI:**
A Microsoft tool that integrates deeply with other Office products.
- **Qlik Sense:**
Known for associative data indexing and user-driven exploration.

### Python-Based Tools

For a more customizable and code-driven approach, Python offers several libraries:

- **Dash (by Plotly):**
A popular framework for building interactive web-based dashboards using Flask, React, and Plotly.
- **Streamlit:**
An easy-to-use library that turns Python scripts into shareable web apps.
- **Panel (by HoloViz):**
Provides a high-level app and dashboarding solution for Python.

### 5. Building an Interactive Dashboard: A Sample with Dash

Let’s walk through a small example. We’ll assume your **SalesDataset** is already available (with columns such as *Order_Id*, *Amount*, *Profit*, *Category*, *Order_date*, etc.) and that you want to create a dashboard that shows sales trends, profit distribution, and a map of sales by region.

### A. Installation

Make sure you install the required libraries:

```bash
pip install dash dash-bootstrap-components pandas plotly
```

### B. Sample Code for a Dashboard

Below is a simple Dash app that includes a couple of interactive visualizations:

```python
import dash
import dash_bootstrap_components as dbc
from dash import html, dcc, Input, Output
import plotly.express as px
import pandas as pd

# Load SalesDataset
df = pd.read_csv('SalesDataset.csv')

# Data preprocessing: Convert order date to a datetime object if needed
df['Order Date'] = pd.to_datetime(df['Order Date'])

# Aggregate monthly sales for a time-series chart
df['Year-Month'] = df['Order Date'].dt.strftime('%Y-%m')
monthly_sales = df.groupby('Year-Month')['Amount'].sum().reset_index()

# Create a scatter plot for Profit vs. Amount
scatter_fig = px.scatter(df, x='Amount', y='Profit', color='Category', hover_data=['CustomerName'])

# Create a line chart for Monthly Sales
line_fig = px.line(monthly_sales, x='Year-Month', y='Amount', title='Monthly Sales Trend')

# Initialize the Dash app with a bootstrap theme for better aesthetics
app = dash.Dash(__name__, external_stylesheets=[dbc.themes.BOOTSTRAP])

# Layout of the dashboard
app.layout = dbc.Container([
    dbc.Row([
        dbc.Col(html.H2("Sales Dashboard Overview"), width=12)
    ], className='my-2'),
    dbc.Row([
        dbc.Col(dcc.Graph(figure=line_fig), width=12)
    ], className='my-2'),
    dbc.Row([
        dbc.Col(dcc.Graph(figure=scatter_fig), width=12)
    ], className='my-2'),
    dbc.Row([
        dbc.Col(html.Div("Additional KPI or controls can go here..."), width=12)
    ], className='my-2')
], fluid=True)

# Run the application
if __name__ == '__main__':
    app.run(debug=True)
```

**Explanation:**

- **Data Preprocessing:**
We prepare the SalesDataset by converting order dates and aggregating monthly sales.
- **Plotly Figures:**
Two figures are created—a line plot for overall sales trends and a scatter plot to analyze profit versus amount.
- **Dash Setup:**
Using Dash and Bootstrap, we arrange our visualizations in a responsive layout with rows and columns.
- **Interactivity Possibilities:**
Although the example is static, Dash easily supports additional components like dropdowns, sliders, and callbacks so that users can interact with the data (filter by date, category, etc.).

### 6. Real-World Use Cases

- **Business Monitoring:**
Track KPIs like sales, profit, and customer engagement to support daily decision-making.
- **Operational Efficiency:**
Monitor inventory levels, order fulfillment, and supply chain metrics in real time.
- **Financial Reporting:**
Consolidate financial and operational data into one screen for executive reviews.
- **Geospatial Analysis:**
Integrate maps (using libraries like Folium) for geographic visualizations of sales or customer distribution.

---

## Introduction to plotly

### 1. What Is Plotly?

**Plotly** is an interactive graphing library that uses modern web technologies like D3.js and WebGL to render plots in the browser. Unlike many static visualization libraries, Plotly allows users to zoom, pan, hover for details, and even dynamically update plots. This interactivity transforms data visualization from a passive experience into a dynamic exploration process.

Key points include:

- **Interactivity:**
    
    Plotly charts are interactive by default. You can hover over data points to reveal more information, zoom into regions of interest, and pan across the visualization.
    
- **Web-Based Rendering:**
    
    The library generates plots as HTML, meaning they can be easily embedded into web applications, dashboards, or Jupyter Notebooks.
    
- **Multiple Interfaces:**
    
    It includes high-level interfaces like **Plotly Express** for quick and efficient plotting, as well as a lower-level **graph_objects** module for fine-tuned control over every element of your plot.
    

### 2. Why Use Plotly?

Plotly is great for a variety of reasons:

- **Interactive Data Exploration:**
    
    With features like hover data, dynamic zooming, and interactive legends, Plotly makes it easy to explore complex datasets.
    
- **Ease of Use with Plotly Express:**
    
    For everyday tasks, Plotly Express provides one-line commands to generate many common chart types. It works directly with Pandas dataframes, which means you can go from data to interactive visualization in a single step.
    
- **Customization and Control:**
    
    For more complex use cases, the graph_objects module gives you granular control over the layout, styling, and behavior of every graphical element.
    
- **Integration Capabilities:**
    
    Plotly seamlessly integrates with web frameworks (such as Dash) and existing workflows, making it ideal for creating real-time dashboards and shared web applications.
    

### 3. Plotly Express vs. Plotly Graph Objects

### Plotly Express

- **High-Level API:**
Designed to create common graphs with minimal code.
- **Works Out-of-the-Box:**
Automatically infers axis labels, legends, and color scales based on your data.
- **Example Use-Cases:**
Scatter plots, line charts, bar charts, histograms, and more.

### Plotly Graph Objects

- **Low-Level, Flexible API:**
Provides full control of the visualization.
- **Customization:**
For modifying almost every element of the plot, including axes properties, annotations, and interactive components.
- **Use When:**
You need a custom layout or when combining multiple subplots and complex annotations.

### 4. Hands-On Examples

Let's illustrate some core features with practical examples using a hypothetical dataset—like our **SalesDataset** which might include columns such as *Amount*, *Profit*, *Category*, *Order_date*, etc.

### Example 1: Creating a Simple Line Chart with Plotly Express

Suppose we want to visualize the trend of sales over time.

```python
import plotly.express as px
import pandas as pd

# Load the SalesDataset (make sure the CSV file is in your working directory)
df = pd.read_csv('SalesDataset.csv')

# Assuming 'Year-Month' is a column in your dataset representing time
# For improved date handling, you may convert it using pd.to_datetime() if needed

fig = px.line(
    df,
    x='Year-Month',
    y='Amount',
    title='Sales Amount Over Time',
    labels={'Amount': 'Sales Amount', 'Year-Month': 'Date'},
    markers=True  # This adds markers at data points
)
fig.update_layout(xaxis_tickangle=-45)  # Rotate x-axis labels for clarity
fig.show()
```

**Explanation:**

- **px.line()**: Quickly creates a line chart with a default interactive toolbar.
- **Parameters:**
    - `x` and `y` specify the data columns.
    - `markers=True` displays markers at each data point, which can help in identifying individual observations.
- **Customization:**
The `update_layout` method is used to rotate the x-axis labels, enhancing readability.

### Example 2: Building an Interactive Scatter Plot

Here, we show how sales *Amount* relates to *Profit*, with different colors for each *Category*.

```python
fig = px.scatter(
    df,
    x='Amount',
    y='Profit',
    color='Category',      # Color points by category for additional insight
    hover_data=['CustomerName'],  # Display customer names upon hovering
    title='Sales Amount vs. Profit',
    labels={'Amount': 'Sales Amount', 'Profit': 'Profit'}
)
fig.update_traces(marker=dict(size=10, opacity=0.8))
fig.show()
```

**Explanation:**

- **px.scatter()**: Generates an interactive scatter plot that reveals additional dimensions through color and hover data.
- **Interactivity:**
Hovering over any point shows details like the customer name, enhancing data exploration.

### Example 3: Customizing a Bar Chart with Graph Objects

For those who need fine-grained control over their visualization, the graph_objects API is a powerful tool.

```python
import plotly.graph_objects as go

# Aggregate total profit by Category from the SalesDataset
category_profit = df.groupby('Category')['Profit'].sum().reset_index()

# Create a horizontal bar chart
fig = go.Figure(go.Bar(
    x=category_profit['Profit'],
    y=category_profit['Category'],
    orientation='h',
    marker=dict(color='rgba(58, 71, 80, 0.6)', line=dict(color='rgba(58, 71, 80, 1.0)', width=1))
))

fig.update_layout(
    title='Total Profit by Category',
    xaxis_title='Profit',
    yaxis_title='Category',
    yaxis=dict(autorange="reversed"),  # This reverses the y-axis so the highest value is on top
    template="plotly_white"
)
fig.show()
```

**Explanation:**

- **go.Bar():**
Defines a bar chart where you manually set attributes like orientation, marker color, and line width.
- **Update Layout:**
The `update_layout` method is used for setting titles, axis labels, and other stylistic elements.
- **Why Use Graph Objects?**
This approach gives you a complete control point which is beneficial for producing highly customized visualizations.

### 5. Advantages and Real-World Applications

- **Interactive Data Dashboards:**
Plotly charts can be embedded into interactive dashboards with frameworks like Dash, offering real-time data exploration.
- **Presentation-Ready Visuals:**
The crisp, professional appearance of Plotly makes it an excellent choice for presenting data insights to stakeholders.
- **Domain Versatility:**
Whether you’re in finance, marketing, healthcare, or any other field, Plotly's diverse chart types (from bubble charts to 3D scatter plots) allow you to visualize data in ways that reveal deeper insights.

---

## Plotly - scatter, line, bar, bubble, histogram, pie, sunburst

### 1. Scatter Plot

**Use case:** Examine the relationship between two continuous variables—for instance, how sales `Amount` and `Profit` relate, while distinguishing different product `Category` groups.

```python
import plotly.express as px
import pandas as pd

# Load SalesDataset (ensure the CSV is in your working directory)
df = pd.read_csv('SalesDataset.csv')

# Create a scatter plot: x-axis is Amount and y-axis is Profit.
# Markers are colored by Category, and hovering shows the CustomerName.
fig = px.scatter(
    df,
    x='Amount',
    y='Profit',
    color='Category',
    hover_data=['CustomerName'],
    title='Scatter Plot: Sales Amount vs. Profit'
)
fig.show()
```

**Explanation:**

- **Interactivity:** Hovering over points reveals additional info (customer names).
- **Color-coding:** Different colors represent distinct `Category` values, letting you spot group differences in one glance.

### 2. Line Plot

**Use case:** Visualize trends over time, like changes in sales `Amount` over different months recorded in `Year-Month`.

```python
fig = px.line(
    df,
    x='Year-Month',
    y='Amount',
    title='Line Plot: Sales Trend Over Time',
    labels={'Year-Month': 'Date', 'Amount': 'Sales Amount'},
    markers=True  # Adds data point markers for emphasis
)
fig.update_layout(xaxis_tickangle=-45)  # Rotate x-axis labels for readability
fig.show()
```

**Explanation:**

- **Trend visualization:** Easily observe growth, declines, or seasonal patterns in sales.
- **Customization:** Markers help pinpoint individual month values; rotating labels improves readability.

### 3. Bar Chart

**Use case:** Compare aggregated metrics across categories. For example, you might want to see total `Profit` by each product `Category`.

```python
# First aggregate profit by Category
category_profit = df.groupby('Category', as_index=False)['Profit'].sum()

fig = px.bar(
    category_profit,
    x='Category',
    y='Profit',
    title='Bar Chart: Total Profit by Category',
    labels={'Profit': 'Total Profit'}
)
fig.update_xaxes(tickangle=-45)
fig.show()
```

**Explanation:**

- **Aggregation:** Data is grouped by `Category` to sum up the profit so comparisons are meaningful.
- **Visual clarity:** A bar chart makes it simple to spot which categories are performing best.

### 4. Bubble Chart

**Use case:** Add an extra dimension to a scatter plot. Here, the marker size represents `Quantity` sold while plotting `Amount` vs. `Profit` and differentiating by `Category`.

```python
fig = px.scatter(
    df,
    x='Amount',
    y='Profit',
    size='Quantity',       # Bubble size shows Quantity sold
    color='Category',
    hover_data=['CustomerName'],
    title='Bubble Chart: Sales Data with Quantity'
)
fig.show()
```

**Explanation:**

- **Multidimensional visualization:** Each point encodes three dimensions: x (Amount), y (Profit), and marker size (Quantity).
- **Enhanced insight:** This chart helps reveal how order volume might be associated with profitability.

### 5. Histogram

**Use case:** Understand the distribution of a single variable—for example, the spread of sales `Amount`.

```python
fig = px.histogram(
    df,
    x='Amount',
    nbins=30,  # Adjust the number of bins for finer or coarser resolution
    title='Histogram: Distribution of Sales Amount',
    labels={'Amount': 'Sales Amount'}
)
fig.show()
```

**Explanation:**

- **Distribution insight:** A histogram breaks down the continuous variable into intervals (bins) so you can identify patterns such as skewness or outliers.
- **Customization:** Adjusting `nbins` helps tailor the chart to your data’s granularity.

### 6. Pie Chart

**Use case:** Illustrate proportions—such as the distribution of orders by `PaymentMode`.

```python
# First, count the occurrences for each PaymentMode
payment_counts = df['PaymentMode'].value_counts().reset_index()
payment_counts.columns = ['PaymentMode', 'Count']

fig = px.pie(
    payment_counts,
    values='Count',
    names='PaymentMode',
    title='Pie Chart: Payment Mode Distribution'
)
fig.show()
```

**Explanation:**

- **Proportional representation:** Each slice of the pie represents how frequently a particular payment mode appears, making it easy to see the dominant methods at a glance.
- **Interactivity:** Hover data shows exact counts, providing both an overview and details on demand.

### 7. Sunburst Chart

**Use case:** Depict hierarchical data. For example, illustrate the breakdown of sales `Amount` by `Category` and then by `Sub-category`.

```python
fig = px.sunburst(
    df,
    path=['Category', 'Sub-category'],  # Hierarchical levels
    values='Amount',
    title='Sunburst Chart: Sales Breakdown by Category and Sub-category'
)
fig.show()
```

**Explanation:**

- **Hierarchical insight:** The inner rings usually represent higher-level groups (e.g., Category) and the outer rings represent breakdowns (e.g., Sub-category).
- **Visual storytelling:** Sunburst charts can intuitively reveal the contribution of each subgroup to the overall total.

---

## Introduction to Dash

Dash is a Python framework developed by Plotly for building interactive, web-based dashboards and data applications entirely in Python. 

It abstracts away the complexity of web development—handling the intricacies of HTML, CSS, and JavaScript behind the scenes—so that you, as a data professional, can focus on creating compelling data visualizations and interactive reports.

### 1. What Is Dash?

- **Interactive Web Applications:**
    
    Dash lets you turn Python scripts into interactive web applications. The dashboards you create are rendered in the web browser and respond to user inputs in real time.
    
- **Built on Flask, Plotly, and React:**
    
    At its core, Dash uses Flask (a Python web framework) for the back-end, Plotly.js for interactive charts, and React for building dynamic user interfaces.
    
- **Pure Python:**
    
    You build your entire dashboard in Python. There is no need to write HTML, CSS, or JavaScript—unless you need very fine control.
    

### 2. Why Use Dash?

- **Rapid Prototyping:**
    
    Quickly go from idea to interactive dashboard without learning front-end development.
    
- **Seamless Plotly Integration:**
    
    Since Dash is built by Plotly, it integrates flawlessly with Plotly Express and Plotly Graph Objects, bringing you stunning, interactive visualizations.
    
- **Custom Interactivity with Callbacks:**
    
    Dash's callback system allows you to connect user inputs, like dropdown menus, sliders, or buttons, with your visualizations—dynamically updating graphs as users interact with your dashboard.
    
- **Ideal for Data-Driven Applications:**
    
    Use Dash for monitoring KPIs, exploring data, and presenting insights interactively.
    

### 3. Key Components of a Dash App

A Dash application is built around three core concepts:

1. **The App Layout:**
    
    This defines the structure and visual layout of your dashboard. Using Python components that correspond to HTML elements (via `dash.html` and `dash.dcc`), you arrange your graphs, text, and interactive widgets in a hierarchy.
    
2. **Dash Components:**
    
    Dash provides a suite of components (such as graphs, dropdowns, sliders, buttons, and inputs) that you can use to build your interface. Examples include:
    
    - `dcc.Graph` for displaying Plotly figures.
    - `dcc.Dropdown` for selections.
    - `dcc.Slider` for numeric or date selections.
    - `html.Div`, `html.H1`, etc., for structuring content.
3. **Callbacks:**
    
    Callback functions are what make your dashboard interactive. A callback links input components (like a dropdown change) to output components (like updating a graph). Dash’s decorator system (`@app.callback`) manages the communication between these elements.
    

### 4. A Simple Dash Example

Let’s create a basic dashboard that displays a line chart of sales over time. Assume your **SalesDataset** CSV has columns like `Year-Month` and `Amount`. This example shows how to set up a Dash app along with a simple callback.

### Step-by-Step Code Example

1. **Installation:**
    
    Make sure you have Dash and its dependencies installed:
    
    ```bash
    pip install dash dash-bootstrap-components pandas plotly
    ```
    
2. **Code Example:**
    
    Create a Python file (e.g., `app.py`) with the following content:
    
    ```python
    import dash
    import dash_bootstrap_components as dbc
    from dash import html, dcc, Input, Output
    import pandas as pd
    import plotly.express as px
    
    # Load the SalesDataset
    df = pd.read_csv('SalesDataset.csv')
    
    # Convert 'Year-Month' to a datetime if needed (or ensure it's in a proper format)
    # df['Year-Month'] = pd.to_datetime(df['Year-Month'])
    
    # Create aggregated data: monthly total sales for the line chart
    monthly_sales = df.groupby('Year-Month')['Amount'].sum().reset_index()
    
    # Create a simple Plotly Express line chart
    fig = px.line(monthly_sales, x='Year-Month', y='Amount', title='Monthly Sales Trend')
    fig.update_layout(xaxis_tickangle=-45)
    
    # Initialize the Dash app with a Bootstrap theme
    app = dash.Dash(__name__, external_stylesheets=[dbc.themes.BOOTSTRAP])
    
    # Define the layout of the app
    app.layout = dbc.Container([
        dbc.Row([
            dbc.Col(html.H2("Sales Dashboard Overview"), width=12)
        ], className='my-2'),
        dbc.Row([
            dbc.Col(
                dcc.Graph(id='line-chart', figure=fig),
                width=12
            )
        ], className='my-2'),
        dbc.Row([
            dbc.Col([
                html.Label("Select a Category:"),
                dcc.Dropdown(
                    id='category-dropdown',
                    options=[{'label': cat, 'value': cat} for cat in df['Category'].unique()],
                    value=df['Category'].unique()[0],
                    multi=False
                )
            ], width=4)
        ], className='my-2'),
        dbc.Row([
            dbc.Col(dcc.Graph(id='category-line-chart'), width=12)
        ], className='my-2')
    ], fluid=True)
    
    # Define callbacks to update graphs based on user input
    @app.callback(
        Output('category-line-chart', 'figure'),
        Input('category-dropdown', 'value')
    )
    def update_category_chart(selected_category):
        # Filter the dataset by the selected category
        filtered_df = df[df['Category'] == selected_category]
        category_monthly_sales = filtered_df.groupby('Year-Month')['Amount'].sum().reset_index()
        # Create a line chart for the selected category
        fig_category = px.line(category_monthly_sales, x='Year-Month', y='Amount',
                                 title=f'Monthly Sales Trend for {selected_category}')
        fig_category.update_layout(xaxis_tickangle=-45)
        return fig_category
    
    if __name__ == '__main__':
        app.run(debug=True)
    ```
    
    **Explanation:**
    
    - **Layout Definition:**
    The layout is set using Dash Bootstrap Component (`dbc.Container`) for a polished look. We have a header, a static overall line chart, a dropdown for category selection, and an initially empty graph for category-specific trends.
    - **Callback:**
    The callback function `update_category_chart` is triggered when the dropdown value changes. It filters the dataset by the selected category and updates the corresponding graph.
    - **Integration with Plotly:**
    We use Plotly Express to build our figures, ensuring interactivity like hover details and zooming.
    - **Running the App:**
    Running the script starts a local web server. Open the provided URL (usually `http://127.0.0.1:8050/`) in your browser to interact with your dashboard.

---

## Dash basics - HTML and Core components

1. **HTML Components (dash.html)** – which let you create standard HTML elements (like headings, paragraphs, divs, buttons, etc.) directly in Python.
2. **Core Components (dash.dcc)** – which provide higher-level interactive controls (like graphs, dropdowns, sliders, inputs, and more) that integrate with your data.

Both of these groups work together to build your app’s layout and interactivity without requiring you to write raw HTML or JavaScript.

### 1. HTML Components

Dash’s HTML components (available via `dash.html`) mimic standard HTML tags and let you build your page structure entirely in Python. In addition, you can pass any valid HTML properties as keyword arguments.

### Key Points:

- **Structure and Layout:**
Use components like `html.Div`, `html.H1`, `html.P`, `html.Button`, etc., to organize text, headings, images, or other elements into containers.
- **The `children` Property:**
Every HTML component in Dash accepts a `children` property. This property holds the element’s content (which could itself be another component, a list of components, or plain text).

### Examples of HTML Components:

- **`html.Div`**
A generic container that can be used for grouping other components.
- **`html.H1`, `html.H2`, ... `html.H6`**
Heading tags for titles and subtitles.
- **`html.P`**
Paragraph tags for text content.
- **`html.Button`**
Clickable buttons, which you can later bind to callbacks.

### Basic HTML Example:

```python
from dash import html

app_layout = html.Div([
    html.H1("Welcome to My Dashboard"),
    html.P("This dashboard is built entirely in Python using Dash."),
    html.Div([
        html.Button("Click Me", id="button-example", n_clicks=0)
    ], style={'padding': '20px', 'backgroundColor': '#f9f9f9'})
])
```

**Explanation:**

- The outer `html.Div` acts as the main container.
- `html.H1` displays the main heading.
- `html.P` displays a paragraph of text.
- The nested `html.Div` groups together a button which is later customizable via styles (like padding or background color).

### 2. Core Components

Dash Core Components (accessed via `dash.dcc`) provide interactive user interface elements such as graphs, dropdowns, sliders, and inputs. These components are highly integrated with Plotly for rendering interactive visualizations.

### Key Components:

- **`dcc.Graph`:**
Embed interactive Plotly charts into your dashboard.
- **`dcc.Dropdown`:**
Present a drop-down list allowing users to select one or more options.
- **`dcc.Input`:**
Accept user input as text or numeric data.
- **`dcc.Slider`:**
Let users select values along a numeric range.
- **`dcc.Checklist` or `dcc.RadioItems`:**
Allow for selection of options in various formats.

### Basic Core Components Example:

```python
from dash import dcc

core_components_layout = html.Div([
    dcc.Graph(
        id='example-graph',
        figure={
            'data': [
                {'x': [1, 2, 3, 4], 'y': [10, 15, 13, 17], 'type': 'line', 'name': 'Sales Trend'}
            ],
            'layout': {
                'title': 'Sales Over Time'
            }
        }
    ),
    html.Div([
        html.Label("Choose a Category:"),
        dcc.Dropdown(
            id='category-dropdown',
            options=[
                {'label': 'Electronics', 'value': 'electronics'},
                {'label': 'Fashion', 'value': 'fashion'},
                {'label': 'Home & Kitchen', 'value': 'home_kitchen'}
            ],
            value='electronics',  # default value
            clearable=False
        )
    ], style={'width': '50%', 'padding': '20px'})
])
```

**Explanation:**

- **`dcc.Graph`:**
    - Creates an interactive chart using Plotly.
    - The `figure` property is defined as a dictionary with keys for `data` and `layout`.
- **`dcc.Dropdown`:**
    - Displays a dropdown menu.
    - `options` is a list of dictionaries specifying the label (what the user sees) and the value (what is returned to your callbacks) for each choice.
    - The `value` property sets the default selected option.

### 3. Putting It All Together: A Simple Dash Layout

Now, let’s combine HTML and Core Components to create a complete simple Dash app layout.

```python
import dash
from dash import html, dcc

# Initialize the Dash app
app = dash.Dash(__name__)

# Define the app's layout using HTML and Core Components
app.layout = html.Div([
    # Title section with HTML components
    html.Div([
        html.H1("Sales Dashboard", style={'textAlign': 'center'}),
        html.P("An interactive dashboard built with Dash.", style={'textAlign': 'center'})
    ], style={'padding': '20px', 'backgroundColor': '#e8f4f8'}),

    # First section: Interactive Graph using dcc.Graph
    html.Div([
        dcc.Graph(
            id='sales-trend',
            figure={
                'data': [
                    {'x': ['2025-01', '2025-02', '2025-03', '2025-04'],
                     'y': [2500, 3000, 2800, 3200],
                     'type': 'line',
                     'name': 'Total Sales'}
                ],
                'layout': {
                    'title': 'Monthly Sales Trend'
                }
            }
        )
    ], style={'padding': '20px'}),

    # Second section: Dropdown for filtering example
    html.Div([
        html.Label("Select Product Category:"),
        dcc.Dropdown(
            id='product-category',
            options=[
                {'label': 'Electronics', 'value': 'Electronics'},
                {'label': 'Apparel', 'value': 'Apparel'},
                {'label': 'Home & Kitchen', 'value': 'Home & Kitchen'}
            ],
            value='Electronics'
        )
    ], style={'width': '50%', 'padding': '20px', 'margin': 'auto'})
])

# Run the Dash app
if __name__ == "__main__":
    app.run(debug=True)
```

**Step-by-Step Explanation:**

1. **App Initialization:**
    - `app = dash.Dash(__name__)` creates a new Dash application.
2. **Layout Overview:**
    - The entire layout is defined in a single outer `html.Div` component.
    - **Title section:**
    Uses `html.H1` and `html.P` to display a title and a descriptive paragraph. Styling (like text alignment and background color) is applied.
    - **Graph Section:**
    A `dcc.Graph` component displays a simple line chart. The figure is defined as a dictionary with both data and layout.
    - **Control Section:**
    A `dcc.Dropdown` is provided inside an `html.Div` (with `html.Label` for clarity) to allow users to select a product category. This component is styled for better presentation.
3. **Running the Dashboard:**
    - Finally, the `if __name__ == "__main__":` block starts the local server so you can view the dashboard in your browser (usually at `http://127.0.0.1:8050/`).

---

## Interactive dashboards - user inputs & callbacks

Below is an example that uses a sample SalesDataset. 

In this example, you’ll be able to select a product category (from a dropdown) and set a minimum sales threshold (via an input box). 

Based on these two inputs, a line chart is updated to show the monthly sales trend for the selected category filtered by the specified minimum sales amount.

### Step 1. Set Up Your Environment

Make sure you have the required packages installed:

```bash
pip install dash dash-bootstrap-components pandas plotly
```

### Step 2. Prepare Your Data

For this example, assume your CSV file (SalesDataset.csv) includes columns like:

- **Order_date**
- **Amount**
- **Category**

We’ll convert the order dates to a proper format and extract a “Year-Month” for grouping.

### Step 3. Create the Dash App with Interactive Components and Callbacks

Below is the complete code example:

```python
import dash
import dash_bootstrap_components as dbc
from dash import dcc, html, Input, Output
import pandas as pd
import plotly.express as px

# Load your SalesDataset
df = pd.read_csv('SalesDataset.csv')

# Convert Order_date to datetime & create a Year-Month column for grouping
df['Order_date'] = pd.to_datetime(df['Order_date'])
df['Year-Month'] = df['Order_date'].dt.strftime('%Y-%m')

# Initialize the Dash app with a Bootstrap theme for improved aesthetics
app = dash.Dash(__name__, external_stylesheets=[dbc.themes.BOOTSTRAP])

# Define the layout of the app using HTML and Core Components
app.layout = dbc.Container([
    dbc.Row([
        dbc.Col(html.H1("Interactive Sales Dashboard", style={'textAlign': 'center'}), width=12)
    ], className='my-3'),

    dbc.Row([
        dbc.Col([
            html.Label("Select Product Category:"),
            dcc.Dropdown(
                id='category-dropdown',
                options=[{'label': cat, 'value': cat} for cat in sorted(df['Category'].unique())],
                value=sorted(df['Category'].unique())[0],
                clearable=False
            )
        ], width=4),

        dbc.Col([
            html.Label("Minimum Sales Amount:"),
            dcc.Input(
                id='min-sales-input',
                type='number',
                placeholder='Enter minimum sales value',
                value=0
            )
        ], width=4)
    ], className='my-3'),

    dbc.Row([
        dbc.Col(
            dcc.Graph(id='line-chart'),
            width=12
        )
    ], className='my-3')
], fluid=True)

# Define the callback to update the line chart based on user inputs
@app.callback(
    Output('line-chart', 'figure'),
    Input('category-dropdown', 'value'),
    Input('min-sales-input', 'value')
)
def update_line_chart(selected_category, min_sales):
    """
    When the user selects a category and/or updates the minimum sales amount,
    this function filters the data accordingly, groups the sales by Year-Month,
    and creates an updated line chart.
    """
    # Filter the dataset by the selected category
    filtered_df = df[df['Category'] == selected_category]

    # Group data by Year-Month and sum the Amount
    grouped = filtered_df.groupby('Year-Month')['Amount'].sum().reset_index()

    # Apply minimum sales filtering: show only months above the specified threshold
    grouped = grouped[grouped['Amount'] >= min_sales]

    # Create a Plotly Express line chart
    fig = px.line(grouped, x='Year-Month', y='Amount',
                  title=f"Monthly Sales Trend for {selected_category}",
                  labels={'Amount': 'Total Sales Amount', 'Year-Month': 'Month'})

    # Rotate x-axis labels for clarity
    fig.update_layout(xaxis_tickangle=-45)
    return fig

# Run the Dash app
if __name__ == '__main__':
    app.run(debug=True)
```

### Explanation

1. **Data Preparation:**
    - The SalesDataset is loaded with Pandas.
    - The `Order_date` column is converted to a datetime object.
    - A new “Year-Month” column is created for grouping purposes.
2. **Layout:**
    - **HTML Components:**
    We use `html.H1` for the title and `html.Label` for field descriptions.
    - **Core Components:**
    A `dcc.Dropdown` lets the user choose a product category, and a `dcc.Input` (of type number) allows the user to specify a minimum sales threshold.
    - These components are organized using Dash Bootstrap Components (`dbc.Row` and `dbc.Col`) to ensure a responsive design.
3. **Callback:**
    - The `@app.callback` decorator defines a function `update_line_chart` that listens for changes in the dropdown (`category-dropdown`) and number input (`min-sales-input`).
    - When the input values change, the callback function filters the dataset by the selected category, groups it by the “Year-Month” column, applies the minimum sales filter, and generates a new line chart using Plotly Express.
    - The updated chart is returned and rendered in the `dcc.Graph` component with the id `line-chart`.
4. **Running the App:**
    - The script runs a local web server. When you navigate to the URL (commonly `http://127.0.0.1:8050/`), you'll see the interactive dashboard where selecting a different category or entering a minimum sales value updates the chart immediately.

---

###