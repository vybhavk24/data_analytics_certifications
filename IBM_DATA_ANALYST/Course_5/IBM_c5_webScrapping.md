# IBM_c5_webScrapping

## Intro to web scrapping:

### **Why Web Scraping?**

Web scraping is useful in various fields, including:

- **Market Research:** Track competitor prices, product availability, and trends.
- **Data Journalism:** Gather statistics or reports from multiple sources.
- **Financial Analysis:** Scrape stock prices, economic indicators, or earnings reports.
- **Academic Research:** Extract scientific publications, census data, or social trends.
- **News Aggregation:** Automatically collect and organize articles from different sources.

### **How Web Scraping Works**

A web scraper follows these steps:

1. **Send a Request:** Access a webpage using HTTP (via Python's `requests` library).
2. **Retrieve the HTML:** Download the webpage’s content.
3. **Parse the Data:** Extract specific elements using a parser like BeautifulSoup or lxml.
4. **Store and Process:** Save the extracted data in structured formats like CSV, JSON, or databases.

### **Essential Tools for Web Scraping**

- **`requests`** – Downloads web pages.
- **BeautifulSoup (`bs4`)** – Parses HTML and XML.
- **Scrapy** – A powerful framework for large-scale scraping.
- **Selenium** – Automates browsers to handle dynamic JavaScript content.
- **Pandas** – Cleans and stores scraped data in tabular formats.

### **Basic Web Scraping Example (Using Requests & BeautifulSoup)**

```python
import requests
from bs4 import BeautifulSoup

url = "<https://example.com>"
response = requests.get(url)

if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")

    # Extract all headings
    headings = soup.find_all("h1")
    for heading in headings:
        print(heading.get_text().strip())

    # Extract links
    links = soup.find_all("a")
    for link in links:
        print(f"Text: {link.get_text()}, URL: {link.get('href')}")
else:
    print("Failed to retrieve webpage")
```

### **Legal and Ethical Considerations**

Before scraping a website:

- **Check `robots.txt`** – Many sites specify scraping permissions in their `robots.txt` file.
- **Respect Terms of Service** – Some websites prohibit automated scraping.
- **Be Kind to Servers** – Avoid excessive requests; use delays and rate limits.
- **Do Not Scrape Sensitive or Private Data** – Ensure compliance with data protection laws.

---

## HTML for web scrapping:

### **1. Basics of HTML**

HTML (HyperText Markup Language) structures web content using **tags** that define elements like headings, paragraphs, tables, and links. Here’s a simple example:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sample Web Page</title>
  </head>
  <body>
    <h1>Welcome to Web Scraping!</h1>
    <p>This paragraph contains some data.</p>
    <a href="<https://example.com>">Click Here</a>
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
    </ul>
    <table>
      <tr>
        <th>Name</th>
        <th>Age</th>
      </tr>
      <tr>
        <td>Alice</td>
        <td>25</td>
      </tr>
      <tr>
        <td>Bob</td>
        <td>30</td>
      </tr>
    </table>
  </body>
</html>
```

### **Key HTML Elements for Scraping**

- **`<h1>`, `<h2>`, `<h3>` ...** → Headings
- **`<p>`** → Paragraphs
- **`<a href="URL">`** → Hyperlinks
- **`<ul>`, `<li>`** → Lists
- **`<table>`, `<tr>`, `<td>`** → Tables
- **`<div>` and `<span>`** → Containers for styling and organization

These elements help structure content, making it easier to extract.

### **2. Inspecting HTML Structure**

When scraping a webpage, first inspect its HTML using browser **developer tools**:

- Right-click anywhere on the page and select **"Inspect"** (Chrome, Edge, Firefox).
- Identify the **CSS classes, IDs, and element tags** that contain the data you need.

### **3. Using BeautifulSoup to Parse HTML**

Python’s **BeautifulSoup** library makes HTML parsing easy. Below is a basic example of how to extract headings, paragraphs, links, and tables.

### **Installation**

```bash
pip install beautifulsoup4 requests
```

### **Extracting Data from HTML**

```python
import requests
from bs4 import BeautifulSoup

# Fetch HTML content
url = "<https://example.com>"
response = requests.get(url)

if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")

    # Extract headings
    headings = soup.find_all("h1")
    for h in headings:
        print("Heading:", h.get_text())

    # Extract paragraphs
    paragraphs = soup.find_all("p")
    for p in paragraphs:
        print("Paragraph:", p.get_text())

    # Extract links
    links = soup.find_all("a")
    for link in links:
        print("Link:", link.get("href"))

    # Extract table data
    table_rows = soup.find("table").find_all("tr")
    for row in table_rows:
        columns = row.find_all("td")
        print([col.get_text() for col in columns])
else:
    print("Failed to retrieve the page")
```

### **Explanation:**

- **Requests Module** → Fetches HTML content from a webpage.
- **BeautifulSoup** → Parses the content and lets you search by tags (`find_all`).
- **Extracting Elements** → `find_all("tag")` gets all occurrences of a tag.

### **4. Handling Dynamic Content**

Some websites generate content dynamically using **JavaScript** (e.g., infinite scrolling, interactive elements). If standard scraping doesn't work:

- **Selenium** → Automates browsers to extract fully rendered pages.
- **Requests-HTML** → Handles JavaScript rendering.

For example, using Selenium:

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("<https://example.com>")
html = driver.page_source  # Get fully rendered HTML
driver.quit()
```

### **5. Best Practices & Ethics**

- **Check `robots.txt`** → Some sites restrict scraping.
- **Respect Terms of Service** → Avoid violating usage policies.
- **Use Rate Limiting** → Avoid overloading servers with requests.
- **Be Transparent** → If scraping public data, inform users where it's from.

---

## **Web Scraping Using BeautifulSoup**

### 1. What Is BeautifulSoup?

BeautifulSoup is a Python library designed for quick turnaround projects like screen-scraping. It constructs a parse tree from page source (HTML or XML) which makes it easy to extract and manipulate data. With BeautifulSoup, you can:

- Search for elements by tag, attribute, or text.
- Navigate between parents, children, and siblings.
- Use CSS selectors via the `.select()` method.
- Clean or modify the parsed HTML.

It works well with parsers such as Python’s built-in `"html.parser"` or more powerful ones like `"lxml"` (if installed).

### 2. Installation

Before you start scraping, you need to install BeautifulSoup (and usually the `requests` library to fetch pages):

```bash
pip install beautifulsoup4 requests
```

You can also install an additional parser like `lxml` for faster parsing:

```bash
pip install lxml
```

### 3. Basic Usage

### a. Fetching the HTML Content

Most web scraping starts by downloading the raw HTML content from a webpage. The `requests` library is perfect for this:

```python
import requests

url = "<https://example.com>"
response = requests.get(url)

if response.status_code == 200:
    html_content = response.text
else:
    print("Failed to retrieve website. Status code:", response.status_code)
```

### b. Parsing HTML with BeautifulSoup

Once you have the HTML content, create a BeautifulSoup object to parse it:

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object with the HTML and a parser.
soup = BeautifulSoup(html_content, "html.parser")  # You can also use "lxml" if installed.
```

### 4. Navigating the DOM and Extracting Data

BeautifulSoup provides several methods and attributes to navigate and search the HTML DOM.

### a. Finding Elements

### **Finding a Single Element**

Use the `.find()` method to return the first matching element.

```python
title_tag = soup.find("title")
print("Page Title:", title_tag.get_text())
```

### **Finding All Matching Elements**

Use `.find_all()` to return a list of elements that match.

```python
# Extract all headings (e.g., h1 tags)
headings = soup.find_all("h1")
for heading in headings:
    print("Heading:", heading.get_text().strip())
```

### b. Using CSS Selectors

The `.select()` method allows you to use CSS selectors, which is powerful when elements have specific classes or IDs.

```python
# Select all elements with the class "article"
articles = soup.select(".article")
for article in articles:
    # Using get_text() to extract the text content.
    print(article.get_text().strip())
```

### c. Accessing Attributes and Text

You can retrieve the attributes of an element using the `.get()` method and its text content using `.get_text()`.

```python
# Extract hyperlinks (<a> tags)
links = soup.find_all("a")
for link in links:
    text = link.get_text().strip()
    url = link.get("href")
    print(f"Link Text: {text}, URL: {url}")
```

### d. Navigating the Tree

BeautifulSoup allows you to move through the DOM tree by accessing children, parents, and siblings.

```python
first_paragraph = soup.find("p")
if first_paragraph:
    # Get parent element (e.g., maybe a <div> that wraps the paragraph)
    parent = first_paragraph.parent
    print("Parent tag:", parent.name)

    # Iterate over all sibling tags
    for sibling in first_paragraph.next_siblings:
        # sibling could be a string (e.g., whitespace) – check using .name
        if sibling.name:
            print("Sibling tag:", sibling.name)
```

### 5. Complete Example: Extracting Data from a Sample Page

Imagine you want to extract the page title, all the headings, and all hyperlinks from a webpage. Here’s how you might put it all together:

```python
import requests
from bs4 import BeautifulSoup

def scrape_page(url):
    try:
        # Step 1: Download the page
        response = requests.get(url, timeout=10)
        response.raise_for_status()
    except requests.RequestException as e:
        print(f"Error fetching URL: {e}")
        return

    # Step 2: Parse the HTML content with BeautifulSoup
    soup = BeautifulSoup(response.text, "html.parser")

    # Step 3: Extract the title
    title = soup.find("title")  # Find the <title> element
    if title:
        print("Page Title:", title.get_text().strip())
    else:
        print("Title not found.")

    # Step 4: Extract all <h1> headings
    headings = soup.find_all("h1")
    print("\\nHeadings:")
    for heading in headings:
        print("-", heading.get_text().strip())

    # Step 5: Extract all hyperlinks
    links = soup.find_all("a")
    print("\\nLinks:")
    for link in links:
        link_text = link.get_text().strip()
        link_href = link.get("href")
        print(f"- {link_text} -> {link_href}")

# Example usage:
scrape_page("<https://example.com>")
```

### Explanation:

- **Error Handling:**
We use try-except to catch network errors or bad responses.
- **Parsing:**`"html.parser"` is sufficient for most needs; switch to `"lxml"` for speed if available.
- **Data Extraction:**
We extract the title, headings, and links by navigating the DOM with `.find()` and `.find_all()`.
- **Output:**
The script prints the extracted elements, ready for further processing or storage.

### 6. Best Practices

- **Inspect the Target Page:**
Use your browser's developer tools (right-click and "Inspect") to understand the structure of the page.
- **Respect Website Policies:**
Check the site’s `robots.txt` and terms of service.
- **Rate Limiting:**
Add delays between requests (e.g., using `time.sleep()`) if scraping multiple pages.
- **Error Handling:**
Handle HTTP errors and connection issues gracefully.
- **Dynamic Content:**
For JavaScript-heavy pages, consider integrating Selenium or Requests-HTML to allow the page to render before extraction.

---

## **Extracting Stock Data Using a Python Library:**

Notebook → Extracting_data.ipynb

```tsx
!pip install yfinance
!pip install matplotlib
```

### **!pip install yfinance**

### **✅ What it does:**

- This line **installs** the yfinance library.
- yfinance allows you to **download stock market data** from Yahoo Finance.

### **🧠 What’s happening:**

- pip is Python’s package manager. Think of it like the Play Store or App Store, but for Python tools.
- The ! at the start tells **Jupyter Notebook** to run this command like you would in a terminal/command line.
- You’re saying: *“Hey Python, please install the yfinance library so I can use it in my notebook!”*

### **📦 Why yfinance?**

Because you’ll use it to **get real-time and historical stock data** for your analysis.

### **!pip install matplotlib**

### **✅ What it does:**

- This line installs the matplotlib library.
- matplotlib is used to **create graphs and charts** in Python.

### **🧠 What’s happening:**

- Again, pip install is used to download and set up the package.
- matplotlib will help you **visualize** your stock performance — for example, plotting stock price trends over time.

| **Line** | **What it installs** | **Why it’s useful** |
| --- | --- | --- |
| !pip install yfinance | A tool to get stock market data | You’ll use it to pull stock prices |
| !pip install matplotlib | A graphing tool | You’ll use it to make charts and dashboards |

---

```tsx
import yfinance as yf
import pandas as pd
```

### **import yfinance as yf**

### **✅ What it does:**

- This **brings the yfinance library into your code**, so you can use its features.
- You’re giving it a **short nickname**: yf. So every time you want to use it, you just write yf instead of yfinance.

### **🧠 Real-world example:**

Imagine you’re carrying a big toolbox named “yfinance”. But that name is long, so you tell your team:

> “Hey, let’s call this toolbox just yf from now on so it’s quicker to use.”
> 

### **🛠️ Why it matters:**

You’ll soon write code like yf.Ticker("AAPL") to fetch Apple stock data. This line is setting you up for that.

### **import pandas as pd**

### **✅ What it does:**

- This imports the **pandas** library, which is used for **handling and analyzing data**.
- Just like before, you’re giving it a short name: pd.

### **🧠 What is pandas?**

Think of pandas as **Excel for Python** — but way more powerful. It helps you:

- Create and manage tables (called DataFrames)
- Filter, sort, and analyze data
- Clean messy data
- Handle large datasets easily

### **🛠️ Why it matters:**

You’ll soon use pandas to organize your stock data into **rows and columns**, just like a spreadsheet.

| **Line** | **What it does** | **Why it matters** |
| --- | --- | --- |
| import yfinance as yf | Loads the stock data tool | You’ll use it to fetch stock prices |
| import pandas as pd | Loads the data-handling tool | You’ll organize and analyze data with it |

---

```tsx
apple = yf.Ticker("AAPL")
```

### **apple = yf.Ticker("AAPL")**

Let’s break it down slowly:

### **✅ What’s happening?**

- You are creating a **Ticker object** for the company **Apple Inc.**
- yf.Ticker("AAPL") tells Python:
    
    > “Go to Yahoo Finance and grab everything you know about the stock symbol AAPL (which stands for Apple Inc.).”
    > 
- You’re **saving** that information into a variable called apple.

### **🧠 Beginner Explanation:**

- Think of yf.Ticker("AAPL") like searching for “Apple stock” on Yahoo Finance.
- But instead of opening a browser, Python does it for you silently and quickly behind the scenes.
- The result is a **Python object** with **all of Apple’s financial data**, like:
    - Stock prices
    - Company info
    - Historical charts
    - Earnings, dividends, etc.

### **🗃️ What is apple now?**

It’s a **custom object** that stores all of Apple’s stock info.

You can now do cool things like:

```
apple.info           # Basic company info
apple.history()      # Historical stock prices
apple.dividends      # Dividend history
```

| **Part** | **Meaning** |
| --- | --- |
| yf.Ticker("AAPL") | Fetches Apple stock data |
| apple = ... | Saves that data into a variable called apple |

---

```tsx
%pip install wget
import wget
```

### **%pip install wget**

### **✅ What it does:**

- This installs the **wget** package in your Jupyter Notebook environment.
- It lets you **download files from the internet directly into your notebook**, just like how a browser downloads files.

### **🧠 Why %pip instead of !pip ?**

- %pip is a **Jupyter magic command** — it’s specially designed to work inside notebooks.
- It ensures the package is installed in the **same environment** as your notebook’s Python kernel.

✅ Both !pip and %pip install packages, but %pip is **more notebook-safe**. It’s preferred in Jupyter.

### **import wget**

### **✅ What it does:**

- This loads the wget package into your code so you can start using it.
- You only need to install a package **once**, but you need to import it every time you use it in a new notebook or session.

### **🧠 Real-life analogy:**

- %pip install wget = downloading a new app to your phone.
- import wget = opening the app to start using it.

### **✅ What you’ll use wget for:**

In this project, wget is typically used to:

- **Download datasets** (like a CSV file of stock prices) from a URL
- Store them in your working folder so you can analyze them with pandas

Example usage:

```
wget.download("https://somewebsite.com/stockdata.csv")
```

| **Line** | **What it does** | **Why it’s needed** |
| --- | --- | --- |
| %pip install wget | Installs wget | So you can download files from the internet |
| import wget | Loads it into your code | So you can use it to fetch files |

---

```tsx
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json

Error: zsh:1: command not found: wget

So i tried:

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json"
wget.download(url, "apple.json")
```

### **🔹 1. The original line:**

```
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json
```

### **✅ What this line was trying to do:**

- This is a **terminal command**, using wget from your **system**, not Python.
- It tells the computer:
    
    > “Hey system, download this file from the internet using the wget tool.”
    > 

### **❌ Why you got this error:**

> zsh:1: command not found: wget
> 
- Your **Mac** (which uses zsh as the terminal shell) doesn’t have wget installed **as a system tool**.
- So when Jupyter tried to run !wget, it couldn’t find it and gave that error.

### **🔹 2. The alternative (your solution):**

```
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json"
wget.download(url, "apple.json")
```

### **✅ What this does:**

- You’re now using **Python’s wget library**, which you installed earlier via %pip install wget.
- This downloads the file from the web and **saves it as apple.json** in your working folder.

### **🧠 Explanation for beginners:**

| **Line** | **What it means** |
| --- | --- |
| url = "..." | Save the web link into a variable called url |
| wget.download(url, "apple.json") | Use Python’s wget to download the file at that link and save it as apple.json |

This is 100% the **Pythonic way** to download files when the system command wget is unavailable.

| **Line** | **What it was meant for** | **Problem** | **Fix** |
| --- | --- | --- | --- |
| !wget <url> | Use system’s wget to download file | Your system doesn’t have wget installed | ✅ Use wget.download(url) from Python instead |

---

```tsx
import json
with open('apple.json') as json_file:
    apple_info = json.load(json_file)
       
    print("Type:", type(apple_info)) #prints variable type
apple_infoPerfect — now you’re working with **JSON files**, which are super common in data science and web development. Let’s explain each line like you’re new to both Python **and** data formats.
```

### **import json**

### **✅ What it does:**

- Loads Python’s built-in **json** module.
- This module lets you **read and write JSON data** in Python.

### **🧠 What is JSON?**

- **JSON** stands for *JavaScript Object Notation*.
- It’s a **way to store structured data** — like dictionaries and lists.
- Looks like this:

```
{
  "name": "Apple Inc.",
  "symbol": "AAPL",
  "price": 195.56
}
```

So json helps you load this into Python as a normal dictionary.

### **with open('apple.json') as json_file:**

### **✅ What it does:**

- This **opens** the file named apple.json so Python can read it.
- with makes sure the file is safely opened and automatically closed when you’re done.

### **🧠 Real-world analogy:**

- Think of open() like opening a book.
- The with block ensures the book is **closed** properly when you’re done — even if something goes wrong.

### **apple_info = json.load(json_file)**

### **✅ What it does:**

- Reads the contents of apple.json and **converts** it into a Python dictionary.
- Stores that dictionary in a variable called apple_info.

### **🧠 Simple version:**

This line says:

> “Take the data from this JSON file and load it into Python as a dictionary called apple_info.”
> 

### **# print("Type:", type(apple_info))**

- This line (if uncommented) would print the **type** of the variable apple_info.
- You’d see:

```
Type: <class 'dict'>
```

- 
- That means the data is now stored as a **Python dictionary** — like this:

```
{
  "country": "USA",
  "sector": "Technology",
  ...
}
```

### **🔹**

### **apple_info**

- This line **displays the contents** of apple_info in your Jupyter Notebook.
- Since this is the last line in the cell, Jupyter automatically prints the variable’s value — just like how a calculator shows the result of a sum.

| **Line** | **What it does** |
| --- | --- |
| import json | Loads the JSON-handling tool |
| with open(...) | Opens the file safely |
| json.load(...) | Reads the file and converts it into a Python dictionary |
| apple_info | Shows you the loaded data |

---

```tsx
apple_info['country']
```

### **apple_info['country']**

### **✅ What it does:**

- This line **accesses the “country” field** inside the apple_info dictionary.

### **🧠 Step-by-step:**

- Earlier, you loaded the JSON file into apple_info, which is now a Python **dictionary** (key-value pairs).
- That dictionary might look like this:

```
{
    "symbol": "AAPL",
    "country": "USA",
    "sector": "Technology",
    ...
}
```

- So this line says:
    
    > “Give me the value stored under the key 'country'.”
    > 

### **📥 Output:**

- It will return:

```
'USA'
```

### **💡 Concept learned:**

- You now know how to **access dictionary values** in Python:

```
dict_variable['key_name']
```

---

```tsx
apple_share_price_data = apple.history(period="max")
```

### **apple_share_price_data = apple.history(period="max")**

### **✅ What it does:**

- This fetches the **entire history of Apple’s stock prices** from Yahoo Finance and saves it in a new variable called apple_share_price_data.

### **🧠 Step-by-step:**

- apple is the ticker object you created earlier using yf.Ticker("AAPL").
- apple.history() is a **method** (or function) that gets the **historical price data**.
- period="max" means:
    
    > “Give me all the data available — from the oldest to the most recent.”
    > 

### **⏳ What kind of data is returned?**

- A **pandas DataFrame** — like a table.
- It includes columns like:
    - Open, High, Low, Close, Volume, Dividends, etc.
- Example:

```
            Open   High    Low   Close   Volume
Date
1980-12-12  0.12   0.13   0.12   0.13    4690336
1980-12-15  0.13   0.15   0.13   0.15    17588400
...
```

### **💡 Concepts learned:**

- How to **call a method** on an object in Python: object.method()
- How to fetch and store **tabular data** in pandas
- How to deal with **time series data** (rows indexed by date)

| **Line** | **What it does** |
| --- | --- |
| apple_info['country'] | Gets the country Apple is based in — 'USA' |
| apple.history(period="max") | Downloads Apple’s full stock price history from Yahoo |

---

```tsx
apple_share_price_data.head()
```

### **apple_share_price_data.head()**

### **✅ What it does:**

- This line shows you the **first 5 rows** of the apple_share_price_data table.

### **🧠 Why use .head() ?**

When you load a big dataset, it can have **thousands of rows** (Apple has been public since the 1980s!).

So instead of printing the whole table, you use .head() to just **peek at the top** — like checking the cover page and table of contents of a book.

### **📊 Example Output:**

Let’s say the first few rows look like this:

| **Date** | **Open** | **High** | **Low** | **Close** | **Volume** | **Dividends** | **Stock Splits** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1980-12-12 | 0.51 | 0.54 | 0.51 | 0.51 | 47281600 | 0.0 | 0.0 |
| 1980-12-15 | 0.52 | 0.53 | 0.51 | 0.52 | 20985600 | 0.0 | 0.0 |
| … | … | … | … | … | … | … | … |

Each row is for one trading day, and each column is a piece of data for that day.

### **✅ By default:**

- .head() shows **5 rows**.
- But you can specify how many rows you want:

```
apple_share_price_data.head(10)  # shows 10 rows
```

### **🧠 Concepts Learned:**

| **Concept** | **Explanation** |
| --- | --- |
| Method | .head() is a DataFrame method |
| Default argument | Shows 5 rows unless you specify a number |
| Data exploration | It’s a good first step to understand your data |

---

```tsx
apple_share_price_data.reset_index(inplace=True)
```

### **apple_share_price_data.reset_index(inplace=True)**

### **✅ What it does:**

This line **moves the Date column** (which was the row index before) **back into the table as a normal column.**

### **📊 Before this line:**

When you did .head(), your table probably looked like this:

| **Date** | **Open** | **High** | **Low** | **Close** | **Volume** |
| --- | --- | --- | --- | --- | --- |
| 1980-12-12 | 0.51 | 0.54 | 0.51 | 0.51 | 47281600 |
| 1980-12-15 | … | … | … | … | … |

Notice how Date was in **bold** and not part of the numbered columns?

That means it was the **index** of the table — like row labels.

### **🧠 What is an “index”?**

- In pandas, every row has an **index** — a special column used to identify rows.
- By default, it’s numbers: 0, 1, 2, 3, ...
- But when you load time series data like stock prices, pandas sets the **Date** as the index.

This is great for plotting, but not always ideal when you want to treat Date like regular data.

### **.reset_index() - What it does:**

- It **removes** the Date column from the index.
- And it **adds** it back as a **normal column** in the table.

Now your table will look like this:

| **index** | **Date** | **Open** | **High** | **Low** | **Close** | **Volume** |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | 1980-12-12 | 0.51 | 0.54 | 0.51 | 0.51 | 47281600 |
| 1 | 1980-12-15 | … | … | … | … | … |

### **⚙️ What does inplace=True mean?**

- It tells Python:
    
    > “Make this change
    > 
    > 
    > **in the original DataFrame**
    > 

If you didn’t use inplace=True, you’d have to write:

```
apple_share_price_data = apple_share_price_data.reset_index()
```

### **🧠 Real-world analogy:**

Imagine you have a list of student marks and their roll numbers are written outside the table (like row labels).

Using reset_index() brings those roll numbers **into the table** so you can use them like any other data column.

| **Part** | **What it means** |
| --- | --- |
| .reset_index() | Move the index (date) into the table as a column |
| inplace=True | Apply the change directly to the existing data |

---

```tsx
apple_share_price_data.plot(x="Date", y="Open")
```

### **apple_share_price_data.plot(x="Date", y="Open")**

### **✅ What this does (in plain English):**

It **draws a line chart** that shows how Apple’s **opening stock price** has changed **over time**.

### **🔍 Breaking it Down:**

### **1️⃣ apple_share_price_data**

- This is your **pandas DataFrame** — a table full of Apple stock data.
- Each row = one day
- Each column = one type of data (Date, Open, Close, etc.)

### **2️⃣ .plot(...)**

- This is a **built-in plotting method** from pandas.
- Under the hood, it uses the **matplotlib** library to draw charts.

You’re basically saying:

> “Hey pandas, please draw a chart using some of this table data.”
> 

### **3️⃣ x="Date"**

- This tells pandas:

> “Use the values in the Date column for the
> 
> 
> **x-axis**
> 

So, dates will go from left to right — like a timeline 📆 ➡️

### **4️⃣ y="Open"**

- This tells pandas:

> “Use the values in the Open column for the
> 
> 
> **y-axis**
> 

That means the line will go **up and down** based on how the stock opened each day 📈📉

### **🖼️ What the chart will look like:**

- **X-axis:** Dates (from the oldest trading date to the newest)
- **Y-axis:** Apple’s opening stock price
- You’ll see a **line graph** showing how the price moved over time.

| **Concept** | **Explanation** |
| --- | --- |
| .plot() | A method to create quick charts from data |
| x=... and y=... | Define what goes on each axis |
| Line chart | The default for .plot() with time-series data |
| matplotlib | The library used behind the scenes (you already installed it!) |

### **🧪 Bonus Tips:**

- Want to add a title?

```
apple_share_price_data.plot(x="Date", y="Open", title="Apple Opening Price Over Time")
```

- Want to make it fancier?

```
apple_share_price_data.plot(x="Date", y="Open", kind="line", color="green", figsize=(12, 6))
```

---

```tsx
apple.dividends
apple.dividends.plot()
```

### **apple.dividends**

### **✅ What it does:**

This line **gets all of Apple’s dividend payment history** — directly from Yahoo Finance — using your apple ticker object.

### **🧠 What is a dividend?**

> A **dividend** is a payment that a company gives to its shareholders, usually every quarter, as a way to share profits.
> 
- Not all companies give dividends.
- Apple started giving them again in 2012 after a long break.

### **🔍 What you get:**

- The result of apple.dividends is a **pandas Series**.
- Each row = a date Apple paid a dividend
- Each value = the dividend amount (in USD)

Example:

```
Date
2012-08-16    0.378571
2012-11-08    0.378571
2013-02-07    0.378571
...
2023-08-17    0.24
Name: Dividends, dtype: float64
```

### **apple.dividends.plot()**

### **✅ What it does:**

This **draws a line chart** showing how Apple’s **dividend payments have changed over time**.

### **🔍 What the chart shows:**

- **X-axis**: Dates when dividends were paid
- **Y-axis**: Dividend amounts (in USD)
- You’ll likely see a **stepped line**, with increases over time — Apple has slowly increased its dividend.

### **🧠 Why is this useful?**

- Investors love dividend-paying companies — they offer **regular income**.
- This plot helps you:
    - Spot when Apple resumed paying dividends (around 2012)
    - See if the dividend is growing steadily (a good sign for investors!)

| **Python Concept** | **Explanation** |
| --- | --- |
| Object attribute | apple.dividends accesses built-in financial data |
| pandas Series | Like a column with a date index |
| .plot() | Quickly creates a line chart |
| Time series | You’re plotting changes across time (date on x-axis) |

### **📌 Bonus — make the chart prettier:**

```
apple.dividends.plot(title="Apple Dividend History", ylabel="Dividend (USD)", figsize=(10, 5), color='purple')
```

---

## **Extracting Stock Data Using a Web Scraping**

Notebook → Extracting_web.ipynb

```tsx
!pip install pandas
!pip install requests
!pip install bs4
!pip install html5lib 
!pip install lxml
!pip install plotly
```

### **!pip install pandas**

✅ **What it does:**

Installs **pandas**, the most important library for working with data tables (called *DataFrames*).

📦 You’ll use pandas to:

- Store data you scrape
- Clean and transform it
- Analyze it later

📘 Think of it as: Excel + Python = pandas

### **!pip install requests**

✅ **What it does:**

Installs **requests**, a library used to **download data from websites**.

🧠 It allows your Python code to say:

> “Hey website, please send me your HTML page.”
> 

🔧 You’ll often use this for web scraping when a website allows you to access its content.

## **!pip install bs4**

✅ **What it does:**

Installs **BeautifulSoup**, a library from the bs4 package used to **parse (read and understand) HTML and XML**.

📖 Imagine HTML as a giant document — BeautifulSoup helps Python **find specific pieces of information**, like:

- The current stock price
- A company’s name
- Headlines or tags

### **!pip install html5lib**

✅ **What it does:**

Installs **html5lib**, which is an **HTML parser**.

💡 Parsers are engines that help BeautifulSoup read messy or complex HTML pages — and html5lib is great at handling “badly written” HTML.

### **!pip install lxml**

✅ **What it does:**

Installs another **HTML/XML parser** called lxml.

📘 You don’t *need* both html5lib and lxml, but it’s good to have options. lxml is faster, while html5lib is more forgiving.

👉 When using BeautifulSoup, you’ll specify which parser to use:

```
BeautifulSoup(html, 'lxml')  # or 'html.parser' or 'html5lib'
```

### **!pip install plotly**

✅ **What it does:**

Installs **Plotly**, a powerful library for building **interactive graphs and dashboards**.

📊 With Plotly, you’ll be able to:

- Create interactive line/bar charts
- Hover over points to see data
- Build the final dashboard for your project!

### **🧠 Summary — What Each Library Does:**

| **Library** | **Use Case** |
| --- | --- |
| pandas | Handle tabular data (like Excel in Python) |
| requests | Download web pages |
| bs4 (BeautifulSoup) | Extract specific data from HTML |
| html5lib | Parse poorly structured HTML |
| lxml | Parse HTML/XML quickly |
| plotly | Make interactive graphs & dashboards |

---

```tsx
import pandas as pd
import requests
from bs4 import BeautifulSoup
```

### **import pandas as pd**

✅ What it does:

- This **imports the pandas library**.
- You’re giving it a shortcut name: pd.

📘 Why use pandas?

- Once you scrape data from the website (like stock prices, company names, etc.), you’ll **store it in a DataFrame**.
- A DataFrame is like a neat Excel sheet: rows + columns.

💡 Real-life example:

```
data = pd.DataFrame([...])
```

### **import requests**

✅ What it does:

- This brings in the requests library.
- It allows your Python code to **make web requests**, like opening a URL in your browser.

🧠 Think of this line as saying:

> “I want to send a message to a website and get the HTML response back.”
> 

You’ll usually use it like this:

```
response = requests.get("https://example.com")
```

### **from bs4 import BeautifulSoup**

✅ What it does:

- Imports the BeautifulSoup class from the bs4 package.

📖 BeautifulSoup helps you **read and search** the HTML page you got from requests.

🧠 Imagine the HTML is a jungle of tags and text — BeautifulSoup is your **machete to cut through and find just what you want**.

Example use:

```
soup = BeautifulSoup(response.text, 'lxml')
```

### **🔁 How These 3 Work Together:**

| **Step** | **What Happens** |
| --- | --- |
| 1️⃣ | Use requests.get() to fetch the HTML page |
| 2️⃣ | Use BeautifulSoup() to parse and search the page |
| 3️⃣ | Use pandas to store and organize the scraped data |

### **🧠 Summary:**

| **Line** | **Role** |
| --- | --- |
| import pandas as pd | Tool to organize your scraped data |
| import requests | Tool to grab webpages |
| from bs4 import BeautifulSoup | Tool to extract data from HTML |

---

```tsx
import warnings

# Ignore all warnings
warnings.filterwarnings("ignore", category=FutureWarning)
```

### **import warnings**

### **✅ What it does:**

- You’re bringing in Python’s built-in **warnings module**.
- This module controls how **warnings** are shown in your notebook.

### **🧠 What are “warnings”?**

> Warnings are **non-breaking messages**Warnings are **non-breaking messages** Python gives you — kind of like gentle reminders or heads-ups.
> 

They don’t stop your code from running — they just say:

> “Hey, this feature might stop working in future versions,” or
“You’re doing something that’s not ideal.”
> 

### **warnings.filterwarnings("ignore", category=FutureWarning)**

Let’s break this down:

| **Part** | **Meaning** |
| --- | --- |
| "ignore" | You’re telling Python to **hide** the warning |
| category=FutureWarning | Only hide warnings of this specific type: **FutureWarning** |

### **💡 What is a FutureWarning ?**

- A FutureWarning tells you:

> “This thing still works **for now not work in future versions of Python or libraries.”**
> 

You often see these when you’re using:

- Newer versions of pandas or numpy
- Deprecated functions or features

### **🧽 Why ignore it?**

Because you’re focusing on:

- **Learning**
- **Writing clean code**
- **Not getting distracted by long warning messages**

This line just says:

> “Hide the warnings about future changes. I’ll worry about those later.”
> 

### **🧠 Real-world analogy:**

Imagine you’re trying to follow a cooking recipe, but a chef keeps whispering:

> “Oh, this pan might not be recommended in next year’s cookbook…”
> 

You’re like:

> “Shhh, let me just finish cooking right now.”
> 

That’s what this line is doing 😄

### **✅ Summary:**

| **Line** | **What it does** |
| --- | --- |
| import warnings | Lets you manage warning messages |
| warnings.filterwarnings("ignore", category=FutureWarning) | Hides future-related warnings to keep the output clean |

---

```tsx
#Step 1: Send an HTTP request to the web page

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/netflix_data_webpage.html"
```

### **url = "https://cf-courses-data...netflix_data_webpage.html"**

### **✅ What this line does:**

- You’re **creating a variable** called url.
- You’re **storing a link** (a string) inside it — this is the **webpage** you want to scrape.

### **🧠 Python Concepts You’re Using Here:**

| **Concept** | **Explanation** |
| --- | --- |
| url | This is a variable — a label you give to some data. In this case, it’s a **web address (URL)**. |
| "..." | Anything inside quotes is a **string** — just text. This one happens to be a web address. |
| = | The assignment operator — it means you’re storing the value on the right (the string) into the variable on the left (url). |

### **🌐 What’s inside this webpage?**

This specific link goes to a saved .html file hosted by IBM.

It’s part of the course, and it contains:

- A fake webpage with **Netflix stock data** in a table format
- You’ll be scraping this table using BeautifulSoup

You’re treating this URL as your **target** to download and extract data from.

### **🧠 Real-life analogy:**

Think of url like a **home address**, and you’re saying:

> “This is where I want to send my Python code to collect some data.”
> 

---

```tsx
data  = requests.get(url).text
print(data)
```

### **data = requests.get(url).text**

### **✅ What it does:**

- This **downloads the web page** at the given URL
- It then **extracts the HTML content as plain text**
- Finally, it stores that content inside a variable named data

### **🧠 Breaking it down:**

| **Part** | **What it means** |
| --- | --- |
| requests.get(url) | Sends a **GET request** to the webpage and brings back a response (like opening a URL in your browser) |
| .text | Extracts the raw HTML content from that response (as a string) |
| data = ... | Stores the full HTML string in the variable data |

### **🧠 What is HTML?**

> HTML is the language that websites are built with. It stands for
> 
> 
> **HyperText Markup Language**
> 

Your code just downloaded something that looks like this:

```
<html>
<head><title>Netflix Data</title></head>
<body>
  <h1>Netflix Stock Data</h1>
  <table>
    <tr><th>Date</th><th>Open</th><th>Close</th></tr>
    <tr><td>2022-01-01</td><td>530</td><td>550</td></tr>
    ...
  </table>
</body>
</html>
```

You’ll extract the table from this messy text in the next steps.

### **print(data)**

### **✅ What it does:**

- This just **prints out** the raw HTML you downloaded.

👀 You’ll see a lot of:

- <html>, <table>, <tr>, <td> — these are **HTML tags**
- These tags define the structure of the web page

### **🧠 Real-life analogy:**

Imagine visiting a web page and doing **Right-click > View Page Source**.

That’s what requests.get(url).text gives you — the **raw behind-the-scenes code** of the webpage.

### **✅ Summary:**

| **Line** | **What it does** |
| --- | --- |
| requests.get(url).text | Downloads and extracts HTML as text |
| data = ... | Saves the HTML to a variable for later use |
| print(data) | Lets you view the raw HTML to understand what you’ll be scraping |

---

```tsx
#Step 2: Parse the HTML content

soup = BeautifulSoup(data, 'html.parser')
```

### **soup = BeautifulSoup(data, 'html.parser')**

### **✅ What it does:**

You’re creating a **BeautifulSoup object** from the raw HTML string (data), so you can:

- **Read it**
- **Search it**
- **Extract** specific parts like tables, headings, or text

You’re also telling BeautifulSoup:

> “Use the html.parser engine to understand the HTML.”
> 

### **🧠 Breaking It Down:**

| **Part** | **What it means** |
| --- | --- |
| BeautifulSoup(...) | This creates a BeautifulSoup object |
| data | The raw HTML string you downloaded earlier |
| 'html.parser' | A built-in parser that helps BeautifulSoup understand HTML syntax |
| soup = ... | You store the parsed HTML object in a variable named soup |

### **🎯 What is soup now?**

After this line, soup becomes a **structured version of your webpage**.

That means you can now write:

```
soup.find('table')       # Find the first <table> element
soup.find_all('tr')      # Find all table rows
soup.title.text          # Get the text inside <title> tags
```

Without BeautifulSoup, you’d be stuck manually searching through giant strings — this makes it easy!

### **🧠 Real-life analogy:**

Think of HTML like a messy PDF with a million pages.

BeautifulSoup turns it into a clean table of contents you can search with a few lines of code.

### **✅ Summary:**

| **Code** | **What it does** |
| --- | --- |
| BeautifulSoup(data, 'html.parser') | Parses HTML into a searchable object |
| soup = ... | Stores the parsed page in a variable for easy access |

---

```tsx
#Step 3: Identify the HTML tags

netflix_data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])
```

This line is **very important** for data analysis and dashboard building.

### **netflix_data = pd.DataFrame(columns=[...])**

### **✅ What this does:**

You’re creating a new, **empty table** (called a **DataFrame**) using **pandas**, and giving it **column headers** just like in Excel or Google Sheets.

### **🧠 Breaking It Down:**

| **Part** | **Meaning** |
| --- | --- |
| pd.DataFrame(...) | Tells pandas to create a new DataFrame (think: an empty table) |
| columns=[...] | You’re specifying the **column names** that your data will have |
| netflix_data = ... | You’re saving this table into a variable called netflix_data |

### **📊 The Table You’re Creating Has These Columns:**

| **Column Name** | **Meaning** |
| --- | --- |
| "Date" | The date of the stock data |
| "Open" | Stock price when the market opened that day |
| "High" | Highest price on that day |
| "Low" | Lowest price on that day |
| "Close" | Stock price when the market closed |
| "Volume" | How many shares were traded on that day |

🔎 These are **typical stock market metrics** — you’ll be extracting them from the <table> in the HTML.

### **💡 Why set up an empty DataFrame first?**

Because you’ll be **adding rows** to this DataFrame inside a loop.

For example:

```
for row in soup.find_all('tr'):
    # extract data from the row
    # add the data as a new row to netflix_data
```

By defining the structure first, you’re saying:

> “Hey pandas, get ready to hold data that looks like this!”
> 

### **🧠 Real-life analogy:**

Think of this like opening Excel, creating column headers:

```
Date | Open | High | Low | Close | Volume
```

…but not typing in any values yet.

You’re preparing a **container** to hold data once it’s scraped.

### **✅ Summary:**

| **Code** | **What it does** |
| --- | --- |
| pd.DataFrame(...) | Creates a table using pandas |
| columns=[...] | Sets the column headers |
| netflix_data = ... | Saves the table to use in later steps |

### **Working on HTML table:**

These are the following tags which are used while creating HTML tables.

- <table>: This tag is a root tag used to define the start and end of the table. All the content of the table is enclosed within these tags.
- <tr>: This tag is used to define a table row. Each row of the table is defined within this tag.
- <td>: This tag is used to define a table cell. Each cell of the table is defined within this tag. You can specify the content of the cell between the opening and closing tags.
- <th>: This tag is used to define a header cell in the table. The header cell is used to describe the contents of a column or row. By default, the text inside a tag is bold and centered.
- <tbody>: This is the main content of the table, which is defined using the tag. It contains one or more rows of elements.

---

```tsx
# Step 4: Use a BeautifulSoup method for extracting data

# First we isolate the body of the table which contains all the information
# Then we loop through each row and find all the column values for each row

for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    Open = col[1].text
    high = col[2].text
    low = col[3].text
    close = col[4].text
    adj_close = col[5].text
    volume = col[6].text
    
    # Finally we append the data of each row to the table
    netflix_data = pd.concat([netflix_data,pd.DataFrame({"Date":[date], "Open":[Open], "High":[high], "Low":[low], "Close":[close], "Adj Close":[adj_close], "Volume":[volume]})], ignore_index=True)    
```

You’re now doing the **core part of web scraping** — extracting actual stock data from a webpage’s table and filling it into your pandas DataFrame.

### **🧱 Big Picture of What You’re Doing**

You’re scraping data from a table that looks like this (in HTML):

```
<table>
  <thead>...</thead>   <-- header
  <tbody>              <-- body with actual data rows
    <tr>               <-- each row
      <td>2023-01-01</td>   <-- each column
      <td>300</td>
      <td>310</td>
      ...
    </tr>
    ...
  </tbody>
</table>
```

### **for row in soup.find("tbody").find_all('tr'):**

➡️ This line starts a loop through all the table rows (<tr>) inside the <tbody> part of the HTML.

| **Code** | **Meaning** |
| --- | --- |
| soup.find("tbody") | Finds the <tbody> tag (where the actual stock data rows are) |
| .find_all('tr') | Finds all <tr> tags inside it — each one is a **row** |
| for row in ... | Starts a loop: you’ll handle one row of data at a time |

### **col = row.find_all("td")**

➡️ This finds **all the columns** (<td> tags) inside one row.

You’re now ready to extract values from each column like Date, Open, High, etc.

### **🔹 These lines extract the text from each column:**

```
date = col[0].text
Open = col[1].text
high = col[2].text
low = col[3].text
close = col[4].text
adj_close = col[5].text
volume = col[6].text
```

| **Variable** | **Data it stores** |
| --- | --- |
| date | Date of the stock entry |
| Open | Price at which stock opened |
| high | Highest price that day |
| low | Lowest price that day |
| close | Closing price |
| adj_close | Adjusted close (for splits/dividends) |
| volume | Number of shares traded |

.text pulls out the actual **text content** from the HTML tag.

### **🔹 Appending each row to your DataFrame:**

```
netflix_data = pd.concat([
    netflix_data,
    pd.DataFrame({
        "Date": [date], "Open": [Open], "High": [high],
        "Low": [low], "Close": [close],
        "Adj Close": [adj_close], "Volume": [volume]
    })
], ignore_index=True)
```

### **What’s going on here?**

You’re:

1. Creating a **one-row DataFrame** using pd.DataFrame({...})
2. Adding (concat) that row to your netflix_data table
3. ignore_index=True ensures pandas reindexes rows correctly

### **🧠 Why concat instead of .append() ?**

- append() is deprecated in new versions of pandas.
- pd.concat([...]) is the preferred method.

### **🧠 Real-life analogy:**

You’re:

- Going row by row in a printed stock report
- Reading the values with your eyes (using .text)
- Typing each row into Excel (using pd.DataFrame(...))
- Sticking it below the previous rows (using pd.concat())

### **✅ Summary Table**

| **Code** | **What it does** |
| --- | --- |
| soup.find("tbody").find_all("tr") | Finds all data rows in the table |
| row.find_all("td") | Finds all cells (columns) in one row |
| .text | Extracts text from the HTML cell |
| pd.DataFrame(...) | Makes a one-row table with the extracted data |
| pd.concat(...) | Adds it to the growing main table (netflix_data) |

---

```tsx
#Step 5: Print the extracted data

netflix_data.head()
```

### **netflix_data.head()**

### **✅ What this does:**

This shows you the **first 5 rows** of the netflix_data table.

It’s a quick way to:

- Check if the data looks correct
- Make sure the table was filled properly during your scraping loop

### **🧠 Why use .head() ?**

Imagine you’re working with a huge Excel sheet with **hundreds of rows**.

You don’t want to scroll through the whole thing just to verify it’s right — you just want to see the top few rows.

That’s exactly what .head() does in pandas.

### **📊 Example output might look like:**

|  | **Date** | **Open** | **High** | **Low** | **Close** | **Adj Close** | **Volume** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 2023-01-01 | 300 | 310 | 295 | 305 | 305 | 5,000,000 |
| 1 | 2023-01-02 | 306 | 312 | 300 | 309 | 309 | 4,800,000 |
| 2 | … | … | … | … | … | … | … |

Each row = one day’s stock data

Each column = a different attribute (like open price, volume, etc.)

### **🧠 Want to see more rows?**

You can pass a number into .head(), like this:

```
netflix_data.head(10)  # Show top 10 rows
```

### **✅ Summary**

| **Code** | **What it does** |
| --- | --- |
| netflix_data.head() | Shows the first 5 rows of the table |
| head(10) | Shows the first 10 rows |
| Use case | To check your data without printing the entire thing |

---

### **What is read_html in pandas library?**

read_html in the **pandas** library is a super useful tool that helps you extract tables directly from a **webpage** or **HTML file** — without needing BeautifulSoup or manual scraping.

### **pandas.read_html()**

### **✅ What it does:**

It **reads all <table> tags** from a webpage or HTML file and **automatically converts them into pandas DataFrames**.

### **📦 Syntax:**

```
pd.read_html("URL_or_HTML_file")
```

> It returns a **list of DataFrames** — one for each table found.
> 

### **💡 Example 1: Reading tables from a website**

```
import pandas as pd

tables = pd.read_html("https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)")
print(len(tables))          # How many tables found?
print(tables[0].head())     # Show first few rows of the first table
```

📌 This automatically:

- Opens the page
- Looks for all <table> tags
- Parses their content
- Converts them into DataFrames

### **💡 Example 2: Reading from a local HTML file**

```
tables = pd.read_html("netflix_data_webpage.html")
netflix_table = tables[0]
```

### **✅ Why is it useful?**

| **Without** read_html | **With** read_html |
| --- | --- |
| Use requests, BeautifulSoup, loop through tags manually | One line of code |
| Manually find each table, clean it | Automatically extracts all tables |
| Tedious for beginners | Beginner-friendly and fast |

### **⚠️ A few things to remember:**

| **Rule** | **Explanation** |
| --- | --- |
| The table must be **well-formed** | Poorly structured HTML might confuse it |
| You must have **lxml**, **html5lib**, or **bs4** installed | These help parse the HTML |
| Returns a **list of DataFrames** | Use indexing like tables[0] to get a specific table |

### **✅ Summary**

| **Function** | **What it does** |
| --- | --- |
| pd.read_html(url_or_path) | Reads tables from a webpage or HTML file |
| Returns | A list of DataFrames (1 per table) |
| Libraries needed | lxml, bs4, or html5lib |

### **🚀 Want to try it?**

Try running this:

```
import pandas as pd
tables = pd.read_html("https://www.basketball-reference.com/leagues/NBA_2023_per_game.html")
tables[0].head()
```

It will load an NBA stats table — automatically!

---