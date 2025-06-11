# IBM_c4_m5

## Application Programming Interface (APIs)

### **1. What Is an API?**

### **Definition**

An **Application Programming Interface (API)** is a set of protocols, tools, and definitions that allow software applications to communicate with each other. It acts as an intermediary that enables two systems—whether web services, operating systems, or applications—to exchange data and functionality.

### **Why APIs Matter**

- **Standardized communication**: APIs provide a consistent way for applications to interact.
- **Efficiency**: Developers can reuse existing functionalities instead of reinventing them.
- **Interoperability**: APIs allow different software to work together seamlessly.
- **Security**: Controlled access to data and services via authentication and authorization.

### **2. Types of APIs**

APIs can be categorized based on their functionality and use case.

### **a. Web APIs (HTTP APIs)**

Web APIs allow applications to communicate over the internet using HTTP. These are commonly used in web development and cloud services.

### **Common Web API Protocols**

1. **REST (Representational State Transfer)**
    - Uses standard HTTP methods (`GET`, `POST`, `PUT`, `DELETE`).
    - Stateless communication.
    - Data is often exchanged in JSON or XML format.
2. **SOAP (Simple Object Access Protocol)**
    - Uses XML-based messaging.
    - Supports more complex security and transactions.
    - Often used in enterprise applications.
3. **GraphQL**
    - Developed by Facebook.
    - Allows clients to request only the data they need.
    - More efficient than REST in certain use cases.

### **b. Local APIs**

Local APIs allow communication within a single system (e.g., an operating system API or a database API).

Examples:

- **Windows API**: Provides system functionalities to Windows applications.
- **POSIX API**: Used in Unix-based systems for system calls.

### **c. Database APIs**

Database APIs allow applications to interact with databases.

- **ODBC (Open Database Connectivity)**: Standard API for accessing database management systems.
- **JDBC (Java Database Connectivity)**: Java-based API for interacting with databases.

### **d. Hardware APIs**

These provide access to hardware functionalities, such as:

- **Graphics APIs**: OpenGL, Vulkan, DirectX.
- **Sensor APIs**: Used in mobile devices for accessing GPS, accelerometers, etc.

### **e. Third-Party APIs**

External services provide APIs for integration:

- **Google Maps API**: Allows apps to embed maps and location data.
- **Twitter API**: Provides access to tweets and user data.
- **Stripe API**: Enables payment processing.

### **3. API Architecture**

APIs are built using different architectural styles, which define how they communicate and expose data.

### **a. RESTful Architecture**

- **Stateless**: The server doesn’t remember previous requests.
- **Uses HTTP methods**:
    - `GET`: Retrieve data.
    - `POST`: Create new resources.
    - `PUT`: Update existing resources.
    - `DELETE`: Remove resources.

Example REST API request:

```bash
GET <https://api.example.com/users>
```

Example response (JSON):

```json
{
  "users": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ]
}
```

### **b. SOAP Architecture**

- Uses XML for messaging.
- More robust error handling and security.
- Defines operations in **WSDL (Web Services Description Language).**

Example SOAP request:

```xml
<soap:Envelope>
  <soap:Body>
    <GetUser>
      <UserId>1</UserId>
    </GetUser>
  </soap:Body>
</soap:Envelope>
```

### **c. GraphQL Architecture**

- Clients specify the exact data they need.
- Reduces over-fetching and under-fetching.

Example GraphQL query:

```graphql
{
  user(id: 1) {
    name
    email
  }
}
```

### **4. API Authentication and Security**

APIs must be protected to ensure secure communication and prevent unauthorized access.

### **a. API Authentication Methods**

1. **API Keys**
    - A simple token sent in API requests.
    - Example:
    
    ```bash
    GET <https://api.example.com/data?api_key=YOUR_API_KEY>
    ```
    
2. **OAuth (Open Authorization)**
    - Used for authentication between services.
    - Example: Logging in to a third-party website using Google credentials.
3. **JWT (JSON Web Token)**
    - Secure way to transmit authentication tokens.

### **b. API Security Measures**

1. **Rate Limiting**: Restrict the number of requests to prevent abuse.
2. **HTTPS Encryption**: Protects data in transit.
3. **Input Validation**: Prevents SQL injection and malicious attacks.

### **5. API Development and Testing**

APIs are developed using frameworks and tested with specialized tools.

### **a. API Development Frameworks**

- **Flask/Django (Python)**: Used to build RESTful APIs.
- **Express.js (Node.js)**: Lightweight framework for building APIs.
- **Spring Boot (Java)**: Enterprise-grade API framework.

### **b. API Testing Tools**

- **Postman**: Interactive tool for API testing.
- **cURL**: Command-line tool for making API requests.
- **Swagger**: API documentation and testing framework.

Example using Postman to test a REST API request:

```bash
POST <https://api.example.com/users>
{
  "name": "Alice",
  "email": "alice@example.com"
}
```

### **6. API Integration and Use Cases**

APIs power many applications and services.

### **a. API Integration Examples**

- **Connecting Applications:** Mobile apps retrieve weather data via APIs.
- **Automation:** APIs allow automated data extraction and processing.
- **Machine Learning:** APIs provide access to AI models (e.g., OpenAI’s GPT API).

### **b. Real-World Applications**

- **Finance:** APIs integrate stock data and banking transactions.
- **Healthcare:** APIs enable telemedicine platforms.
- **E-commerce:** APIs connect payment gateways and product catalogs.

### **7. Future Trends in APIs**

- **Microservices Architecture:** APIs allow independent service components to communicate.
- **Serverless APIs:** APIs powered by cloud functions (AWS Lambda, Google Cloud Functions).
- **GraphQL Adoption:** More applications are shifting to GraphQL for efficient data retrieval.
- **AI-Powered APIs:** APIs provide natural language processing and image recognition.

### **8. Hands-On API Exercises**

1. **Use an Open API:**
    - Find a free API (e.g., OpenWeatherMap).
    - Make a request using Python:
    
    ```python
    import requests
    response = requests.get("<https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY>")
    print(response.json())
    ```
    
2. **Create a Simple REST API:**
    - Use Flask to create an API endpoint:
    
    ```python
    from flask import Flask, jsonify
    
    app = Flask(__name__)
    
    @app.route('/hello', methods=['GET'])
    def hello():
        return jsonify({"message": "Hello, World!"})
    
    if __name__ == '__main__':
        app.run(debug=True)
    ```
    
3. **Test an API with Postman:**
    - Set up a request in Postman.
    - Authenticate using an API key.
    - Analyze the response.

## **9. Summary**

- **APIs** enable communication between software applications.
- **Types of APIs** include Web APIs (REST, SOAP, GraphQL), Local APIs, and Database APIs.
- **Authentication** methods like API keys and OAuth ensure secure access.
- **API development** uses frameworks like Flask, Express.js, and Spring Boot.
- **Testing tools** like Postman and Swagger help verify API functionality.
- **Future trends** include microservices, AI-powered APIs, and serverless architectures.

---

## Pandas in APIs and REST APIs

In modern data-centric applications, it's common to build REST APIs that serve data analysis, cleaning, or transformation functionality powered by Pandas. This combination allows you to expose powerful data processing routines as services that other applications (or even front-end interfaces) can consume.

### 1. Why Use Pandas in a REST API?

Pandas is a robust library for data manipulation and analysis. Integrating it into your API can help you:

- **Perform Real-Time Data Processing:** Clean, transform, and analyze incoming data on the fly.
- **Expose Analytics:** Provide endpoints that return summary statistics, reports, or processed datasets.
- **Data-Driven Decision Making:** Create microservices that power dashboards or support forecasting by processing large datasets.
- **Batch and Ad-hoc Queries:** Enable users to query datasets processed by Pandas and get results in a standardized format (like JSON).

For example, you might have a CSV file or database that you load into a Pandas DataFrame. Then, your REST API could expose endpoints that compute averages, filter rows, pivot tables, or even generate charts from the data.

### 2. Building a Simple REST API with Pandas Using Flask

Let’s walk through creating a basic REST API that uses Pandas to process and serve data. In this example, we’ll create an endpoint that:

- Loads data from a CSV file into a DataFrame.
- Performs a simple aggregation (e.g., computes summary statistics).
- Returns the result as a JSON response.

### Step-by-Step Example

### a. Install Necessary Packages

You'll need Flask and Pandas. If not installed, use:

```bash
pip install Flask pandas
```

### b. Create a Sample CSV Data File

For demonstration purposes, create a CSV file named `sales.csv`:

```
region,sales
North,100
South,150
East,200
West,130
North,110
East,220
```

### c. Write the Flask Application

Create a file called `app.py` with the following code:

```python
from flask import Flask, jsonify, request
import pandas as pd

app = Flask(__name__)

# Helper function to load and process data
def get_sales_data():
    # Load CSV data into Pandas DataFrame
    df = pd.read_csv("sales.csv")
    return df

@app.route('/sales/summary', methods=['GET'])
def sales_summary():
    """
    Returns summary statistics for sales data,
    aggregated by region (e.g., total and average sales).
    """
    try:
        df = get_sales_data()
        # Group by region to get total and average sales per region
        summary_df = df.groupby('region').agg(
            total_sales=('sales', 'sum'),
            average_sales=('sales', 'mean'),
            count=('sales', 'count')
        ).reset_index()

        # Convert the DataFrame to JSON-friendly format
        result = summary_df.to_dict(orient="records")
        return jsonify({"status": "success", "data": result})
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

@app.route('/sales/filter', methods=['GET'])
def sales_filter():
    """
    Filters sales data based on a sales threshold passed as a query parameter.
    For example: /sales/filter?min_sales=120
    """
    try:
        min_sales = float(request.args.get('min_sales', 0))
        df = get_sales_data()
        filtered_df = df[df['sales'] >= min_sales]
        result = filtered_df.to_dict(orient="records")
        return jsonify({"status": "success", "data": result})
    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

if __name__ == '__main__':
    app.run(debug=True)
```

### d. How It Works

- **Data Processing:**
    
    The `get_sales_data()` function loads the CSV file into a Pandas DataFrame. This DataFrame is then used to perform grouping, filtering, and aggregation.
    
- **API Endpoints:**
    - **`/sales/summary`:** Aggregates sales by region and returns total, average, and count as JSON.
    - **`/sales/filter`:** Accepts a query parameter (`min_sales`) to filter sale records and returns the subset.
- **Error Handling:**
    
    Exceptions are caught to return a JSON error message with an HTTP 500 status if something goes wrong.
    
- **JSON Conversion:**
    
    Pandas’ `.to_dict(orient="records")` method converts DataFrame rows into a list of dictionaries, making it easy to serve via JSON.
    

### e. Run and Test the API

Start your Flask app:

```bash
python app.py
```

Now, visit:

- `http://127.0.0.1:5000/sales/summary` to see the aggregated summary.
- `http://127.0.0.1:5000/sales/filter?min_sales=120` to see the filtered dataset.

You can also use tools like Postman or cURL to test these endpoints.

### 3. Advanced Considerations

### a. Handling Large Datasets

- **Lazy Loading:** Instead of loading the CSV with every request, cache the DataFrame if the data doesn’t change frequently.
- **Chunking:** Consider processing the data in chunks using `pd.read_csv(..., chunksize=...)` for very large datasets.

### b. Data Caching

- Use in-memory caches or tools like Redis to cache processed results, thereby reducing the load on repeated data processing.

### c. Using Modern Frameworks

- **FastAPI:** For better performance and async capabilities, you might consider FastAPI. It works very well with Pandas and has automatic Swagger documentation.
- **Django REST Framework:** If you’re already in the Django ecosystem, DRF can be integrated with Pandas processing in view functions.

### d. Security and Validation

- Validate query parameters and handle potential errors (e.g., invalid numeric inputs) to prevent unhandled exceptions.
- Secure your API endpoints if they expose sensitive data.

### 4. Conclusion

Integrating Pandas within a REST API lets you bring powerful data processing capabilities to your web services. By exposing endpoints that perform data aggregation, filtering, and analysis on the fly, you can build responsive, data-driven applications and microservices.

We covered:

- **The Why and How:** The reasons to power your API with Pandas and a practical guide using Flask.
- **Building API Endpoints:** Loading CSV data, performing group-by operations, filtering data via query parameters, and returning JSON responses.
- **Advanced Considerations:** Caching, handling large datasets, alternative frameworks like FastAPI, and security measures.

This approach enables you to build APIs that not only serve static data but also perform real-time analysis and transformations, providing valuable insights to clients or downstream applications.

---

## REST APIs and HTTP requests - Part 1

### 1. Introduction to REST APIs

**REST** (Representational State Transfer) is an architectural style for designing networked applications. A REST API (or RESTful API) exposes resources—such as data or services—via standard HTTP methods. Some key points are:

- **Stateless Communication:** Each request from the client to the server must contain all of the information needed, with no stored context on the server.
- **Resource-Based:** Resources are identified by URLs (Uniform Resource Locators), and the API exposes actions (such as read, update, create, delete) on these resources.
- **Uniform Interface:** By using standard HTTP methods and status codes, REST APIs provide a consistent and predictable interface.

### 2. Understanding HTTP Requests

At the heart of REST APIs is the HTTP protocol. An **HTTP request** is how a client (for example, a web browser or a mobile app) asks a server to perform some action on a resource. Here’s a breakdown of its key components.

### a. HTTP Request Line

The request line specifies the type of action you want to perform on a resource. It includes three parts:

1. **HTTP Method**: Indicates the action (e.g., GET, POST, PUT, DELETE).
2. **Request URI (Uniform Resource Identifier)**: Specifies the resource’s location.
3. **HTTP Version**: Typically, HTTP/1.1 or HTTP/2.

**Example:**

```
GET /users/123 HTTP/1.1
```

This line means “Retrieve the resource at `/users/123` using HTTP/1.1.”

### b. HTTP Request Headers

Headers provide metadata about the request. They can include information on the client, the type of data being sent, encoding, authentication tokens, and more.

**Common Headers:**

- **`Accept`**: Specifies the data formats the client can process (e.g., `application/json`).
- **`Content-Type`**: Indicates the format of the data in the request body (e.g., `application/json` for JSON data).
- **`Authorization`**: Carries credentials (like API keys or tokens) for authenticating the request.
- **`User-Agent`**: Provides information about the client software.

**Example Header Section:**

```
Accept: application/json
Content-Type: application/json
Authorization: Bearer ABCDEFG12345678
User-Agent: MyApp/1.0
```

### c. HTTP Request Body

The body of an HTTP request carries the data to be sent to the server, and it’s mostly used with methods like POST, PUT, or PATCH. For GET requests, the body is typically empty because data is passed in the URL as query parameters.

**Example Body (JSON):**

```json
{
  "name": "Alice",
  "email": "alice@example.com"
}
```

This might accompany a POST request to create a new user.

### d. Query Parameters

Query parameters are appended to the URL to pass additional data to the server. They are typically used with GET requests.

**Example URL with Query Parameters:**

```
GET /users?active=true&sort=desc HTTP/1.1

```

Here, `active=true` and `sort=desc` are query parameters that refine what data is requested.

### 3. HTTP Methods in REST APIs

The HTTP method in the request line indicates the action to be performed:

- **GET:** Retrieve a resource or a collection of resources. It should not modify the server’s state.
    
    *Example:* `GET /api/books` retrieves a list of books.
    
- **POST:** Create a new resource. The request body typically contains the data for the new resource.
    
    *Example:* `POST /api/books` with a JSON payload to add a new book.
    
- **PUT:** Update or replace an existing resource completely. The URL identifies the resource to update, and the request body contains the new version.
    
    *Example:* `PUT /api/books/123` with updated book details.
    
- **PATCH:** Partially update an existing resource. Only the changes are sent.
    
    *Example:* `PATCH /api/books/123` to update the title of the book.
    
- **DELETE:** Remove a specific resource.
    
    *Example:* `DELETE /api/books/123` removes the book with ID 123.
    

### 4. Example of an HTTP Request

Let's look at a complete example using a GET request to fetch data:

### Example: GET Request Using cURL

```bash
curl -X GET "<https://api.example.com/users?active=true>" \\
     -H "Accept: application/json" \\
     -H "Authorization: Bearer YOUR_API_TOKEN"
```

- **`X GET`** specifies the GET method.
- **URL** includes query parameters.
- **`H`** adds headers for accepted content type and authentication.

### Example: POST Request Using cURL

```bash
curl -X POST "<https://api.example.com/users>" \\
     -H "Content-Type: application/json" \\
     -H "Authorization: Bearer YOUR_API_TOKEN" \\
     -d '{"name": "Alice", "email": "alice@example.com"}'
```

- **`X POST`** specifies the POST method.
- **`d`** sends the JSON data in the request body.

### 5. Summary

- **REST APIs** harness HTTP to allow different systems to communicate through resolved resources.
- An **HTTP request** is made up of a request line (method, URI, and version), headers (providing meta-information), and optionally, a body (for methods that send data).
- **HTTP methods** like GET, POST, PUT, PATCH, and DELETE define the actions an API can perform.
- Query parameters and headers refine and control the request.

---

## REST APIs and HTTP requests - Part 2

### 1. Anatomy of an HTTP Response

An HTTP response is how a server communicates the outcome of an HTTP request. It comprises three main parts:

### a. Status Line

The status line includes:

- **HTTP Version:** e.g., `HTTP/1.1` or `HTTP/2`.
- **Status Code:** A three-digit number that indicates the result of the request.
- **Reason Phrase:** A textual description of the status code.

**Example:**

```
HTTP/1.1 200 OK
```

This indicates that the request was successful.

### b. Response Headers

Response headers provide metadata about the response. They may include:

- **`Content-Type`:** Describes the MIME type of the returned data (e.g., `application/json`).
- **`Content-Length`:** Indicates the size of the response body in bytes.
- **`Cache-Control`:** Directs caching policies.
- **`ETag`:** A unique identifier for the version of the resource, useful for caching.
- **Others:** Headers like `Set-Cookie`, `Location` (in redirects), etc.

**Example Headers:**

```
Content-Type: application/json
Content-Length: 230
Cache-Control: no-cache
```

### c. Response Body

The body contains the actual data returned by the server. For REST APIs, this is typically in JSON format—but it could also be XML, HTML, or even binary data. For example:

```json
{
  "users": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ]
}
```

### 2. HTTP Status Codes

Status codes communicate the result of the HTTP request. They are grouped into several classes:

### a. Successful Responses (2xx)

- **200 OK:** The request was successful, and the response body contains the result.
- **201 Created:** A new resource has been created as a result of the request. Often returned after a POST request.
- **204 No Content:** The request was successful, but there is no content to return (commonly used with DELETE operations).

### b. Redirection (3xx)

- **301 Moved Permanently:** The resource has been permanently moved to a new URL.
- **302 Found:** The resource resides temporarily under a different URL.
- **304 Not Modified:** Indicates that the cached version can be used (used with conditional GET requests).

### c. Client Errors (4xx)

- **400 Bad Request:** The request is malformed or contains invalid parameters.
- **401 Unauthorized:** Authentication is required or has failed.
- **403 Forbidden:** The client does not have permission to access the resource.
- **404 Not Found:** The requested resource could not be found.
- **422 Unprocessable Entity:** The request is well-formed but contains semantic errors (often used in REST APIs when data fails validation).

### d. Server Errors (5xx)

- **500 Internal Server Error:** A generic error indicating that the server encountered an unexpected condition.
- **503 Service Unavailable:** The server is currently unable to handle the request due to temporary overload or maintenance.

### 3. Content Negotiation and Response Formats

APIs can serve multiple formats. Clients use the **`Accept`** header in the request to specify the expected response content type. The server then sets the `Content-Type` header accordingly.

**Example:**

- Request Header: `Accept: application/json`
- Response Header: `Content-Type: application/json`

This flexibility ensures that APIs can serve various clients—from web browsers to mobile apps or other services.

### 4. Error Handling in REST APIs

Effective error handling is crucial for a robust API. Good error responses help clients understand what went wrong and how to fix it.

### a. Structure of Error Responses

A common best practice is to return a JSON object containing:

- **Status Code:** The HTTP status.
- **Error Message:** A human-readable error description.
- **Error Details:** Optional, such as error codes or validation failures.

**Example:**

```json
{
  "status": 404,
  "error": "Not Found",
  "message": "The requested user was not found."
}
```

To standardize error responses, some APIs follow specifications like [RFC 7807 (Problem Details for HTTP APIs)](https://tools.ietf.org/html/rfc7807).

### b. Using HTTP Response Codes Effectively

- **Meaningful Codes:** Always match the error condition with the appropriate HTTP status code (e.g., 400 for bad requests, 401 for unauthorized access).
- **Clear Messages:** Provide clear and actionable error messages.
- **Consistency:** Use a consistent error response format so that clients can easily parse and handle errors.

### c. Example Scenario for an Error Response

Imagine a REST API endpoint that fetches user information by ID. If a user is not found, the API might return:

```
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "status": 404,
  "error": "Not Found",
  "message": "User with ID 123 does not exist."
}
```

This response lets the client know immediately that no such resource exists.

### 5. Advanced HTTP Response Concepts

### a. Caching

- **Headers like `Cache-Control` and `ETag`** help manage how responses are stored by clients and proxies.
- **ETag:** A unique signature representing the current version of a resource. Clients can use `If-None-Match` in their requests to check if the data has changed, enabling efficient caching with potential `304 Not Modified` responses.

### b. Redirection

- When a resource moves, the server uses 3xx codes (like 301, 302) with the **`Location`** header to direct clients to the new resource URL.

### c. Asynchronous Responses

- In modern APIs, especially those dealing with long-running tasks, responses might include a link to a status endpoint where clients can poll for completion.

### 6. Practical Example with cURL

### Example: Successful Response

```bash
curl -X GET "<https://api.example.com/users/123>" \\
     -H "Accept: application/json"
```

**Possible Response:**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 75

{
  "id": 123,
  "name": "Alice",
  "email": "alice@example.com"
}
```

### Example: Error Response

```bash
curl -X GET "<https://api.example.com/users/999>" \\
     -H "Accept: application/json"
```

**Possible Response:**

```
HTTP/1.1 404 Not Found
Content-Type: application/json
Content-Length: 112

{
  "status": 404,
  "error": "Not Found",
  "message": "User with ID 999 does not exist."
}
```

### 7. Summary

- **HTTP Response Structure:** Consists of the status line, headers, and an optional body.
- **Status Codes:** Provide immediate feedback on the outcome of a request, categorized as successes (2xx), redirections (3xx), client errors (4xx), and server errors (5xx).
- **Content Negotiation:** The interplay between `Accept` and `Content-Type` headers allows APIs to communicate in multiple formats.
- **Error Handling:** Standardized error responses (often in JSON) let clients understand and react to issues; using proper status codes and clear messages is key.
- **Advanced Considerations:** Caching, redirection, and asynchronous responses are all part of building robust REST APIs.

---

## **Web Scraping and HTML Basics**

### 1. Introduction to Web Scraping

**Web scraping** is the process of programmatically extracting data from websites. Instead of manually copying and pasting information, you write a script that downloads web pages, parses their content, and extracts the data you need.

### Why Web Scraping?

- **Automation:** Repeatedly extract data from multiple web pages without manual labor.
- **Data Aggregation:** Combine data from various sources for market analysis, research, competitive intelligence, and more.
- **Real-Time Data:** Build systems that continuously collect up-to-date information (e.g., price tracking, news aggregation).
- **Integration:** Feed scraped data into databases or visualizations for further analysis or reporting.

While web scraping is powerful, it requires a clear understanding of legal and ethical guidelines—which we’ll touch on later.

### 2. HTML Basics: Understanding the Structure of Web Pages

Since web scraping is performed on web pages, understanding HTML is crucial. HTML (HyperText Markup Language) is the language used to create webpages. Here are the fundamentals:

### a. HTML Document Structure

Every HTML document follows a basic structure that defines its content and layout. At the highest level, an HTML document might look like this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My Sample Page</title>
    <!-- Meta tags, styles, and scripts go here -->
  </head>
  <body>
    <!-- Visible content begins here -->
    <h1>Welcome to My Website</h1>
    <p>This is a paragraph of text.</p>
    <a href="<https://example.com>">Click here to visit Example.com</a>
  </body>
</html>
```

**Key Sections:**

- **`<!DOCTYPE html>`:**
    
    Declares the document type and version of HTML (HTML5 in this case).
    
- **`<html>` Element:**
    
    The root element that encloses all other elements on the page.
    
    - The `lang` attribute specifies the language (e.g., English).
- **`<head>` Section:**
    
    Contains metadata such as:
    
    - `<meta charset="UTF-8">` sets the character encoding.
    - `<title>` defines the title shown in the browser tab.
    - Links to external CSS files or JavaScript scripts.
- **`<body>` Section:**
    
    Contains all the content that users see, including text, images, links, and interactive elements.
    

### b. HTML Elements, Tags, and Attributes

- **Elements** are defined by tags. For example:
    - `<h1>` to `<h6>`: Headings.
    - `<p>`: Paragraphs.
    - `<a>`: Anchors (hyperlinks).
    - `<div>`: A generic container used to group content.
- **Attributes** are additional pieces of information within a tag that modify its behavior:
    - Example: `<a href="<https://example.com>" target="_blank">`
    Here, `href` defines the destination URL and `target` tells the browser where to open the link.

### c. The DOM (Document Object Model)

When a browser loads an HTML document, it converts the HTML into a **DOM**—a tree-like structure where every element is a node. This structure allows scripting languages (such as JavaScript or Python libraries) to navigate and manipulate the page.

- **Parent and Child Nodes:**
    
    Elements are nested; for example, in `<div><p>Text</p></div>`, the `<p>` element is a child of the `<div>`.
    
- **Siblings:**
    
    Elements that share the same parent are considered siblings.
    

Understanding the DOM is essential because web scraping libraries operate by mimicking DOM navigation.

### 3. Tools for Web Scraping in Python

Several Python libraries simplify the process of web scraping. The most popular ones include:

### a. `requests`

- **Purpose:**
    
    The `requests` library is used to make HTTP requests. It lets you download web page content—in other words, the raw HTML—using simple commands.
    
- **Example:**
    
    ```python
    import requests
    
    url = "<https://example.com>"
    response = requests.get(url)
    if response.status_code == 200:
        html_content = response.text
    else:
        print("Failed to retrieve the page.", response.status_code)
    ```
    

### b. BeautifulSoup (from the `bs4` Package)

- **Purpose:**
    
    BeautifulSoup is a library that parses HTML and XML documents. It creates a parse tree that you can use to navigate the page and extract data.
    
- **Installation:**
    
    ```bash
    pip install beautifulsoup4
    ```
    
- **Basic Usage:**
    
    ```python
    from bs4 import BeautifulSoup
    
    # Assuming html_content was obtained from requests
    soup = BeautifulSoup(html_content, "html.parser")
    
    # Extracting all <h1> tags
    headings = soup.find_all("h1")
    for heading in headings:
        print(heading.get_text().strip())
    
    # Extracting links from <a> tags
    links = soup.find_all("a")
    for link in links:
        link_text = link.get_text().strip()
        link_href = link.get("href")
        print(f"Text: {link_text}, URL: {link_href}")
    ```
    

### c. Handling Dynamic Content

Sometimes a webpage generates content via JavaScript (e.g., infinite scrolling, interactive maps). In such cases:

- **Selenium:**
Automates a web browser to render JavaScript and then extracts content.
- **Requests-HTML:**
Offers a convenient interface that can render JavaScript without the overhead of Selenium, though it may not work for all sites.

### 4. A Step-by-Step Web Scraping Example

Let’s walk through a practical example where we extract data from a simple static web page.

### Scenario: Extract Headings and Links

1. **Download the Web Page:**
    
    ```python
    import requests
    
    url = "<https://example.com>"
    response = requests.get(url)
    if response.status_code == 200:
        html_content = response.text
    else:
        html_content = ""
        print("Error fetching page:", response.status_code)
    ```
    
2. **Parse the HTML with BeautifulSoup:**
    
    ```python
    from bs4 import BeautifulSoup
    
    soup = BeautifulSoup(html_content, "html.parser")
    ```
    
3. **Extract Data:**
    - **Headings:**
        
        ```python
        headings = soup.find_all("h1")
        for heading in headings:
            print("Heading:", heading.get_text().strip())
        ```
        
    - **Links:**
        
        ```python
        links = soup.find_all("a")
        for link in links:
            link_text = link.get_text().strip()
            link_href = link.get("href")
            print(f"Link: {link_text} -> {link_href}")
        ```
        

This example shows the core steps: downloading HTML, parsing the DOM, and navigating through tags to extract useful information.

### 5. Legal and Ethical Considerations

Before scraping any website, it’s important to consider:

- **`robots.txt`:**
    
    Most websites provide a file called `robots.txt` at the root of their domain (e.g., `https://example.com/robots.txt`) that guides which parts of the site can or cannot be scraped by automated tools.
    
- **Terms of Service:**
    
    Always review the website's terms of use to ensure that your scraping activities do not violate any rules.
    
- **Rate Limiting and Courtesy:**
    
    Avoid bombarding a server with rapid, successive requests. Implement delays (using time.sleep) between requests to reduce load on the server.
    
- **Data Privacy:**
    
    Be mindful of personal or sensitive data, and ensure that your scraping and subsequent use comply with privacy laws and regulations.
    

### 6. Summary

- **Web Scraping:**
    
    Automates the extraction of data from web pages, saving manual effort and enabling large-scale data collection.
    
- **HTML Basics:**
    
    HTML documents consist of nested elements (tags) with attributes. The DOM represents the hierarchical structure of these elements.
    
- **Core Tools:**
    - **`requests`:** Makes HTTP requests to download webpage content.
    - **BeautifulSoup:** Parses HTML and offers navigation functions to extract data from the DOM.
- **Practical Steps:**
    
    Download the page, parse the HTML, and extract the desired data (e.g., headings, links).
    
- **Ethical Considerations:**
    
    Always check a website’s `robots.txt` and terms of service, and be careful not to overload servers.
    

---

## Requests in Python

### 1. What Is the Requests Library?

**Requests** is a third-party Python library that provides a more human-friendly way to send HTTP/1.1 requests. It abstracts much of the complexity associated with making requests directly with built-in modules like `urllib`, letting you interact with web resources using simple functions.

**Key Benefits:**

- **Ease of Use:** Simple API for GET, POST, PUT, DELETE, etc.
- **Powerful Features:** Supports sessions, custom headers, authentication, cookies, and more.
- **Readable Syntax:** Code written with Requests tends to be more clear and concise.

## 2. Installation

To install Requests, use pip:

```bash
pip install requests
```

Once installed, you can import it into your Python scripts like so:

```python
import requests
```

### 3. Basic Usage

### a. A Simple GET Request

The simplest use of Requests is retrieving a web page:

```python
import requests

url = "<https://api.github.com>"
response = requests.get(url)

# Check status code
print("Status Code:", response.status_code)

# Get response text (if it's a text-based format, e.g., JSON)
print("Content:", response.text)
```

Here, `response` is an instance of `Response` that contains all the data returned by the server.

### b. Accessing the Response Data

The `Response` object provides various attributes and methods:

- **`.status_code`**
    
    Returns the HTTP status code (e.g., 200 for success).
    
- **`.headers`**
    
    A dictionary-like object containing the response headers.
    
- **`.text`**
    
    The content of the response, decoded to a string.
    
- **`.json()`**
    
    Parses the response as JSON and returns a Python dictionary (if the content is valid JSON).
    

**Example:**

```python
if response.status_code == 200:
    data = response.json()  # Automatically converts JSON to dictionary
    print("JSON Data:", data)
else:
    print("Request failed with status:", response.status_code)
```

### 4. HTTP Methods with Requests

Requests supports all the common HTTP methods:

### a. GET

Used to retrieve information.

```python
response = requests.get("<https://api.example.com/items>")
```

### b. POST

Used to create a resource. Pass data (e.g., JSON payload) with the request.

```python
payload = {"name": "Alice", "email": "alice@example.com"}
response = requests.post("<https://api.example.com/users>", json=payload)
```

Note that specifying `json=payload` automatically serializes the dictionary to JSON and sets the appropriate header (`Content-Type: application/json`).

### c. PUT and PATCH

- **PUT** replaces an entire resource.
- **PATCH** partially updates a resource.

```python
# PUT example
update_payload = {"name": "Alice Smith", "email": "alice.smith@example.com"}
resp_put = requests.put("<https://api.example.com/users/123>", json=update_payload)

# PATCH example
partial_update = {"email": "newalice@example.com"}
resp_patch = requests.patch("<https://api.example.com/users/123>", json=partial_update)
```

### d. DELETE

Used to remove a resource.

```python
resp_delete = requests.delete("<https://api.example.com/users/123>")
print("Delete status:", resp_delete.status_code)
```

### 5. Working with Parameters and Headers

### a. URL Parameters (Query Strings)

When making a GET request, you can pass query parameters via the `params` parameter:

```python
params = {"search": "python requests", "page": 2}
response = requests.get("<https://api.example.com/search>", params=params)
print("Final URL:", response.url)  # URL with encoded query parameters
```

### b. Custom Request Headers

You might need to send specific headers, for example, to authenticate or declare the content type:

```python
headers = {
    "Authorization": "Bearer YOUR_API_TOKEN",
    "Accept": "application/json"
}
response = requests.get("<https://api.example.com/secure-data>", headers=headers)
```

### 6. Handling Responses and Errors

### a. Checking Status Codes

Always check the response’s status code to handle errors gracefully:

```python
if response.status_code == 200:
    print("Success!")
else:
    print("Error:", response.status_code)
```

### b. Handling Exceptions

The Requests library can raise exceptions for network-related issues. Use try-except to catch these:

```python
try:
    response = requests.get("<https://api.example.com/data>", timeout=5)
    response.raise_for_status()  # Raises HTTPError for bad responses
except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error occurred: {http_err}")
except requests.exceptions.ConnectionError as conn_err:
    print(f"Connection error occurred: {conn_err}")
except requests.exceptions.Timeout as timeout_err:
    print(f"Timeout error: {timeout_err}")
except Exception as err:
    print(f"An error occurred: {err}")
```

### c. Response Content Types

If working with non-JSON content (e.g., XML or HTML), use `response.text` or, for binary content, `response.content`.

```python
# For binary data (like images)
image_response = requests.get("<https://example.com/image.png>")
with open("downloaded_image.png", "wb") as f:
    f.write(image_response.content)
```

### 7. Advanced Features: Sessions, Authentication, and More

### a. Using Sessions

A **Session** keeps certain parameters across requests, like cookies and headers. This is useful when working with login-required sites or APIs that maintain state.

```python
session = requests.Session()
session.headers.update({"Authorization": "Bearer YOUR_API_TOKEN"})

# Now use the session to make requests:
response = session.get("<https://api.example.com/profile>")
```

### b. Authentication

Requests supports several authentication mechanisms. For example, basic authentication:

```python
response = requests.get(
    "<https://api.example.com/protected>",
    auth=("username", "password")
)
```

Or using custom auth by subclassing `requests.auth.AuthBase`.

---

## Web scrapping using Pandas

### 1. Why Use Pandas for Web Scraping?

- **Extracting HTML Tables:**
    
    Many websites, such as financial data pages, statistics pages, or Wikipedia articles, include data formatted as HTML tables. Pandas provides the `read_html()` function, which automatically detects and extracts all tables into one or more DataFrames.
    
- **Seamless Data Analysis:**
    
    Once you've extracted the table(s) into Pandas DataFrames, you can immediately use its vast array of data manipulation, cleaning, and visualization functions—all in one ecosystem.
    

### 2. The `pandas.read_html()` Function

The key function for scraping tables with Pandas is `read_html()`. Here’s how it generally works:

- **Input:**
    
    You pass a URL (or a string containing HTML) into `read_html()`.
    
- **Internals:**
    
    Under the hood, `read_html()` uses libraries such as BeautifulSoup, lxml, or html5lib (you must have one of these installed) to parse the HTML and locate `<table>` elements.
    
- **Output:**
    
    The function returns a list of DataFrames—one for each detected table in the HTML.
    

### 3. Basic Usage

### a. Reading Tables Directly from a URL

Here is a straightforward example where we extract tables from a Wikipedia page:

```python
import pandas as pd

# URL containing one or more tables
url = "<https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)>"

# Retrieve all tables on the page (as a list of DataFrames)
tables = pd.read_html(url)

print(f"Number of tables found: {len(tables)}")
# Inspect the first table
print(tables[0].head())
```

- **Explanation:**
    - In this example, Pandas scans the HTML content provided in the URL for `<table>` elements.
    - All the tables are returned as a list of DataFrame objects. You can then select the one you need (e.g., the first table) and proceed with analysis.

### b. Reading HTML from a Local String or File

If you’ve downloaded HTML content using another method (for example, with `requests`), you can pass the HTML string to `read_html()`:

```python
import requests

url = "<https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)>"
response = requests.get(url)
html_content = response.text

# Extract tables from the HTML content stored in the string
tables = pd.read_html(html_content)
print(len(tables))
```

### 4. Advanced Features and Parameters

`read_html()` comes with several useful parameters:

- **`match`**:
    
    A string or regular expression that filters the tables whose text content matches the pattern.
    
    *Example:* Only return tables that contain the word “GDP”.
    
    ```python
    tables = pd.read_html(url, match="GDP")
    ```
    
- **`flavor`**:
    
    Some installations might support multiple HTML parsing libraries. Pandas automatically chooses one but you can specify it (e.g., `"lxml"` or `"bs4"`).
    
    ```python
    tables = pd.read_html(url, flavor="lxml")
    ```
    
- **`header`**:
    
    You may indicate which row (or rows) of the table should be used as the column names. For example, if the header is in the second row (index 1):
    
    ```python
    tables = pd.read_html(url, header=1)
    ```
    
- **`index_col`**:
    
    If you wish to use one of the columns as the index of the DataFrame.
    
- **`encoding`**:
    
    Set the encoding when parsing HTML from a non-UTF-8 source (e.g., `"ISO-8859-1"`).
    

These parameters help you tailor the table extraction process for different website structures.

### 5. Tips for Effective Table Extraction

- **Inspect the Web Page:**
    
    Before calling `read_html()`, use your browser’s developer tools (Inspect Element) to examine the HTML structure. Look for the `<table>` tags and note if you need specific parameters for header rows.
    
- **Multiple Tables:**
    
    If a page contains multiple tables, `read_html()` will return a list of all of them. Use `len(tables)` to check how many were found, and examine each DataFrame to determine which one you need.
    
- **Cleaning the DataFrame:**
    
    After extraction, use Pandas functions like `dropna()`, `rename()`, or `astype()` to clean and format the data as needed.
    
- **Error Handling:**
    
    Sometimes a page might not contain any HTML tables or the structure might be unusual. In such cases, handle exceptions gracefully to inform the user or log the issue for debugging.
    

## 6. Real-World Use Cases

- **Financial Analysis:**
    
    Scrape stock data, GDP tables, or financial reports published as HTML tables on news or government websites.
    
- **Research and Data Aggregation:**
    
    Collect and analyze data from sources such as Wikipedia, sports statistics websites, or academic publications.
    
- **Market Intelligence:**
    
    Monitor pricing, product listings, or reviews from e-commerce sites that often use tables to organize data.
    

---

## Working with different file formats

### 1. CSV (Comma-Separated Values)

**Overview:**

CSV files are plain text files where each line represents a record and fields are separated by commas (or another delimiter). They are widely used because they are human-readable and easily generated.

**Reading CSV Files:**

- Use `pd.read_csv()`
- Key parameters:
    - `sep`: Specify a custom delimiter (e.g., `sep="\\t"` for tab-delimited).
    - `header`: Identify the row to use as column names (default is row 0).
    - `encoding`: Often needed when handling non-UTF-8 files, e.g., `"ISO-8859-1"`.
    - `na_values`: Define strings that should be considered as missing values.

**Example:**

```python
import pandas as pd

df_csv = pd.read_csv("data.csv", sep=",", header=0, encoding="utf-8", na_values=["NA", "--"])
print(df_csv.head())
```

**Writing CSV Files:**

- Use `df.to_csv()`
- You can control facets such as:
    - `index=False`: Do not write row indices.
    - `sep`: Change the delimiter.
    - `encoding`: Specify encoding for the output.

**Example:**

```python
df_csv.to_csv("output.csv", index=False, sep=",", encoding="utf-8")
```

### 2. Excel Files

**Overview:**

Excel files (.xls and .xlsx) are common in business environments. They often contain multiple sheets and may have additional formatting.

**Reading Excel Files:**

- Use `pd.read_excel()`
- Key parameters include:
    - `sheet_name`: Specify which sheet to read (e.g., name or index).
    - `header`, `index_col`, and others behave similarly to CSV.

**Example:**

```python
df_excel = pd.read_excel("data.xlsx", sheet_name="Sheet1", header=0)
print(df_excel.head())
```

**Writing Excel Files:**

- Use `df.to_excel()`
- Can specify a sheet name and decide whether to include the index column.

**Example:**

```python
df_excel.to_excel("output.xlsx", index=False, sheet_name="CleanedData")
```

### 3. JSON (JavaScript Object Notation)

**Overview:**

JSON is a popular data interchange format that is text-based and supports nested structures. Many APIs return data in JSON format.

**Reading JSON Files:**

- Use `pd.read_json()`
- Parameters such as `orient` control how JSON records map to DataFrame dimensions (e.g., `"records"`, `"split"`).

**Example:**

```python
df_json = pd.read_json("data.json", orient="records")
print(df_json.head())
```

**Writing JSON Files:**

- Use `df.to_json()`
- You can choose an orientation and whether to indent the output for readability.

**Example:**

```python
df_json.to_json("output.json", orient="records", lines=True, indent=2)
```

### 4. HTML Files

**Overview:**

Some web pages provide data in table form. Pandas can scrape these tables directly using `pd.read_html()`.

**Reading HTML Tables:**

- Use `pd.read_html()`
- Returns a list of DataFrames for every `<table>` tag found in the HTML.

**Example:**

```python
tables = pd.read_html("<https://example.com/page-with-tables.html>")
print(f"Found {len(tables)} tables.")
df_table = tables[0]  # Choose the first table
print(df_table.head())
```

*Note:* Writing HTML is less common in Pandas but you can use DataFrame methods to convert to HTML (e.g., `df.to_html()`).

### 5. SQL Databases

**Overview:**

Many applications store data in structured databases. Pandas can interact directly with SQL databases using a SQLAlchemy engine.

**Reading from SQL:**

- Use `pd.read_sql(query, con)`
- Requires a valid connection (`con`) provided by SQLAlchemy or a database connector.

**Example:**

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///mydatabase.db")
df_sql = pd.read_sql("SELECT * FROM users", engine)
print(df_sql.head())
```

**Writing to SQL:**

- Use `df.to_sql(table_name, con, if_exists="replace")`
- `if_exists` controls whether to replace, append, or fail if the table exists.

**Example:**

```python
df_sql.to_sql("cleaned_users", engine, if_exists="replace", index=False)
```

### 6. Parquet

**Overview:**

Parquet is a columnar storage file format optimized for large-scale data processing and analytical queries. It is binary, compressed, and efficient.

**Reading Parquet Files:**

- Use `pd.read_parquet()`
- Requires libraries like `pyarrow` or `fastparquet`.

**Example:**

```python
df_parquet = pd.read_parquet("data.parquet")
print(df_parquet.head())
```

**Writing Parquet Files:**

- Use `df.to_parquet()`
- You can set compression types and other optimizations.

**Example:**

```python
df_parquet.to_parquet("output.parquet", compression="snappy", index=False)
```

### 7. Pickle

**Overview:**

Pickle is Python’s native object serialization format. It’s fast and preserves data types but is Python-specific and not safe for untrusted data.

**Reading Pickle Files:**

- Use `pd.read_pickle()`

**Example:**

```python
df_pickle = pd.read_pickle("data.pkl")
print(df_pickle.head())
```

**Writing Pickle Files:**

- Use `df.to_pickle()`

**Example:**

```python
df_pickle.to_pickle("output.pkl")
```

### 8. HDF5

**Overview:**

HDF5 is a file format suitable for storing and organizing large amounts of data. Pandas supports it via PyTables.

**Reading HDF5 Files:**

- Use `pd.read_hdf()`

**Example:**

```python
df_hdf = pd.read_hdf("data.h5", key="df")
print(df_hdf.head())
```

**Writing HDF5 Files:**

- Use `df.to_hdf()`

**Example:**

```python
df_hdf.to_hdf("output.h5", key="df", mode="w")
```

### 9. Best Practices for Working with Files

- **Inspect Your Data:**
    
    Always check the first few rows (`df.head()`) and the data types (`df.info()`) after loading data.
    
- **Specify Encodings:**
    
    When working with text files, specify the correct encoding to avoid mishandling characters.
    
- **Be Mindful of Memory:**
    
    For very large files, consider reading in chunks (`chunksize` parameter) to avoid memory errors.
    
- **Data Cleaning:**
    
    Often, the raw data will need transformation. Use methods like `dropna()`, `fillna()`, and type conversion functions (`astype()`) to prepare your DataFrame.
    
- **Error Handling:**
    
    Wrap file I/O operations in try-except blocks to gracefully handle errors (missing files, bad formats, etc.).
    

---