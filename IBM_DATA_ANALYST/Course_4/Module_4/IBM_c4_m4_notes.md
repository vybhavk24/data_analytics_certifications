# IBM_c4_m4

## Reading files with Open

Reading files is one of the core tasks in Python, and the built-in `open()` function provides a robust way to work with file I/O.

### 1. The `open()` Function

At its simplest, you use `open()` to create a file object, which you can then use to read (or write) the file's contents. The most common syntax is:

```python
file_object = open("filename.txt", "mode", encoding="utf-8")
```

- **Filename:** A string that specifies the path to the file.
- **Mode:** Determines how the file is to be used.
- **Encoding:** (Optional) Especially important for text files. For example, `"utf-8"` is standard.

### 2. File Modes

When you open a file, you need to specify the mode. Here are the most common ones:

- **`"r"` (Read Mode):** Open a file for reading. This is the default mode.
- **`"w"` (Write Mode):** Open a file for writing. If the file exists, its contents are overwritten.
- **`"a"` (Append Mode):** Open a file to append new information to the end.
- **`"r+"` (Read and Write Mode):** Open a file for both reading and writing.

For reading, you’ll most often use `"r"`. For example:

```python
file_obj = open("example.txt", "r")
```

### 3. Reading File Contents

Once you've opened a file, there are several methods you can use to read its contents:

### a. Using `read()`

The `read()` method reads the entire file as a single string.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
print(content)
```

*Tip:* Be cautious using `read()` on very large files since it loads everything into memory.

### b. Using `readline()`

The `readline()` method reads one line at a time.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    line1 = file.readline()
    line2 = file.readline()
    # You can process each line individually
    print("Line 1:", line1)
    print("Line 2:", line2)
```

### c. Using `readlines()`

This method reads all lines into a list, where each element is one line.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    lines = file.readlines()
for line in lines:
    print(line.strip())  # .strip() removes any leading/trailing whitespace
```

### d. Iterating Over the File Object

A memory-efficient way to read large files is to iterate directly over the file object, which reads one line at a time.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

### 4. Best Practices: Using the `with` Statement

It is recommended to use the `with` statement when opening files. This context manager automatically closes the file once the block is exited, even if an error occurs.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    data = file.read()
# No need to call file.close() here—the file is closed automatically.
```

This forward-thinking pattern prevents resource leaks and helps make your code cleaner.

### 5. Handling Encoding

Text files can be encoded in different character sets. It’s a best practice to always specify the encoding (like `"utf-8"`) to ensure consistency, particularly when working in an international environment or processing data from various sources.

```python
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
```

If you omit the encoding, Python will use a default that may vary by system, which might lead to unexpected errors (like `UnicodeDecodeError`).

### 6. Exception Handling When Reading Files

It’s wise to handle potential exceptions that may occur when working with files—such as the file not existing or permission issues. You can combine `with` and a try-except block:

```python
try:
    with open("example.txt", "r", encoding="utf-8") as file:
        content = file.read()
    print(content)
except FileNotFoundError:
    print("The file 'example.txt' was not found!")
except Exception as e:
    print(f"An error occurred: {e}")
```

This robustness is crucial in real-world data processing, where files might be missing or inaccessible.

### 7. Reading Binary Files

If you need to read non-text files (like images or executables), you should open files in binary mode by appending `"b"` to the mode:

```python
with open("image.png", "rb") as file:
    binary_data = file.read()
# binary_data is a bytes object that you can process accordingly.
```

## 8. Summary

- **`open()` Function:** Use it to access files, specifying the filename, mode, and optionally encoding.
- **Modes:** `"r"` for reading, `"w"` for writing, `"a"` for appending, and `"r+"` for both reading and writing.
- **Reading Methods:**
    - `read()`: Reads the whole file as one string.
    - `readline()`: Reads one line at a time.
    - `readlines()`: Reads all lines into a list.
- **Iteration:** Iterate over the file object for large files line-by-line.
- **Context Manager (`with`):** Ensures that files are properly closed even if an error occurs.
- **Handling Encoding:** Always specify the encoding to avoid errors with international data.
- **Exception Handling:** Use try-except blocks to gracefully handle issues like missing files.

---

## Writing files with Open:

### 1. The `open()` Function for Writing

You start by using the built-in `open()` function with an appropriate mode to write to a file. The basic syntax is:

```python
file_object = open("filename.txt", "mode", encoding="utf-8")
```

When writing files, the mode changes how Python interacts with the file, so let’s review the most common writing modes next.

### 2. File Modes for Writing

- **`"w"` (Write Mode):**
    
    Opens the file for writing. If the file exists, it truncates (overwrites) its contents; if it doesn’t exist, a new file is created.
    
    ```python
    with open("output.txt", "w", encoding="utf-8") as file:
        file.write("This is the first line.\\n")
        file.write("This will overwrite any existing content.\\n")
    ```
    
- **`"a"` (Append Mode):**
    
    Opens the file for appending. If the file exists, new data is added to the end; if it doesn't, a new file is created.
    
    ```python
    with open("output.txt", "a", encoding="utf-8") as file:
        file.write("This line is added to the end.\\n")
    ```
    
- **`"x"` (Exclusive Creation):**
    
    Opens the file for exclusive creation. If the file already exists, Python raises a `FileExistsError`. This mode is useful when you want to be sure you're not overwriting an existing file.
    
    ```python
    try:
        with open("newfile.txt", "x", encoding="utf-8") as file:
            file.write("Creating a new file safely!")
    except FileExistsError:
        print("File already exists!")
    ```
    
- **Combined Modes:**
    - **`"w+"`**: Opens the file for both writing and reading. It truncates the file if it exists.
    - **`"a+"`**: Opens the file for both appending and reading. The file pointer is at the end if the file exists.
    
    These modes are useful when you need to read back what you've written without opening the file twice.
    

### 3. Writing Text Data

Once you open a file in writing mode, you can use different methods to write data:

### a. Using `write()`

The `write()` method writes a string to the file. Note that it does not add a newline automatically.

```python
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("Hello, Data Science!\\n")
    file.write("This line is written to the file.\\n")
```

### b. Using `writelines()`

If you have a list (or any iterable) of strings, you can write them all at once with `writelines()`. However, remember that it doesn’t add newlines automatically.

```python
lines = [
    "First line.\\n",
    "Second line.\\n",
    "Third line.\\n"
]

with open("output.txt", "w", encoding="utf-8") as file:
    file.writelines(lines)
```

If your lines do not include newline characters, you can add them inside a comprehension:

```python
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w", encoding="utf-8") as file:
    file.writelines(f"{line}\\n" for line in lines)
```

### 4. Writing Binary Data

If you're working with binary files (like images or executables), open the file in binary mode by adding a `"b"` to the mode:

```python
with open("picture.jpg", "wb") as file:
    binary_data = b'\\xFF\\xD8\\xFF\\xE0'  # Example byte sequence for a JPEG header
    file.write(binary_data)
```

Binary mode is essential when you don’t want Python to perform any encoding or newline translations.

### 5. Best Practices: Using Context Managers

Always use the `with` statement when working with files. This ensures that the file is automatically closed after its block of code is executed, even if an error occurs.

```python
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("This file will be automatically closed.\\n")
```

By using `with`, you avoid issues like file handle leaks and ensure a cleaner code structure.

### 6. Exception Handling with File Writing

Just as with file reading, it’s a good idea to handle exceptions that may occur during file writing (such as permission errors or disk issues). Combine `with` with try-except blocks:

```python
try:
    with open("output.txt", "w", encoding="utf-8") as file:
        file.write("Writing to a file safely.\\n")
except IOError as e:
    print(f"An I/O error occurred: {e}")
```

This approach makes your code more robust and helps provide meaningful error messages when something goes wrong.

### 7. Flushing and Closing Files

- **Flushing:**
    
    Sometimes you may need to ensure that your data is physically written to disk even before closing the file. You can use the `flush()` method.
    
    ```python
    with open("output.txt", "w", encoding="utf-8") as file:
        file.write("Partial data...")
        file.flush()  # Forces Python to write the buffer to disk immediately.
        # Continue writing more data...
    ```
    
- **Closing:**
    
    While using `with` automatically closes the file, if you don't use it, ensure you call `close()` to free up system resources.
    
    ```python
    file = open("output.txt", "w", encoding="utf-8")
    file.write("Don't forget to close the file!")
    file.close()  # Manual closing is required if not using 'with'
    ```
    

### 8. Real-World Relevance for Data Analysts

- **Logging and Reporting:**
    
    Writing data to files is essential for logging error messages, creating reports, or storing the results of data processing tasks. Whether you’re saving a summary of an analysis or exporting transformed data, reliable file writing is key.
    
- **Data Export:**
    
    After cleaning and analyzing data, you might write the final results to a CSV, JSON, or text file for further use, presentation, or sharing with colleagues.
    
- **Automation:**
    
    Automation scripts frequently need to generate reports or backup data. Efficient file writing ensures smooth operation in scheduled tasks or data pipelines.
    

### 9. Hands-On Exercises

1. **Simple Text Logger:**
    
    Create a script that writes log messages to a file named `log.txt`. Use append mode so that each run adds new log lines.
    
    ```python
    import datetime
    
    log_message = f"{datetime.datetime.now()}: This is a log entry.\\n"
    with open("log.txt", "a", encoding="utf-8") as log_file:
        log_file.write(log_message)
    ```
    
2. **Report Generation:**
    
    Write a function that takes a list of strings (e.g., names or data entries) and writes them to a file, each on a new line.
    
    ```python
    def write_report(filename, data_list):
        with open(filename, "w", encoding="utf-8") as file:
            file.writelines(f"{item}\\n" for item in data_list)
    
    report_data = ["Data Point 1", "Data Point 2", "Data Point 3"]
    write_report("report.txt", report_data)
    ```
    
3. **Binary File Writing:**
    
    Write binary data to a new file. Create a simple byte sequence and save it to a file called `binary.dat`.
    
    ```python
    binary_data = bytes(range(256))  # Example byte array with values 0 to 255
    with open("binary.dat", "wb") as bin_file:
        bin_file.write(binary_data)
    ```
    

---

## Text vs Binary

### 1. Text Files

### How It Works

When you open a file in text mode (the default mode `"r"` for reading or `"w"` for writing, which is equivalent to `"rt"` or `"wt"`), Python treats the file’s contents as a sequence of characters (i.e., a string). Under the hood, here's what happens:

- **Encoding/Decoding:**
    - **Reading:** Python reads the raw bytes from storage and decodes them into a string using the specified (or default) encoding (commonly UTF-8).
    - **Writing:** Conversely, when you write a string, Python encodes the string into bytes before writing it to disk.
- **Newline Handling:**
    
    Python provides built-in newline translation. For example, on Windows, end-of-line sequences (`\\r\\n`) are automatically converted to `\\n` when reading (and vice versa when writing) unless you specify a particular `newline` parameter.
    
    - You may want to pass an explicit `newline` value (e.g., `newline=''`) if you need to handle line endings manually or preserve them exactly as in the file.

### Common Modes and Their Use-Cases for Text Files

- **`"r"` / `"rt"` (Read Text):**
    
    Opens an existing file for reading. The file is decoded into a string using the specified encoding.
    
    ```python
    with open("example.txt", "r", encoding="utf-8") as f:
        content = f.read()
    print(content)
    ```
    
- **`"w"` / `"wt"` (Write Text):**
    
    Opens a file for writing. If the file exists, its content is overwritten; if not, a new file is created. Python encodes the string into bytes before writing.
    
    ```python
    with open("output.txt", "w", encoding="utf-8") as f:
        f.write("This is a new file.\\nIt uses text encoding automatically.")
    ```
    
- **`"a"` / `"at"` (Append Text):**
    
    Opens a file for appending data at the end of the file without truncating it.
    
    ```python
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write("This line is appended to the file.\\n")
    ```
    

### Handling Various Text File Types

Text files come in many flavors—plain text (.txt), CSV, JSON, XML, etc.—but they mostly share the same underlying behavior in Python:

- **CSV, JSON, XML, and Others:**
    
    Although these formats have their own syntax, when reading and writing them as basic files, Python treats them as text. You decode and encode them just as you would with any other text file. (In advanced applications, you may use specialized libraries like `csv`, `json`, or `xml.etree.ElementTree` to parse and produce these formats.)
    
- **Custom Encodings and Locale Differences:**
    
    Sometimes you may need to work with legacy files or files in an encoding other than UTF-8 (e.g., ISO-8859-1, Windows-1252). In such cases, explicitly specify the encoding:
    
    ```python
    with open("legacy_file.txt", "r", encoding="iso-8859-1") as f:
        legacy_content = f.read()
    ```
    

### 2. Binary Files

### How It Works

When you open a file in binary mode (by adding `"b"` to the mode, such as `"rb"` or `"wb"`), Python does not perform any encoding or decoding. The file is read or written as raw bytes—it treats the file as a sequence of bytes rather than a sequence of characters.

- **No Translation:**
    - **Reading:** The file’s contents are returned as a `bytes` object.
    - **Writing:** You must supply a `bytes` object (or something that can be converted to bytes) to write.
- **No Newline Conversion:**
    
    Binary mode means Python does not alter newline characters. Every byte is read or written exactly as it is stored on disk.
    

### Common Modes and Their Use-Cases for Binary Files

- **`"rb"` (Read Binary):**
    
    Opens a file for reading in binary mode. Useful for images, video, audio, executables, or any file that isn’t plain text.
    
    ```python
    with open("image.png", "rb") as f:
        image_data = f.read()
    # image_data is a bytes object containing the raw data of the image.
    ```
    
- **`"wb"` (Write Binary):**
    
    Opens a file for writing binary data. If the file exists, it is truncated.
    
    ```python
    # Suppose we have some binary content in a bytes object
    binary_content = bytes(range(256))  # Sample bytes from 0 to 255
    with open("output.bin", "wb") as f:
        f.write(binary_content)
    ```
    
- **Other Binary Modes:**
    
    Modes like `"ab"` for appending, or `"rb+"` for reading and writing in binary mode, function as expected, but all with data represented as bytes.
    

### Handling Different Kinds of Binary Files

Everything from images (JPEG, PNG), audio files (MP3, WAV), to compressed files (ZIP, TAR) is accessed in a similar fashion because they are all stored as raw bytes:

- **Image Files:**
    
    When processing images (even if using libraries like Pillow), you first open them in binary mode.
    
- **Audio/Video Files:**
    
    Typically processed as binary data, unless you are using a tool or library that abstracts away the low-level details.
    
- **Executable Files or Databases:**
    
    Similarly, these are read and written as binary data.
    

Because there is no conversion or newline handling in binary mode, the byte values remain untouched, offering precise control over the data.

### 3. Best Practices and Considerations

### Using Context Managers

Always use the `with` statement to open files (both text and binary) so that they are automatically closed after the block of code executes. This prevents resource leaks and is safer in cases of errors.

```python
# Text file example
with open("data.txt", "r", encoding="utf-8") as file:
    text = file.read()

# Binary file example
with open("picture.jpg", "rb") as file:
    image_bytes = file.read()
```

### Exception Handling

File operations can fail (file not found, permission errors, encoding problems) so wrapping your file I/O operations in try-except blocks is a good precaution.

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()
except FileNotFoundError:
    print("The file was not found.")
except Exception as e:
    print(f"An error occurred: {e}")

```

### Choosing the Right Mode

- **Text mode:** Use when you are dealing with human-readable content where the file content needs to be interpreted as characters. Always consider the encoding.
- **Binary mode:** Use when the file contains non-text data or when you wish to process data byte by byte.

---

## Pandas: Loading the data file:

Pandas is one of the most popular libraries for data analysis in Python, and one of its core strengths is the ability to load data from a wide variety of file formats into **DataFrames**—Pandas’ primary data structure for handling tabular data.

### 1. Loading CSV Files

The most common format in data analysis is CSV (Comma-Separated Values). Pandas provides the `read_csv()` function for this.

### Basic Usage

```python
import pandas as pd

# Load a CSV file into a DataFrame
df = pd.read_csv("data.csv")
print(df.head())  # Display the first few rows
```

### Common Parameters

- **`sep`**: Specify a different delimiter if your file is not comma-separated (e.g., tab-delimited use `sep="\\t"`).
- **`header`**: Indicates the row number to use as the column names (default is `header=0`).
- **`index_col`**: Choose a column to use as the row labels of the DataFrame.
- **`encoding`**: Set the text encoding (e.g., `"utf-8"` or `"ISO-8859-1"`).
- **`dtype`**: Control the data types for certain columns.
- **`na_values`**: Specify additional strings to recognize as NA/NaN.
- **`parse_dates`**: Instruct Pandas to parse columns as datetime objects.

**Example with parameters:**

```python
df = pd.read_csv(
    "data.csv",
    sep=",",                    # Delimiter
    header=0,                   # First row as header
    index_col="ID",             # Use "ID" column as the DataFrame index
    encoding="utf-8",           # Specify encoding
    dtype={"age": int},         # Ensure 'age' is read as an integer
    na_values=["NA", "--"],     # Additional strings that represent missing values
    parse_dates=["registration_date"]  # Parse 'registration_date' as datetime
)
print(df.info())
```

This approach gives you full control over how rows and columns are interpreted during import.

### 2. Loading Excel Files

Pandas can read Excel files (both `.xls` and `.xlsx`) using the `read_excel()` function. Note that you may need to install additional libraries like `openpyxl` or `xlrd`.

### Basic Usage

```python
df_excel = pd.read_excel("data.xlsx")
print(df_excel.head())
```

### Key Parameters

- **`sheet_name`**: Specify the sheet name or index (default is the first sheet).
- **`header`**, **`index_col`**, **`dtype`**, etc., work similarly to `read_csv()`.

**Example:**

```python
df_excel = pd.read_excel(
    "data.xlsx",
    sheet_name="Sales",  # Load a specific sheet named "Sales"
    header=0,
    index_col=None,
    encoding="utf-8"  # Note: Encoding might be inferred automatically for Excel files.
)
print(df_excel.head())
```

### 3. Loading JSON Files

JSON is a widely used format for structured data (often used in web data and APIs). You can load JSON data using `read_json()`.

### Basic Usage

```python
df_json = pd.read_json("data.json")
print(df_json.head())
```

### When to Use

- JSON data can be nested; Pandas will try to normalize the nested structures but sometimes you might need to use additional parameters (or libraries like `json_normalize`) to flatten the data structure.

### 4. Loading Other Formats

Pandas offers many specialized functions to load other data formats, such as:

- **`read_sql()`**: Load data directly from a SQL query or database connection.
- **`read_html()`**: Parse tables from HTML content.
- **`read_parquet()`**: Load data from Apache Parquet files, leveraging efficient columnar storage (requires the `pyarrow` or `fastparquet` library).
- **`read_pickle()`**: Load data from a pickled Pandas object.

For example, to load a Parquet file:

```python
df_parquet = pd.read_parquet("data.parquet")
print(df_parquet.head())
```

### 5. Best Practices and Tips

- **Preview the Data:** Always start with methods like `df.head()`, `df.info()`, or `df.describe()` to get a sense of the data structure and identify potential issues (e.g., missing values, wrong data types).
- **Specify Encoding:** When loading text-based files (like CSV or JSON), explicitly setting the encoding avoids surprises with non-ASCII characters.
- **Set `parse_dates` for Datetime Columns:** This ensures date/time data is read as a datetime object, making further analysis and visualization easier.
- **Handle Missing Values:** Use `na_values` to ensure that all representations of missing data (such as "N/A", "--", etc.) are correctly interpreted as NaN.
- **Memory Optimization:** For large files, consider reading in chunks (using the `chunksize` parameter) or specifying data types manually to limit memory usage.

### 6. Real-World Relevance

For data analysts, correctly loading data is the first essential step in the analysis pipeline. Whether you are preparing data for machine learning, generating business insights, or simply cleaning up incoming raw data, Pandas allows you to ingest data correctly and reliably. 

The flexibility of Pandas' data I/O functions makes it simple to switch between different data sources and formats, integrate web data, and work seamlessly with data stored in databases or cloud storage.

### 7. Hands-On Exercises

1. **CSV Practice:**
    - Download a sample CSV dataset from an online source (for example, a dataset from [Kaggle](https://www.kaggle.com/datasets)).
    - Load it using `read_csv()` with at least three parameters (e.g., `sep`, `encoding`, `parse_dates`) and print the summary of the DataFrame.
2. **Excel and JSON:**
    - Create or download a simple Excel file with multiple sheets. Load a specific sheet by name using `read_excel()`.
    - Similarly, find a small JSON file online (or create one using Python’s `json` module) and load it into a DataFrame using `read_json()`. Inspect the results to see how nested data is handled.
3. **Advanced Loading:**
    - Use `read_csv()` with the `chunksize` parameter to load a very large file in parts. Iterate over the chunks and compute simple statistics (like the mean of a numeric column) on each chunk, then aggregate the results.

---

## Pandas: Working with and Saving data:

### A. Working with Data in Pandas

Once your data is loaded into a DataFrame (via `read_csv()`, `read_excel()`, etc.), you have a powerful suite of operations at your disposal. Here’s a quick tour of common operations:

### 1. Inspecting Data

- **Preview Data:**
Use `head()`, `tail()`, and `sample()` to take a peek at your data.
    
    ```python
    df.head()     # First 5 rows
    df.tail(3)    # Last 3 rows
    df.sample(5)  # Random sample of 5 rows
    ```
    
- **Understand Structure:**
Use `info()` and `describe()` for metadata and summary statistics.
    
    ```python
    df.info()      # Get column names, data types, and non-null counts
    df.describe()  # Get statistical summary for numerical columns
    ```
    

### 2. Data Cleaning and Transformation

- **Handling Missing Values:**
You can drop missing values or fill them:
    
    ```python
    df.dropna(inplace=True)          # Remove any rows with missing values
    df.fillna(value={'col1': 0}, inplace=True)  # Replace NaN in 'col1' with 0
    ```
    
- **Filtering & Sorting:**
Filter rows that meet a condition:
And sort your data:
    
    ```python
    # Select rows where 'age' is greater than 30
    df_filtered = df[df['age'] > 30]
    ```
    
    ```python
    df_sorted = df.sort_values(by="salary", ascending=False)
    ```
    
- **Adding or Modifying Columns:**
Create new columns or transform existing ones:
    
    ```python
    df['net_income'] = df['gross_income'] - df['tax']
    df['full_name'] = df['first_name'] + " " + df['last_name']
    ```
    
- **Renaming Columns:**
You'll want to rename columns for clarity:
    
    ```python
    df.rename(columns={'old_name': 'new_name'}, inplace=True)
    ```
    

### 3. Aggregating and Grouping

- **Group By:**
Combine rows according to one or more keys and compute summary statistics:
    
    ```python
    grouped = df.groupby("department")
    print(grouped["salary"].mean())  # Average salary per department
    ```
    
- **Pivot Tables:**
Create pivot tables to summarize data in a multi-dimensional way:
    
    ```python
    pivot = df.pivot_table(values="sales", index="region", columns="quarter", aggfunc="sum")
    print(pivot)
    ```
    

### 4. Merging and Joining DataFrames

- **Concatenation or Merging:**
Combine DataFrames horizontally or vertically:
    
    ```python
    df_merged = pd.merge(df_left, df_right, on="employee_id", how="inner")
    df_concat = pd.concat([df1, df2], axis=0)  # Stacking vertically
    ```
    

By chaining these operations, you can transform raw data into clean, enriched, and summarized data ready for analysis or reporting.

### B. Saving Data in Various Formats

After processing your data, you’ll typically want to save the resulting DataFrame. Pandas offers several methods to export your data.

### 1. Saving as CSV

**Use Case:** CSVs are universal, human-readable, and a common interchange format.

```python
# Save without row indices, which are often not needed
df.to_csv("cleaned_data.csv", index=False, encoding="utf-8")
```

**Key Parameters:**

- `index`: Whether to include row labels (set to `False` to omit).
- `sep`: The separator (default is a comma, but you can change it, e.g., `sep="\\t"` for tabs).
- `encoding`: Ensures proper character handling. UTF-8 is often a good choice.

### 2. Saving as Excel

**Use Case:** When you need a file that can be readily opened in spreadsheet applications.

```python
df.to_excel("report.xlsx", index=False, sheet_name="Summary")
```

**Key Points:**

- Requires packages like `openpyxl` (for `.xlsx`) or `xlwt` (for `.xls`).
- You can save multiple sheets using `ExcelWriter`.

### 3. Saving as JSON

**Use Case:** JSON is perfect for web applications or when working with hierarchical data.

```python
df.to_json("data.json", orient="records", lines=True)
```

**Key Parameters:**

- `orient`: Controls the format of the JSON (e.g., `records`, `split`, `index`).
- `lines`: If `True`, writes each record on a separate line (useful for streaming).

### 4. Saving as Parquet

**Use Case:** For large-scale data processing, Parquet files are efficient and preserve schema information.

```python
df.to_parquet("data.parquet", index=False)
```

**Note:** Requires external libraries such as `pyarrow` or `fastparquet`.

### 5. Saving as Pickle

**Use Case:** To save Python-specific objects quickly with serialization.

```python
df.to_pickle("data.pkl")
```

**Caution:** Pickled files are Python-specific and not secure against erroneous or malicious data. Only unpickle data you trust.

### Tips and Best Practices

- **Validate Before Saving:**
    
    Always inspect your DataFrame (using `df.head()`, `df.info()` etc.) before saving to ensure transformations have been applied as expected.
    
- **Specify Encoding:**
    
    When saving text files (CSV, Excel, JSON), specify the encoding to avoid issues with non-ASCII characters.
    
- **Consider File Size and Performance:**
    
    For large datasets, formats like Parquet offer optimized storage and faster read/write operations.
    
- **Backup Original Data:**
    
    Before overwriting files, ensure you have appropriate backups if necessary.
    
- **Automation Script:**
    
    In a production pipeline, work with data transformations and then lovingly save your results so downstream processes or reports have the most recent and clean data available.
    

### Real-World Example

Imagine you’ve loaded a raw customer dataset, cleaned it, and computed metrics such as average spend per region. You might then want to save the summarized data as both CSV (for reporting) and Excel (for an executive dashboard):

```python
# After processing your DataFrame 'df'
summary = df.groupby("region")["spend"].mean().reset_index()
summary.rename(columns={"spend": "avg_spend"}, inplace=True)

# Save as CSV for archival or ingestion by another system
summary.to_csv("region_summary.csv", index=False, encoding="utf-8")

# Save as Excel for business presentations
summary.to_excel("region_summary.xlsx", index=False, sheet_name="Avg Spend")
```

## Summary

- **Working with Data:**
Use methods like filtering, grouping, merging, and transforming operations to clean and manipulate your DataFrame.
- **Saving Data:**
Pandas provides several methods to export your DataFrame into formats including CSV, Excel, JSON, Parquet, and Pickle.
- **Best Practices:**
Always inspect your data before saving, choose the right format based on your needs (human readability vs. performance), and take advantage of parameters like `encoding`, `index`, and `sep` to fine-tune your output.

---

## Series and Dataframes in Pandas

### 1. Pandas Series

### What Is a Series?

A **Series** is a one-dimensional labeled array that can hold any data type (integers, strings, floats, Python objects, etc.). Think of it as a column in a spreadsheet or a one-dimensional array that adds labels (called **indices**) to each element. Because of these labels, you can access data by index label rather than by integer position only.

### Key Characteristics

- **One-Dimensional:**
    
    A Series only has one axis (the index), but this axis can be labeled.
    
- **Homogeneous Data:**
    
    While each element in a Series can theoretically be of any type, typically, a single Series stores one type of data (though it can be mixed if not enforced).
    
- **Indexing:**
    
    The index allows for fast lookups. You can assign a custom index or let Pandas create one automatically (default index starts at 0).
    

### Creating a Series

There are several ways to create a Series:

### a. From a List

```python
import pandas as pd

data = [10, 20, 30, 40]
s = pd.Series(data)
print(s)
# Output:
# 0    10
# 1    20
# 2    30
# 3    40
# dtype: int64
```

### b. With a Custom Index

```python
s_custom = pd.Series(data, index=["a", "b", "c", "d"])
print(s_custom)
# Output:
# a    10
# b    20
# c    30
# d    40
# dtype: int64
```

### c. From a Dictionary

Each key in the dictionary becomes an index label.

```python
data_dict = {"x": 100, "y": 200, "z": 300}
s_dict = pd.Series(data_dict)
print(s_dict)
# Output:
# x    100
# y    200
# z    300
# dtype: int64
```

### Common Operations on Series

- **Accessing Elements:**
    
    You can access elements using labels or positions.
    
    ```python
    print(s_custom["a"])   # Outputs: 10
    print(s_custom[0])     # Also outputs: 10 (default integer indexing)
    ```
    
- **Arithmetic Operations:**
    
    Operations are performed element-wise.
    
    ```python
    s2 = s_custom * 2
    print(s2)
    # Output:
    # a    20
    # b    40
    # c    60
    # d    80
    # dtype: int64
    ```
    
- **Statistical Functions:**
    
    Easily compute metrics like mean, sum, etc.
    
    ```python
    print(s_custom.mean())  # Computes the average value.
    print(s_custom.sum())   # Sum of all values.
    ```
    
- **Boolean Indexing:**
    
    Filter the Series based on conditions.
    
    ```python
    filtered = s_custom[s_custom > 20]
    print(filtered)
    # Output:
    # c    30
    # d    40
    # dtype: int64
    ```
    

### 2. Pandas DataFrame

### What Is a DataFrame?

A **DataFrame** is a two-dimensional, size-mutable, and potentially heterogeneous tabular data structure with labeled axes (rows and columns). Think of it as a spreadsheet or SQL table in memory. It is the most widely used structure in Pandas for analyzing and processing data.

### Key Characteristics

- **Two-Dimensional:**
    
    The data is arranged in rows and columns.
    
- **Labeled Axes:**
    
    Both rows and columns have index labels, making data selection and manipulation more intuitive.
    
- **Heterogeneous Data:**
    
    Different columns can hold different data types (e.g., strings, integers, floats).
    

### Creating a DataFrame

There are several ways to create a DataFrame:

### a. From a Dictionary of Lists

Each key becomes a column label, and the corresponding list holds the column data.

```python
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "Salary": [50000, 60000, 70000]
}
df = pd.DataFrame(data)
print(df)
# Output:
#       Name  Age  Salary
# 0    Alice   25   50000
# 1      Bob   30   60000
# 2  Charlie   35   70000
```

### b. From a List of Dictionaries

Each dictionary represents a row, and keys are used to form the columns.

```python
data_list = [
    {"Name": "Alice", "Age": 25, "Salary": 50000},
    {"Name": "Bob", "Age": 30, "Salary": 60000},
    {"Name": "Charlie", "Age": 35, "Salary": 70000}
]
df2 = pd.DataFrame(data_list)
print(df2)
```

### c. From a CSV or Excel File

Load data directly using functions like `pd.read_csv()` or `pd.read_excel()` (covered in-depth in previous topics).

```python
df_csv = pd.read_csv("data.csv")
```

### Common Operations on DataFrames

- **Viewing Data:**
    
    Use `df.head()` or `df.tail()` to see the first or last few rows.
    
    ```python
    print(df.head())
    ```
    
- **Accessing Columns and Rows:**
    - **Columns:**
        
        Access a column as a Series.
        
        ```python
        ages = df["Age"]
        print(ages)
        ```
        
    - **Rows:**
        
        Use `.loc` for label-based selection or `.iloc` for position-based selection.
        
        ```python
        row_0 = df.loc[0]    # Access row by label (assuming index labels are the default integers)
        row_1 = df.iloc[1]   # Access row by position
        print(row_0, row_1)
        ```
        
- **Filtering Data:**
    
    Filter rows based on a condition.
    
    ```python
    df_filtered = df[df["Age"] > 25]
    print(df_filtered)
    ```
    
- **Adding and Modifying Columns:**
    
    Create new columns or modify existing ones.
    
    ```python
    df['Bonus'] = df['Salary'] * 0.10  # Compute a 10% bonus for each employee
    ```
    
- **Merging and Joining DataFrames:**
    
    Combine multiple DataFrames using functions like `merge()`, `concat()`, or `join()`.
    
    ```python
    df1 = pd.DataFrame({"ID": [1, 2, 3], "Name": ["Alice", "Bob", "Charlie"]})
    df2 = pd.DataFrame({"ID": [1, 2, 3], "Salary": [50000, 60000, 70000]})
    merged_df = pd.merge(df1, df2, on="ID")
    print(merged_df)
    ```
    
- **Grouping and Aggregating:**
    
    Use `groupby()` to summarize data.
    
    ```python
    avg_salary = df.groupby("Age")["Salary"].mean()
    print(avg_salary)
    ```
    

### Additional Functionality

- **Pivot Tables:**
    
    Create pivot tables to summarize data over multiple dimensions.
    
    ```python
    pivot = df.pivot_table(values="Salary", index="Name", aggfunc="sum")
    print(pivot)
    ```
    
- **Handling Missing Data:**
    
    Methods such as `dropna()` and `fillna()` help manage missing values gracefully.
    
    ```python
    df_clean = df.dropna()  # Drops rows with missing values
    df_filled = df.fillna(0)  # Replaces missing values with 0
    ```
    
- **Statistics and Descriptions:**
    
    Use `describe()` to quickly generate summary statistics.
    
    ```python
    print(df.describe())
    ```
    
- **Sorting Data:**
    
    Sort by one or more columns.
    
    ```python
    df_sorted = df.sort_values(by="Salary", ascending=False)
    print(df_sorted)
    ```
    

### 3. How They Work Together

In practical use, a **DataFrame** is essentially a collection of **Series** objects—each column in a DataFrame is a Series. This internal structure means that operations on DataFrames often delegate to similar operations on Series (e.g., element-wise arithmetic, filtering, and aggregations).

For example, if you perform an arithmetic operation on a DataFrame column:

```python
df["Salary_Bonus"] = df["Salary"] * 1.10  # Increasing each Salary by 10%
```

This operation acts on the Series representing the "Salary" column and returns a new Series that is added as a new column to the DataFrame.

### 4. Real-World Relevance

- **Exploratory Data Analysis (EDA):**
    
    Use DataFrames to explore and visualize data, compute correlations, and generate descriptive statistics.
    
- **Data Cleaning:**
    
    Use the rich set of DataFrame methods to handle missing data, remove duplicates, and transform data into a usable format.
    
- **Machine Learning Pipelines:**
    
    Feed clean and well-structured data stored in DataFrames into machine learning models using libraries like scikit-learn.
    
- **Time Series Analysis:**
    
    Pandas offers specialized support for time series data (e.g., resampling, date-indexing) in both Series and DataFrames.
    

### 5. Summary

- A **Pandas Series** is a one-dimensional labeled array, similar to a single column of data.
    - You can create it from lists, dictionaries, or other arrays.
    - It supports powerful indexing, arithmetic operations, and adaptive filtering.
- A **Pandas DataFrame** is a two-dimensional table with labeled rows and columns. It consists of multiple Series and provides extensive functionality for:
    - Data cleaning and transformation.
    - Data aggregation, merging, and pivoting.
    - Statistical analysis and visualization.

---

## One dimensional array:

NumPy (Numerical Python) provides an efficient means for performing operations on large arrays and matrices of numeric data. 

One-dimensional arrays (or 1D arrays) are the simplest form of a NumPy array, and understanding them will set the stage for all your numerical computing tasks.

### 1. What Are One-Dimensional NumPy Arrays?

A one-dimensional NumPy array is essentially a list of numbers stored in a contiguous memory block. Unlike Python lists, NumPy arrays are homogeneous—they contain elements of the same data type—and are optimized for speed and efficiency through vectorized operations.

**Key Features:**

- **Homogeneity:** All elements share the same data type (`dtype`).
- **Fixed Size:** Once created, the size of an array doesn't change (though you can create new arrays with modifications).
- **Vectorized Operations:** Arithmetic and other operations are performed element-wise quickly using low-level implementations.
- **Efficient Memory Use:** Data is stored in contiguous memory, leading to performance gains in computation.

### 2. Creating One-Dimensional Arrays

There are several methods to create 1D arrays in NumPy:

### a. Using `np.array()`

Convert a Python list (or other sequences) to a NumPy array.

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr)
# Output: [1 2 3 4 5]
```

### b. Using `np.arange()`

Create an array with regularly spaced values within a specified interval.

```python
arr_arange = np.arange(0, 10, 2)  # Start at 0, stop before 10, step of 2
print(arr_arange)
# Output: [0 2 4 6 8]
```

### c. Using `np.linspace()`

Generate an array of evenly spaced numbers over a specified interval. This is particularly useful when you want a fixed number of values within a range.

```python
arr_linspace = np.linspace(0, 1, 5)  # Five values between 0 and 1
print(arr_linspace)
# Output: [0.   0.25 0.5  0.75 1.  ]
```

### d. Using `np.ones()` and `np.zeros()`

Create arrays filled with ones or zeros.

```python
ones_array = np.ones(5)  # One-dimensional array of five ones
zeros_array = np.zeros(5)  # One-dimensional array of five zeros
print("Ones:", ones_array)
print("Zeros:", zeros_array)
```

### 3. Key Properties of One-Dimensional Arrays

Once you have a 1D array, there are several important attributes you should know about:

- **`ndim` (Number of Dimensions):** For 1D arrays, this is always 1.
    
    ```python
    print(arr.ndim)  # Output: 1
    ```
    
- **`shape`:** Gives a tuple indicating the size along each dimension.
    
    ```python
    print(arr.shape)  # Output: (5,)
    ```
    
- **`dtype`:** The data type of the elements.
    
    ```python
    print(arr.dtype)  # E.g., int64
    ```
    
- **`size`:** Total number of elements in the array.
    
    ```python
    print(arr.size)  # Output: 5
    ```
    

### 4. Indexing, Slicing, and Iteration

### a. Indexing

You access elements in a 1D array similar to a list, using zero-based indexing.

```python
print(arr[0])  # First element: 1
print(arr[-1])  # Last element: 5
```

### b. Slicing

Extract a section of the array.

```python
sub_arr = arr[1:4]  # Elements from index 1 to 3
print(sub_arr)  # Output: [2 3 4]
```

### c. Iteration

You can loop through the array elements:

```python
for element in arr:
    print(element)
```

### 5. Arithmetic and Vectorized Operations

One of NumPy’s most powerful features is the ability to perform arithmetic operations on arrays element-wise without explicit loops.

```python
a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])

# Element-wise operations:
sum_arr = a + b        # [11, 22, 33, 44, 55]
diff_arr = b - a       # [9, 18, 27, 36, 45]
prod_arr = a * 2       # [2, 4, 6, 8, 10]
div_arr = b / a        # [10.0, 10.0, 10.0, 10.0, 10.0]

print("Sum:", sum_arr)
print("Difference:", diff_arr)
print("Product:", prod_arr)
print("Division:", div_arr)
```

These operations are highly optimized and usually run orders of magnitude faster than equivalent Python loops.

### 6. Broadcasting and Universal Functions (ufuncs)

### Broadcasting

Broadcasting allows you to perform operations on arrays of different shapes. With 1D arrays, this typically means applying scalar values or combining arrays with different lengths (if they are compatible).

```python
scalar_mult = a * 3  # Multiply every element by 3
print("Scalar Multiplication:", scalar_mult)
```

### Universal Functions (ufuncs)

NumPy provides a set of vectorized functions that operate element-wise on arrays. For example, mathematical functions like `np.sin()`, `np.exp()`, and `np.sqrt()`.

```python
sin_values = np.sin(a)  # Sine values of each element in a
sqrt_values = np.sqrt(a)  # Square roots of each element in a
print("Sine Values:", sin_values)
print("Square Roots:", sqrt_values)
```

## 7. Boolean Indexing and Filtering

You can create a boolean mask to select elements that meet a condition:

```python
mask = a > 3   # Creates an array like [False, False, False, True, True]
filtered = a[mask]
print("Elements greater than 3:", filtered)
```

This is especially useful for data filtering and analysis.

### 8. Modifying Arrays: In-Place Operations and Views

### In-Place Operations

Many operations can modify the array in place using operators like `+=`, `-=`, etc.

```python
a += 1  # Each element of a is incremented by 1
print("After In-Place Increment:", a)
```

### Views Versus Copies

Slicing generally returns a **view** on the original array, meaning that modifications to the slice affect the original array. Use the `copy()` method to create an independent copy.

```python
sub_a = a[1:4]
sub_a[0] = 100
print("Modified sub_a:", sub_a)
print("Original a after modifying sub_a:", a)

# Creating a copy:
sub_a_copy = a[1:4].copy()
sub_a_copy[0] = 999
print("sub_a_copy:", sub_a_copy)
print("Original a remains unchanged:", a)
```

### 9. Real-World Relevance

One-dimensional NumPy arrays are ubiquitous in scientific computing, data analysis, and machine learning. They often represent:

- **Vectors in Mathematics:** Computation of dot products, norms, and other vector operations.
- **Time-Series Data:** A single sequence of observations recorded over time.
- **Signal Processing:** Audio signals and other one-dimensional data streams.
- **Data Extraction:** Intermediate representations of data columns from larger datasets.

Their efficiency and ease of manipulation make them ideal for both simple tasks and as building blocks for higher-dimensional data structures.

### 10. Hands-On Exercises

1. **Basic Array Operations:**
    
    Create a 1D array of the first 10 positive integers using `np.arange()`. Then compute a new array that represents the square of each element. Finally, filter out all elements greater than 25.
    
    ```python
    arr = np.arange(1, 11)
    squares = arr ** 2
    filtered_squares = squares[squares > 25]
    print("Original Array:", arr)
    print("Squares:", squares)
    print("Filtered (Squares > 25):", filtered_squares)
    ```
    
2. **Statistical Analysis:**
    
    Given a 1D array of random numbers, calculate the mean, median, and standard deviation using NumPy functions.
    
    ```python
    random_arr = np.random.rand(10)  # Array of 10 random numbers between 0 and 1
    mean_val = np.mean(random_arr)
    median_val = np.median(random_arr)
    std_val = np.std(random_arr)
    print("Random Array:", random_arr)
    print("Mean:", mean_val)
    print("Median:", median_val)
    print("Standard Deviation:", std_val)
    ```
    
3. **Boolean Filtering:**
    
    Create an array of 20 random integers between 0 and 50 and extract only the even numbers.
    
    ```python
    rand_ints = np.random.randint(0, 51, size=20)
    even_mask = rand_ints % 2 == 0
    even_ints = rand_ints[even_mask]
    print("Random Integers:", rand_ints)
    print("Filtered Even Integers:", even_ints)
    ```
    

---

## Two dimensional Numpy:

Two-dimensional (2D) arrays are essentially matrices—a grid of data with rows and columns—and they form the basis for most data representations in numerical computing, data analysis, and machine learning.

### 1. What Are Two-Dimensional NumPy Arrays?

- **Definition:** A 2D NumPy array is an ordered collection of elements arranged in rows and columns.
- **Structure:** If an array has shape `(m, n)`, then it has `m` rows and `n` columns.
- **Use Cases:** They are used to represent matrices, images, grids, tables of data, and more.

### 2. Creating 2D Arrays

### a. From Nested Lists

You can create a 2D array directly using a list of lists:

```python
import numpy as np

# Each inner list represents a row
arr_2d = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
print(arr_2d)
```

### b. Using Functions with Reshaping

**`np.arange()` and `reshape()`:** Create a range and reshape it into 2D.

```python
# Create 9 elements and reshape into a 3x3 matrix
arr_2d = np.arange(1, 10).reshape(3, 3)
print(arr_2d)
```

**`np.zeros()` and `np.ones()`:** Create arrays filled with zeros or ones.

```python
zeros_2d = np.zeros((3, 4))  # 3 rows, 4 columns of zeros
ones_2d = np.ones((2, 5))    # 2 rows, 5 columns of ones
print("Zeros:\\n", zeros_2d)
print("Ones:\\n", ones_2d)
```

**`np.eye()`:** Create an identity matrix.

```python
identity = np.eye(4)  # 4x4 identity matrix
print(identity)
```

### 3. Key Properties

Every NumPy array has several descriptive properties:

- **`ndim`:** Number of dimensions. For 2D arrays, `ndim` is 2.
    
    ```python
    print(arr_2d.ndim)  # Output: 2
    ```
    
- **`shape`:** Tuple representing the dimensions, e.g., `(3, 3)` for a 3×3 matrix.
    
    ```python
    print(arr_2d.shape)  # Output: (3, 3)
    ```
    
- **`dtype`:** Data type of the elements (e.g., `int64`, `float64`).
    
    ```python
    print(arr_2d.dtype)
    ```
    
- **`size`:** Total number of elements (rows × columns).
    
    ```python
    print(arr_2d.size)  # For a 3x3 array, output: 9
    ```
    

### 4. Indexing and Slicing

Indexing and slicing in 2D arrays let you access subsets of the data.

### a. Basic Indexing

Access an element using `array[row, column]`:

```python
element = arr_2d[1, 2]  # Access element at second row, third column
print("Element at row 1, col 2:", element)  # Expected: 6
```

### b. Slicing

Slicing works for rows and columns:

```python
# Extract a subarray containing the first two rows
sub_arr = arr_2d[0:2, :]
print("First two rows:\\n", sub_arr)

# Extract a subarray with the last two columns from all rows
sub_arr2 = arr_2d[:, 1:3]
print("Last two columns:\\n", sub_arr2)
```

You can combine slicing to select specific rows and columns.

### c. Advanced Indexing

- **Boolean Indexing:** Filter rows or columns based on a condition.
    
    ```python
    # For example, select rows where the first element is greater than 3:
    mask = arr_2d[:, 0] > 3
    filtered_rows = arr_2d[mask, :]
    print("Rows where first column > 3:\\n", filtered_rows)
    ```
    

### 5. Arithmetic and Vectorized Operations

One of NumPy's strengths is performing arithmetic operations element-wise.

```python
# Create two 2D arrays of the same shape
arr_a = np.array([[1, 2], [3, 4]])
arr_b = np.array([[10, 20], [30, 40]])

# Element-wise addition, multiplication, etc.
add_result = arr_a + arr_b          # Addition
mult_result = arr_a * 3             # Scalar multiplication
product_ab = arr_a * arr_b          # Element-wise multiplication

print("Addition:\\n", add_result)
print("Scalar Multiplication:\\n", mult_result)
print("Element-wise Multiplication:\\n", product_ab)
```

For matrix multiplication (dot product), you can use the `@` operator or `np.dot`:

```python
dot_product = arr_a @ arr_b
print("Matrix Multiplication:\\n", dot_product)
```

### 6. Broadcasting

Broadcasting allows operations between arrays of different shapes when certain rules are met. For example, adding a 1D array to a 2D array:

```python
# 1D array (vector)
vec = np.array([1, 2])
# 2D array (matrix)
matrix = np.array([[10, 20],
                   [30, 40],
                   [50, 60]])
result = matrix + vec  # vec is broadcasted to each row of matrix
print("Broadcasting Addition:\\n", result)
```

This automatic "stretching" of arrays improves code efficiency and readability.

### 7. Array Manipulation and Reshaping

NumPy lets you reshape, flatten, and transpose 2D arrays easily.

- **Reshape:** Change the shape without changing data.
    
    ```python
    arr = np.arange(12)       # 1D array of 12 elements
    reshaped = arr.reshape(3, 4)  # Now a 3x4 matrix
    print("Reshaped Array:\\n", reshaped)
    ```
    
- **Transpose:** Swap rows and columns.
    
    ```python
    transposed = reshaped.T
    print("Transposed Array:\\n", transposed)
    ```
    
- **Flatten:** Convert to a 1D array.
    
    ```python
    flattened = reshaped.flatten()
    print("Flattened Array:", flattened)
    ```
    

### 8. Iterating Over 2D Arrays

While vectorized operations are preferred, sometimes you need to iterate:

- **Row-wise Iteration:** Each row of a 2D array is a 1D array.
    
    ```python
    for row in reshaped:
        print("Row:", row)
    ```
    
- **Element-wise Iteration:** Use `.flat` to iterate over all elements.
    
    ```python
    for value in reshaped.flat:
        print(value, end=" ")
    ```
    

### 9. Hands-On Exercises

1. **Creating and Manipulating a 2D Array:**
    - Create a 2D array of shape (4, 5) using `np.arange()` and reshape.
    - Extract the third row and the first two columns.
    - Replace a specific element (say, at row 2, column 3) with a new value.
    
    ```python
    arr = np.arange(20).reshape(4, 5)
    print("Original Array:\\n", arr)
    
    # Extract third row (index 2)
    third_row = arr[2, :]
    print("Third Row:", third_row)
    
    # Extract first two columns
    first_two_cols = arr[:, 0:2]
    print("First Two Columns:\\n", first_two_cols)
    
    # Modify element at row 2, column 3
    arr[2, 3] = 999
    print("Modified Array:\\n", arr)
    ```
    
2. **Matrix Multiplication and Broadcasting:**
    - Create a 2D array and a 1D vector.
    - Add the vector to each row of the array using broadcasting.
    - Multiply two 2D arrays using both element-wise multiplication and matrix multiplication.
    
    ```python
    matrix = np.array([[1, 2, 3],
                       [4, 5, 6],
                       [7, 8, 9]])
    vector = np.array([10, 20, 30])
    # Broadcasting addition
    result_add = matrix + vector
    print("Matrix + Vector:\\n", result_add)
    
    # Element-wise multiplication
    result_elem = matrix * 2
    print("Matrix Elements * 2:\\n", result_elem)
    
    # Matrix multiplication using @ operator
    result_dot = matrix @ matrix.T
    print("Matrix Multiplication (matrix @ matrix.T):\\n", result_dot)
    
    ```
    
3. **Statistical Aggregations:**
    - For a given 2D array, compute the sum and mean along axes.
    
    ```python
    arr2d = np.array([[1, 2, 3],
                      [4, 5, 6],
                      [7, 8, 9]])
    sum_by_row = np.sum(arr2d, axis=1)   # Sum each row
    sum_by_col = np.sum(arr2d, axis=0)   # Sum each column
    mean_by_row = np.mean(arr2d, axis=1)
    
    print("Sum by Row:", sum_by_row)
    print("Sum by Column:", sum_by_col)
    print("Mean by Row:", mean_by_row)
    ```
    

### 10. Summary

- **Definition:** Two-dimensional NumPy arrays represent data in a matrix (rows and columns) and are key for numerical computations.
- **Creation:** Use functions like `np.array()` with nested lists, `np.arange()` with `reshape()`, `np.zeros()`, `np.ones()`, and `np.eye()`.
- **Properties:** Attributes such as `ndim`, `shape`, `dtype`, and `size` give insights into the structure of the array.
- **Indexing & Slicing:** You can access individual elements with `arr[i, j]`, extract rows, columns, or subarrays using slicing, and filter using Boolean indexing.
- **Operations:** Perform fast element-wise arithmetic, vectorized operations, and matrix multiplication.
- **Broadcasting:** Enables operations between arrays of different, but compatible, shapes.
- **Reshaping:** Methods such as `reshape()`, `transpose()`, and `flatten()` allow you to manipulate the array shape.

---