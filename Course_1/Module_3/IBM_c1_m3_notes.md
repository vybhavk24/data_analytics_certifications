# IBM C1_M3

## Identifying data for analysis

### 1. What Does It Mean to Identify Data for Analysis?

At its core, identifying data for analysis is about **finding the right pieces of information** that will help answer a specific question or solve a problem. Imagine you're trying to understand why a retail store’s sales are fluctuating. Before analyzing the numbers, you need to first pinpoint what kinds of data could provide those answers:

- **Sales Data:** Daily or monthly sales figures.
- **Marketing Data:** Information on promotions or advertisements.
- **Customer Data:** Demographic details or purchasing behavior.
- **External Data:** Economic indicators or seasonal trends.

This process starts with a clear understanding of the problem you're solving. It’s similar to a detective deciding which clues are important to crack a case.

### 2. Key Steps in Identifying Data for Analysis

### A. **Define the Problem or Question**

- **Example:** A company wants to know why a certain product's sales dipped last quarter.
- **Tip:** Write down your key question(s). This helps in narrowing down what data is truly necessary.

### B. **List Potential Data Sources**

- **Internal Sources:** Company databases, CRM systems, point-of-sale systems.
- **External Sources:** Public datasets (like those from Kaggle or government websites), APIs, industry reports.
- **Exercise:** List out a hypothetical scenario. For instance:
    - **Problem:** "Understanding customer churn in a subscription service."
    - **Possible data sources:** Customer usage logs, support tickets, demographic info, and customer feedback surveys.

### C. **Evaluate Data Relevance and Quality**

- **Relevance:** Is the data directly related to your question?
- **Quality:** Is the data complete, accurate, and up-to-date?
- **Tip:** Data that’s missing a lot of entries or contains errors isn’t useful—even if it’s the only data you can get.
- **Exercise:** Think about the Titanic dataset. Does every feature (like passenger class, age, fare, etc.) contribute to answering a survival prediction question? Which ones might be more informative?

### D. **Consider the Structure and Format**

- **Structured Data:** Organized in rows and columns (e.g., spreadsheets, relational databases).
- **Unstructured Data:** Not as neatly organized (e.g., images, text data from social media).

---

## Data Sources

Data sources are the origins or “provenances” of the raw data that analysts, data scientists, or business professionals use to derive insights and make decisions. They encompass not just the location where the data is stored but also the methods by which the data is generated, collected, and maintained.

### **1. Primary vs. Secondary Data Sources**

- **Primary Data Sources:**
    
    These are data gathered directly from the source for a specific research purpose. Because they are collected firsthand, primary data tends to be highly relevant and tailored to your needs.
    
    - **Examples:** Surveys, interviews, direct observations, experiments, or sensor output (e.g., data collected from IoT devices).
- **Secondary Data Sources:**
    
    This refers to data that has already been collected by someone else for a different purpose and is then repurposed for analysis. While secondary data can be less expensive and quicker to obtain, it may need additional validation for relevance and quality.
    
    - **Examples:** Government databases, published reports, academic journals, industry white papers, or data extracted from websites.

*Primary sources offer direct, raw insights, while secondary sources provide interpreted or processed data that can enrich your analysis with historical or broader context.*

### **2. Internal vs. External Data Sources**

- **Internal Data Sources:**
    
    These are generated within an organization from day-to-day operations. They are typically stored in structured formats and managed through internal systems.
    
    - **Examples:** Enterprise applications like Customer Relationship Management (CRM) systems, Enterprise Resource Planning (ERP) systems, transactional databases, employee records, and operational logs.
- **External Data Sources:**
    
    These come from outside the organization and can offer complementary perspectives or additional context.
    
    - **Examples:** Public datasets (such as census data), market research, social media feeds, and third-party data providers offering information like Point-of-Sale records or weather data.

*Internal data is valuable for operational insights and performance tracking, while external data adds a layer of benchmarking and broader market context.*

### **3. Structured, Semi-Structured, and Unstructured Data Sources**

Data sources vary greatly in how they store information:

- **Structured Data Sources:**
    
    This type of data is neatly organized into relational tables with predefined schemas.
    
    - **Examples:** SQL databases (e.g., Oracle, MySQL, SQL Server), data warehouses, and even spreadsheets with consistent columns and rows.
- **Semi-Structured Data Sources:**
    
    Data that does not fit the rigid structure of relational databases but still contains organizational properties identifiable via tags or markers.
    
    - **Examples:** JSON files, XML documents, and logs that include timestamped events.
- **Unstructured Data Sources:**
    
    These contain information that doesn’t fit neatly into rows and columns and typically require more processing before analysis.
    
    - **Examples:** Free text from social media posts or articles, images, videos, and audio recordings.

*Knowing the data format is essential because it dictates the type of processing, cleaning, and transformation you’ll need to perform before analysis.*

### **4. Specialized Data Sources**

With modern analytics, additional specialized sources have arisen:

- **Machine-Generated Data:**
    
    Data produced by processes and systems such as server logs, system (or sensor) outputs, and IoT devices. This data is often time-stamped and voluminous.
    
- **Web Scraping and APIs:**
    
    Data obtained directly from the web using APIs or web scraping tools. For instance, extracting real-time sentiment from social media or market data from financial websites.
    
- **Big Data Ecosystems:**
    
    Datasets stored in distributed systems like data lakes, where data from various sources (structured, semi-structured, and unstructured) is collected for advanced analytics and machine learning.
    

---

## How to gather and import Data

### **1. Define Your Objectives and Identify Your Data Needs**

Before gathering any data, clearly outline what questions you want to answer or what problems you want to solve. This clarity will help you determine:

- **What type of data is required:** Are you looking for customer behavior information? Financial metrics? Sensor or IoT data?
- **Which variables or metrics matter:** Identify key indicators (e.g., sales figures, website traffic statistics, survey responses) that directly tie into your research or business objectives.

*For example, if you want to analyze customer purchasing behavior, you might need transactional data from your Point-of-Sale (POS) systems alongside demographic data from customer profiles.*

### **2. Identify Data Sources**

Data can be gathered from a variety of sources. They generally fall into a few broad categories:

### **Internal Sources**

- **Transactional Databases:**
Internal systems like CRMs, ERPs, or sales databases that store day-to-day business transactions.
- **Logs and Operational Data:**
Server logs, application performance data, or IoT sensors that provide insights into operational behavior.

### **External Sources**

- **Public Data Sets and Government Databases:**
Open data from governmental or international organizations (e.g., census data, economic indicators).
- **APIs and Web Services:**
Many online platforms (like Twitter, LinkedIn, financial markets, or weather services) offer APIs to access data programmatically.
- **Web Scraping:**
Extract relevant data from websites using scraping tools when direct APIs are unavailable.

*Tip:* Maintain a data inventory or catalog that lists all potential data sources, along with details about their format, frequency of updates, and access methods.

### **3. Methods for Gathering Data**

The method you choose to collect data depends on the source:

### **Direct Data Extraction from Databases or Files**

- **Exporting Files:**
    
    Many internal systems allow you to export data directly to CSV, Excel, or XML files.
    
    *Example:* Export daily sales records from your POS system as CSV files.
    
- **Using Database Queries:**
    
    Write SQL queries to extract data directly from relational databases like MySQL or PostgreSQL.
    
    ```sql
    SELECT customer_id, purchase_date, amount
    FROM sales_transactions
    WHERE purchase_date BETWEEN '2024-01-01' AND '2024-01-31';
    
    ```
    

### **APIs and Web Services**

- **Connecting via Code:**
Use libraries (e.g., Python’s `requests`) to make HTTP GET/POST requests.*Example in Python:*
    
    ```python
    import requests
    import pandas as pd
    
    # Make a GET request to an API endpoint
    response = requests.get("<https://api.example.com/data>")
    data = response.json()  # assuming the returned data is in JSON format
    
    # Convert JSON data into a DataFrame for analysis
    df = pd.DataFrame(data)
    print(df.head())
    
    ```
    

### **Web Scraping**

- **Scraping Data from Web Pages:**
Tools like BeautifulSoup (for parsing HTML) and Selenium (for dynamic pages) can be used to extract data.
    
    ```python
    from bs4 import BeautifulSoup
    import requests
    import pandas as pd
    
    url = '<https://example.com/data-page>'
    page = requests.get(url)
    soup = BeautifulSoup(page.content, 'html.parser')
    
    # Find and extract data items; this highly depends on the web page structure
    items = soup.find_all('div', class_='data-item')
    data_list = [item.text for item in items]
    
    # Convert the list into a DataFrame
    df = pd.DataFrame(data_list, columns=['Data'])
    print(df.head())
    
    ```
    

### **Surveys and Direct Collection**

- **Primary Data Methods:**
Use online survey tools like Google Forms or Qualtrics to gather information directly from respondents if primary, customized data is required.

### **4. Importing Data into Your Analytical Environment**

Once you’ve gathered the data from various sources, the next step is “importing” that data into your analysis tool of choice:

### **Using Python (Pandas)**

- **CSV Files:**
    
    ```python
    import pandas as pd
    
    # Import data from a CSV file
    df_csv = pd.read_csv('data/sales_data.csv')
    print(df_csv.head())
    
    ```
    
- **Excel Files:**
    
    ```python
    # Import data from an Excel file with multiple sheets
    df_excel = pd.read_excel('data/customer_data.xlsx', sheet_name='Sheet1')
    print(df_excel.head())
    
    ```
    
- **JSON Files:**
    
    ```python
    # Import data from a JSON file
    df_json = pd.read_json('data/data.json')
    print(df_json.head())
    
    ```
    

### **Using R**

- **CSV Files:**
    
    ```r
    # Import data from a CSV file in R
    df_csv <- read.csv("data/sales_data.csv")
    head(df_csv)
    
    ```
    
- **Excel Files:**
    
    ```r
    # Import data from an Excel file using the 'readxl' package
    library(readxl)
    df_excel <- read_excel("data/customer_data.xlsx", sheet = "Sheet1")
    head(df_excel)
    
    ```
    

### **Connecting Directly to Databases**

- **Python (using SQLAlchemy):**
    
    ```python
    from sqlalchemy import create_engine
    import pandas as pd
    
    # Create a connection to a PostgreSQL database
    engine = create_engine('postgresql://username:password@localhost:5432/mydatabase')
    
    # Query data directly
    query = "SELECT * FROM sales_transactions WHERE region = 'North America'"
    df_db = pd.read_sql(query, engine)
    print(df_db.head())
    
    ```
    
- **R (using RPostgres):**
    
    ```r
    library(RPostgres)
    
    # Establish a connection
    con <- dbConnect(RPostgres::Postgres(), dbname = 'mydatabase',
                     host = 'localhost', port = 5432,
                     user = 'username', password = 'password')
    
    # Execute a query
    df_db <- dbGetQuery(con, "SELECT * FROM sales_transactions WHERE region = 'North America'")
    head(df_db)
    dbDisconnect(con)
    
    ```
    

---

## Data wrangling

Data wrangling—often called data munging or data remediation—is the process of transforming raw, unorganized data into a clean and structured format that’s ready for analysis. 

It’s an essential step in the data analytics pipeline because even the most advanced models or visualizations can only be as reliable as the data fed into them.

### **1. The Purpose of Data Wrangling**

- **Improving Data Quality:**
    
    Raw data is often messy. It may include missing values, duplicates, inconsistencies, and irrelevant details. Data wrangling cleans and standardizes the data so that it reflects accurate and consistent information.
    
- **Enhancing Usability:**
    
    By transforming data into a more organized and structured format, data wrangling makes it easier for analysts to work with the data, whether that’s for statistical analysis, machine learning, or generating reports.
    
- **Ensuring Relevance:**
    
    Data wrangling helps in selecting the appropriate subsets of data, enriching it (by combining different sources if necessary), and discarding noise. This ensures that downstream analyses actually address your research or business questions.
    

### **2. Key Stages in the Data Wrangling Process**

**a. Discovery:**

In this initial phase, you explore the data to understand its nature, scope, and potential issues. This step involves:

- **Identifying Data Sources:** Determining where the data is coming from (internal systems, public datasets, APIs, web scraping, etc.).
- **Assessing Data Quality:** Evaluating the data for accuracy, completeness, and consistency.
- **Defining Objectives:** Establishing what you want to achieve with the data, which helps guide how you’ll clean and transform it.

**b. Data Cleaning:**

Here, you correct or eliminate erroneous data points. Common tasks include:

- **Handling Missing Data:** Filling in missing values with appropriate substitutions or removing incomplete records.
- **Correcting Inconsistencies:** Standardizing formats (like dates, addresses, or categorical labels) to maintain uniformity.
- **Removing Duplicates and Outliers:** Ensuring that duplicate records or anomalous values do not skew the analysis.

**c. Data Transformation:**

This stage restructures data into a format that is suitable for analysis. It can involve:

- **Normalization and Denormalization:** Organizing data into a coherent structure (like transforming a flat file into a relational format or vice versa) according to the analysis needs.
- **Aggregation:** Summarizing data—such as computing totals or averages—to provide higher-level insights.
- **Enrichment:** Integrating additional data sources to provide context or depth—for instance, adding socioeconomic data to customer information.

**d. Data Validation and Verification:**

After cleaning and transforming, it’s crucial to verify that the data is:

- **Accurate:** Correctly reflects reality.
- **Consistent:** Free from logical errors, ensuring relationships between data attributes are maintained.
- **Complete:** Contains all necessary information for your analysis.

### **3. Benefits of Data Wrangling**

- **Higher Quality Insights:**
    
    Clean and well-structured data leads to more reliable analysis, reducing the risk of drawing incorrect conclusions.
    
- **Improved Efficiency:**
    
    Investing time in data wrangling at the start saves time later in the analysis phase, as reliable data simplifies modeling and visualization.
    
- **Better Decision Making:**
    
    When data is accurate and easy to interpret, the insights you generate are directly aligned with the truth of the underlying phenomena, bolstering confidence in business or research decisions.
    

### **4. Tools and Techniques**

Data wrangling can be performed manually or with automated tools, such as:

- **Scripting Languages:**
    - **Python:** Using libraries like Pandas for data cleaning, transformation, and aggregation.
    - **R:** Utilizing packages like dplyr and tidyr for similar tasks.
- **Data Wrangling Platforms:**
Tools like Trifacta, Talend, or even cloud services offered by AWS or Microsoft Azure provide graphical interfaces to streamline the wrangling process.
- **Spreadsheets:**
For smaller datasets, Excel or Google Sheets can be very effective in cleaning and organizing data.

---

## Tools for Data wrangling

Data wrangling tools are software solutions or libraries that help you clean, transform, and prepare raw data for analysis.

### **1. Scripting Libraries and Languages**

For many data professionals, writing custom scripts is the most flexible and powerful way to tackle data wrangling tasks. These tools are widely used because they allow for fine control over transformation logic:

- **Python Libraries:**
    - **Pandas:**
    Perhaps the most popular library for data manipulation and cleaning, Pandas provides data structures like DataFrames that allow you to filter, merge, aggregate, and reshape datasets efficiently.
    - **NumPy:**
    While primarily used for numerical computations, NumPy underpins many data transformations in Python.
    - **PySpark:**
    For scaling up to big data, PySpark provides a DataFrame API similar to Pandas but distributed over a cluster, which is essential when handling massive datasets.
- **R Packages:**
    - **dplyr and tidyr:**
    In R, packages like dplyr (for data transformation and manipulation) and tidyr (for reshaping and cleaning data) are key to effective data wrangling.

*These libraries provide the scripting power that many data analysts favor for their reproducibility and customization capabilities, but they require programming expertise.*

### **2. Interactive, No-Code/Low-Code Platforms**

If you prefer a graphical, drag-and-drop approach or need to empower non-technical users, several platforms provide robust data wrangling capabilities without requiring extensive coding skills:

- **Trifacta (by Google):**
    
    Known for its intuitive interface and smart, algorithm-driven recommendations for cleaning and structuring data, Trifacta Wrangler enables users to visually transform and prepare data.
    
- **Alteryx:**
    
    A versatile analytics platform that not only supports data wrangling with a user-friendly drag-and-drop interface but also integrates data blending and advanced analytics functions.
    
- **Talend:**
    
    Talend offers robust ETL capabilities along with data quality tools. With its visual interface, you can design data workflows that extract, transform, and load (ETL) data from numerous sources.
    
- **Microsoft Power Query (Excel/Power BI):**
    
    Integrated within Excel and Power BI, Power Query lets you import, clean, integrate, and reshape data using an interactive interface, making it accessible to business users.
    

*Such platforms are especially popular for their ease of use and speed in connecting to various data sources, often including pre-built connectors for common databases or file formats.*

### **3. ETL and Data Integration Tools**

Data wrangling is sometimes integrated into broader ETL (Extract, Transform, Load) processes. These tools often provide end-to-end solutions to collect, cleanse, and load data into warehouses or analytics environments:

- **Informatica:**
    
    A well-established ETL tool that automates data cleansing, transformation, and integration, making it easier to bring diverse data into a consistent format.
    
- **AWS Glue and Azure Data Factory:**
    
    Cloud-based ETL platforms that offer serverless data wrangling and integration, scalable for large volumes of data.
    

*These ETL tools are ideal if you need to build reliable, repeatable data pipelines where data wrangling is a crucial step along the way.*

### **4. Specialized Open-Source Tools**

For specific data cleaning tasks or if you’re operating on a lower budget, there are several open-source tools aimed at simplifying data wrangling:

- **OpenRefine:**
    
    A powerful, browser-based tool that helps you clean messy data, transform it from one format to another, and even extend it with web services and external data.
    
- **DataWrangler (now integrated into Trifacta Wrangler):**
    
    Initially developed as an interactive tool for quick data transformations, its concepts continue to live on in modern, interactive platforms.
    

*Open-source tools like these are often favored in academic or exploratory settings where flexibility and community support are paramount.*

---

## Data cleaning

Data cleaning, often referred to as data cleansing or data scrubbing, is the process of detecting, correcting, or removing errors and inconsistencies in raw data to improve its quality before analysis.

### **Why Data Cleaning Matters**

- **Improved Accuracy:**
    
    Errors, duplicates, and missing values can skew analysis. By cleaning data, you ensure that conclusions and predictive models are built on an accurate foundation. This increases confidence in the insights derived from the data, leading to better-informed strategies and decisions .
    
- **Enhanced Efficiency:**
    
    Investing time in cleaning data upfront reduces the troubleshooting and rework needed later in the analysis process. In addition, many data cleaning tools and libraries help automate repetitive cleaning tasks, thereby boosting overall productivity .
    
- **Regulatory Compliance:**
    
    Clean data helps organizations adhere to data governance standards, minimizing potential legal or compliance issues that might arise from reporting inaccurate or incomplete information .
    

### **Key Steps in the Data Cleaning Process**

1. **Data Assessment:**
    
    Begin by exploring your dataset to identify quality issues. This involves checking for:
    
    - **Missing values:** Identifying absent or incomplete entries.
    - **Duplicates:** Removing redundant records.
    - **Inconsistencies:** Detecting and correcting variations in data formats (such as date formats, unit conventions, or category names).
    - **Outliers or Errors:** Recognizing and handling values that deviate significantly from the norm, which may indicate data entry errors or genuine anomalies that need special treatment.
2. **Data Correction:**
    
    Once issues are identified, the cleaning process involves:
    
    - **Imputation:** Filling in missing values using statistical methods (e.g., mean, median, mode) or predictive modeling.
    - **Normalization:** Standardizing data formats so that similar information is represented consistently.
    - **Deduplication:** Removing duplicate entries to prevent biases in the analysis.
3. **Data Transformation and Enrichment:**
    
    In some cases, raw data may need to be reshaped or enriched. This can involve:
    
    - **Restructuring data:** For example, pivoting or melting datasets to match the desired analysis format.
    - **Integrating external data:** Merging additional information (such as demographic data) to provide context and depth to the analysis.
4. **Validation and Verification:**
    
    Finally, the cleaned data is validated to ensure that:
    
    - All known issues have been addressed.
    - The data now meets the quality criteria required for reliable analysis.

### **Tools and Techniques for Data Cleaning**

Discussed above.

---

## Data preparation and reliability

**Data Preparation and Reliability** encompasses all the processes that turn raw, unrefined data into a high-quality, structured, and trustworthy dataset ready for analysis and decision-making.

### **1. Data Preparation**

**Definition:**

Data preparation involves the series of processes that collect, clean, transform, and enrich raw data, making it suitable and effective for downstream analytics, modeling, or reporting. It is often also known as data pre-processing.

**Key Steps in Data Preparation:**

1. **Data Collection:**
    - **Source Identification:**
    Data can come from internal systems (e.g., transactional databases, logs, CRMs) or external sources (e.g., government datasets, APIs, web scraping).
    - **Data Ingestion:**
    Data is gathered into a centralized place—whether in files, databases, or data lakes—for further processing.
2. **Data Discovery and Profiling:**
    - **Understanding Data Characteristics:**
    This step involves exploring the data to understand its size, structure, formats, and inherent issues. It includes identifying missing values, outliers, duplicates, and inconsistencies.
    - **Assessment for Quality Issues:**
    Data profiling techniques help to assess if the data adheres to the expected standards so that anomalies can later be corrected.
3. **Data Cleaning:**
    - **Handling Missing or Incomplete Data:**
    This might involve imputation (filling missing values) or removing records that fall short of quality standards.
    - **Correcting Inconsistencies and Errors:**
    Standardizing data formats (like dates or categorical labels), removing duplicates, and correcting inaccuracies to ensure consistency across the dataset.
    - **Outlier Treatment:**
    Evaluating outliers to decide whether to remove them (if they’re errors) or to handle them cautiously if they might hold important analytical value.
4. **Data Transformation and Integration:**
    - **Restructuring Data:**
    Often, data must be reshaped (for instance, pivoting from long to wide format or vice versa) to become analyzable.
    - **Merging Data:**
    Combining various data sources into one cohesive dataset—for example, joining sales data with customer demographic data.
    - **Feature Engineering:**
    Creating or transforming variables that may be more predictive or useful in further analysis.
5. **Data Validation and Publication:**
    - **Quality Assurance:**
    The processed data goes through rigorous validation checks for consistency, accuracy, and completeness.
    - **Documentation:**
    Maintaining detailed metadata (data dictionaries, provenance, transformation logs) to support transparency and reproducibility.

*The entire process ensures that by the time analysis begins, the data is not only clean and structured but also fully aligned with the original business or research questions.*

### **2. Ensuring Data Reliability**

**Data Reliability** refers to the degree to which the data is consistent, accurate, and trustworthy over time. Reliable data underpins effective decision-making because analytics and models built upon it are more likely to reflect true insights.

**Key Factors and Practices for Data Reliability:**

1. **Consistency in Data Collection:**
    - **Standardized Procedures:**
    Establish and enforce data collection protocols to minimize errors and variations in how data is gathered.
    - **Automation:**
    Automating the collection process (for example, through APIs, ETL pipelines, or streaming tools) can reduce human error and ensure timeliness.
2. **Rigorous Cleaning and Validation:**
    - **Automated Quality Checks:**
    Using scripts or dedicated tools (like Python’s Pandas, R’s tidyverse, or platforms like OpenRefine) to automate repetitive quality checks.
    - **Iterative Review:**
    Regularly verify data against known benchmarks or through cross-validation to catch errors as they arise.
3. **Documentation and Transparency:**
    - **Data Provenance:**
    Tracking data sources, and documenting all modifications through metadata and logs ensures every change is verifiable.
    - **Auditing:**
    Performing periodic audits to confirm that all data preparation processes maintain the reliability of the data.
4. **Feedback Loops:**
    - **Monitoring Changes Over Time:**
    Setting up processes to monitor the reliability of incoming data helps to alert analysts when significant changes or degradation in quality occur.
    - **User Feedback:**
    Allowing domain experts or end users to provide feedback on data quality can highlight issues that automated systems may miss.

---

## Summary:

Transformation of raw data includes the tasks you undertake to:

- Structurally manipulate and combine the data using Joins and Unions.
- Normalize data, that is, clean the database of unused and redundant data.
- Denormalize data, that is, combine data from multiple tables into a single table so that it can be queried faster.
- Clean data, which involves profiling data to uncover quality issues, visualizing data to spot outliers, and fixing issues such as missing values, duplicate data, irrelevant data, inconsistent formats, syntax errors, and outliers.
- Enrich data, which involves considering additional data points that could add value to the existing data set and lead to a more meaningful analysis.