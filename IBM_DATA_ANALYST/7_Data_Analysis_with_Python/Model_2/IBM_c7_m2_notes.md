# IBM_c7_m2

## Pre-processing data in Python

### 1. Why Pre-Processing Matters

Data that comes in “raw” often has problems: missing values, incorrect data types, duplicates, outliers, and inconsistent formats. Pre-processing ensures:

- **Accuracy:** Reducing errors and gaps prevents your analysis from drawing false conclusions.
- **Efficiency:** Better data structures lead to faster processing.
- **Reproducibility:** Clean data creates a consistent starting point for building models and dashboards.
- **Better Insights:** Data aligned to the analysis (e.g., dates in the proper format) uncovers trends you might otherwise miss.

Imagine trying to calculate monthly sales trends if your **Order_date** is in the wrong format or if some rows are duplicated—the conclusions drawn could be entirely off.

### 2. Common Pre-Processing Tasks

### a. Handling Missing Data

Missing values can occur for many reasons—errors in data collection or entry, hardware issues, etc. You have several options:

- **Remove Missing Values:** Use `dropna()` if too many entries are missing.
- **Fill Missing Values:** Use `fillna()` with a default value (like 0 or a mean/median).
- **Advanced Imputation:** Use statistical or machine learning methods to predict missing entries.

**Example:**

```python
import pandas as pd

# Load the SalesDataset
sales_df = pd.read_csv('SalesDataset.csv')

# Check for missing values in each column
print("Missing values before pre-processing:")
print(sales_df.isnull().sum())

# Fill missing values in 'Profit' with 0 (if that's appropriate for your analysis)
sales_df['Profit'] = sales_df['Profit'].fillna(0)

# Alternatively, drop rows where critical fields like Amount are missing
sales_df = sales_df.dropna(subset=['Amount'])

print("Missing values after pre-processing:")
print(sales_df.isnull().sum())
```

### b. Converting Data Types

Correct data types ensure that operations behave as expected. For example, dates stored as strings must be converted to `datetime` objects to enable time series analysis, and numbers saved as strings need conversion to numeric types.

**Example:**

```python
# Convert Order_date to datetime format.
sales_df['Order_date'] = pd.to_datetime(sales_df['Order_date'])

# Also convert the Year-Month column if needed.
sales_df['Year-Month'] = pd.to_datetime(sales_df['Year-Month'], format='%Y-%m')
```

### c. Handling Duplicates

Duplicate records can skew your analysis, especially when calculating aggregates like total sales or average profit.

**Example:**

```python
# Find duplicate rows (if any)
duplicates = sales_df[sales_df.duplicated()]
print("Duplicate rows found:")
print(duplicates)

# Remove duplicates if they are not needed:
sales_df = sales_df.drop_duplicates()
```

### d. Normalizing and Scaling

For analyses like clustering or regression, scaling numerical features can be crucial. Scaling transforms values to a consistent range (e.g., 0 to 1).

**Example:**

```python
from sklearn.preprocessing import MinMaxScaler

# Suppose we want to scale the 'Amount' and 'Profit' columns.
scaler = MinMaxScaler()

sales_df[['Amount_scaled', 'Profit_scaled']] = scaler.fit_transform(sales_df[['Amount', 'Profit']])
print(sales_df[['Amount', 'Amount_scaled', 'Profit', 'Profit_scaled']].head())
```

### e. Feature Engineering

Sometimes the raw columns aren’t enough. You might derive new columns (features) that capture relevant information. For instance, you might calculate a **Profit Margin** column:

```python
# Create a new column for profit margin
sales_df['Profit_Margin'] = sales_df['Profit'] / sales_df['Amount']
print(sales_df[['Order_Id', 'Amount', 'Profit', 'Profit_Margin']].head())
```

---

## Dealing with missing values in Python

### 1. Understanding Missing Values

Missing values in a dataset can occur for several reasons:

- **Data Collection Errors:** Data might not be recorded properly.
- **Systematic Issues:** Some sources may not provide all the information (e.g., a transaction might be missing a profit value).
- **Input Errors:** Human error during data entry can lead to missing data.

In our **SalesDataset**, columns like **Profit**, **CustomerName**, or even **Order_date** might have missing entries. Before diving into handling them, you first need to identify their presence.

### Detecting Missing Data

The common way to check for missing data is using the `isnull()` method combined with `sum()` to get a count per column.

```python
import pandas as pd

# Load the SalesDataset CSV file.
sales_df = pd.read_csv('SalesDataset.csv')

# Get the count of missing values per column.
missing_counts = sales_df.isnull().sum()
print("Missing values per column:")
print(missing_counts)
```

This simple report helps you decide which columns need attention and whether the missing values are few (possible candidates for imputation) or widespread (which might need a different strategy).

### 2. Techniques for Dealing with Missing Values

Once you've detected missing values, you have several strategies at your disposal:

### a. Dropping Missing Values

### When to Use:

- Missing values are few and randomly distributed.
- The rows/columns with missing data are not critical for the analysis.

**Example: Dropping Rows with Missing Values in the 'Amount' Column**

```python
# Drop any rows where 'Amount' is missing. This is a critical numerical field.
sales_df = sales_df.dropna(subset=['Amount'])
```

**Example: Dropping All Rows with Any Missing Values**

```python
# WARNING: This may remove too much data!
sales_df_clean = sales_df.dropna()
```

*Note:* Dropping data outright can sometimes lead to a loss of valuable information. Always check the proportion of missing values before using this method.

### b. Imputing Missing Values

Imputation involves filling in missing values with a substitute that makes sense for your dataset.

### 1. Using a Constant Value

If a missing value implies a default or a known substitute, you can fill it in.

**Example: Filling Missing Profit with 0**

```python
sales_df['Profit'] = sales_df['Profit'].fillna(0)
```

### 2. Using Statistical Metrics

For numerical columns, you might use the **mean**, **median**, or **mode**.

**Example: Impute the 'Profit' Column with its Median Value**

```python
profit_median = sales_df['Profit'].median()
sales_df['Profit'] = sales_df['Profit'].fillna(profit_median)
```

### 3. Forward Fill and Backward Fill

For time series data or ordered data, you might want to propagate the last valid observation forward or backward.

**Example: Assuming 'Order_date' is sorted, filling missing values with the previous value**

```python
# Forward fill: Fills each NaN with the previous value.
sales_df['CustomerName'] = sales_df['CustomerName'].fillna(method='ffill')

# Backward fill: Fills each NaN with the next valid value.
sales_df['CustomerName'] = sales_df['CustomerName'].fillna(method='bfill')
```

### 4. Advanced Imputation Techniques

For more sophisticated datasets, you might use machine learning methods for imputation. The **scikit-learn** library offers `SimpleImputer` and `KNNImputer`.

**Example: Using SimpleImputer**

```python
from sklearn.impute import SimpleImputer

# Create an imputer object with a strategy (e.g., mean) for numerical columns.
imputer = SimpleImputer(strategy='mean')

# Assume we're imputing for 'Profit' and 'Amount' columns.
sales_df[['Profit', 'Amount']] = imputer.fit_transform(sales_df[['Profit', 'Amount']])
```

These techniques allow you to select an imputation strategy that preserves the integrity of your analysis.

### 3. Practical Hands-On Exercise

Let's integrate the ideas into a practical example using our **SalesDataset**:

1. **Inspect missing values.**
2. **Decide on an approach (drop or fill).**
3. **Apply the method and verify the data.**

```python
import pandas as pd
from sklearn.impute import SimpleImputer

# Load the SalesDataset.
sales_df = pd.read_csv('SalesDataset.csv')

# Step 1: Inspect missing values.
print("Missing values per column before pre-processing:")
print(sales_df.isnull().sum())

# Step 2: Decide the approach for each column.
# - For 'Profit', fill missing values with median.
# - For 'Amount', drop rows if missing (as it's crucial).
sales_df = sales_df.dropna(subset=['Amount'])

profit_median = sales_df['Profit'].median()
sales_df['Profit'] = sales_df['Profit'].fillna(profit_median)

# Optionally, impute other numerical columns using SimpleImputer.
# For example, if 'Quantity' has missing values:
imputer = SimpleImputer(strategy='mean')
sales_df[['Quantity']] = imputer.fit_transform(sales_df[['Quantity']])

# Step 3: Verify the missing values have been handled.
print("\\nMissing values per column after pre-processing:")
print(sales_df.isnull().sum())
```

Running this code in your Jupyter Notebook or VS Code will allow you to see before-and-after differences in your dataset.

---

## Data formatting in Python

Formatting helps ensure that every piece of information adheres to standardized types, representations, and styles, which in turn enables accurate analysis, reliable visualizations, and cleaner reporting.

### 1. Why Data Formatting Matters

Before you perform any analysis or modeling, your dataset should be coherent. Data formatting accomplishes this by ensuring:

- **Consistent Data Types:** For instance, date columns must be in a datetime format and numeric columns should be correctly interpreted as numbers.
- **Readable Output:** Proper formatting of numbers (like adding thousand separators or limiting decimal places) improves the clarity of reports.
- **String Uniformity:** Trimming extra spaces and standardizing capitalization helps when filtering, merging, or comparing text data.
- **Facilitates Downstream Tasks:** Clean and well-formatted data minimizes errors later in your pipeline—from merging datasets to writing complex queries.

Imagine preparing a monthly sales report where the dates are in mixed formats, or profit values are strings rather than numbers—the insights may get lost, or worse, lead to erroneous conclusions.

### 2. Common Data Formatting Techniques

Let's get hands-on with techniques and examples:

### a. Converting Data Types

**Dates:** Convert a column like **Order_date** from a string to a datetime object, which allows you to perform time series analysis.

```python
import pandas as pd

# Load your SalesDataset.
sales_df = pd.read_csv('SalesDataset.csv')

# Convert Order_date into a datetime object.
sales_df['Order_date'] = pd.to_datetime(sales_df['Order_date'])
```

Likewise, if you have a column such as **Year-Month** in string format, converting it with the specific format enhances consistency:

```python
sales_df['Year-Month'] = pd.to_datetime(sales_df['Year-Month'], format='%Y-%m')
```

**Numerical Columns:** Sometimes numbers get loaded as strings. Use `pd.to_numeric()` to ensure they’re properly formatted:

```python
sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')
```

The argument `errors='coerce'` converts non-numeric values to NaN, enabling you to spot or impute them later.

### b. String Formatting and Cleaning

Standardizing text is vital for columns like **CustomerName**, **City**, or **Category**. Common tasks include:

- **Trimming Extra Whitespace:**
- **Standardizing Case:** Convert to title case, lowercase, or uppercase as needed.

**Example:**

```python
# Strip whitespace and standardize the CustomerName column.
sales_df['CustomerName'] = sales_df['CustomerName'].str.strip().str.title()

# For City and Category, similar techniques can be applied.
sales_df['City'] = sales_df['City'].str.strip().str.title()
sales_df['Category'] = sales_df['Category'].str.strip().str.capitalize()
```

This makes filtering or joining on these columns more reliable, avoiding mismatches due to small case or spacing differences.

### c. Formatting Numeric Values for Reporting

Sometimes, beyond converting types, you need numeric values displayed neatly—like currency formatting or rounding off decimals.

**Example: Format Amount as Currency**

```python
# Format the 'Amount' column to 2 decimal places with a dollar sign.
sales_df['Formatted_Amount'] = sales_df['Amount'].apply(lambda x: f"${x:,.2f}")
```

This use of formatted string literals (f-strings) is excellent for creating human-readable reports or dashboards.

### d. Handling Date Formatting for Output

After converting date strings to datetime objects, you might want to display them in a specific format when reporting.

**Example:**

```python
# Format Order_date to a specific format like 'Month Day, Year'.
sales_df['Formatted_Order_date'] = sales_df['Order_date'].dt.strftime('%B %d, %Y')
```

This is particularly useful when you’re generating summaries or visualizations where date readability makes a big difference.

### e. Combining and Rearranging Columns

Sometimes, you need to tidy your dataset by combining columns—for instance, merging **State** and **City** into one **Location** column for concise reports.

**Example:**

```python
sales_df['Location'] = sales_df['City'].str.title() + ", " + sales_df['State'].str.upper()
```

This kind of transformation unifies your information and often simplifies further analysis.

### 3. Practical Hands-On Exercise

Here's a mini-project that integrates these formatting steps for the SalesDataset:

```python
import pandas as pd

# Step 1: Load the data.
sales_df = pd.read_csv('SalesDataset.csv')

# Step 2: Convert data types.
sales_df['Order_date'] = pd.to_datetime(sales_df['Order_date'])
sales_df['Year-Month'] = pd.to_datetime(sales_df['Year-Month'], format='%Y-%m')
sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')

# Step 3: Clean string columns.
sales_df['CustomerName'] = sales_df['CustomerName'].str.strip().str.title()
sales_df['City'] = sales_df['City'].str.strip().str.title()
sales_df['Category'] = sales_df['Category'].str.strip().str.capitalize()

# Step 4: Format numeric columns for reporting.
sales_df['Formatted_Amount'] = sales_df['Amount'].apply(lambda x: f"${x:,.2f}")

# Step 5: Format dates for display.
sales_df['Formatted_Order_date'] = sales_df['Order_date'].dt.strftime('%B %d, %Y')

# Step 6: Combine columns for a dynamic field.
sales_df['Location'] = sales_df['City'] + ", " + sales_df['State']

# Preview the formatted data.
print(sales_df[['CustomerName', 'Formatted_Amount', 'Formatted_Order_date', 'Location']].head())
```

---

## Data normalization in Python

Data normalization is the process of transforming numerical data into a common scale—typically without distorting differences in the ranges of values. 

For eg, in **SalesDataset**, columns like **Amount**, **Profit**, and **Quantity** might differ significantly in their magnitudes. Normalizing them makes it easier to compare features and improve model performance.

### 1. Why Normalize?

- **Uniform Scale:**
    
    Many algorithms (e.g., k-nearest neighbors, gradient descent-based models) assume that features are on a similar scale. Without normalization, a feature with a larger range might dominate the influence on the model.
    
- **Faster Convergence:**
    
    For models that use gradient descent, normalization can greatly speed up the learning process by ensuring smoother and more uniform gradients.
    
- **Improved Comparability:**
    
    With features scaled to a common range, visualizations and distance metrics become more meaningful.
    

### 2. Common Methods of Normalization

### a. **Min-Max Scaling (Normalization)**

This technique rescales data to a fixed range, usually [0, 1]. For each value \( x \) in a feature, the transformation is:

```tsx

x(normalized) = (x - x(min) ) / ( x (max) - x (min) )
```

### b. **Standardization (Z-score Normalization)**

Standardization scales the data so that it has a mean of 0 and a standard deviation of 1. The formula is:

```tsx
z = ( x - mu ) / sigma
```

where mu is the mean and sigma is the standard deviation of the feature.

### c. **Other Techniques**

There are other more sophisticated techniques (e.g., Robust Scaling, Log Transformation) that are useful in different contexts, particularly when dealing with outliers.

### 3. Practical Examples with the SalesDataset

Let’s say we want to normalize the **Amount** and **Profit** columns in our SalesDataset. We’ll use both the Min-Max normalization and Standardization approaches using Python's **scikit-learn** library.

### a. Using Min-Max Scaling

```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Load the SalesDataset
sales_df = pd.read_csv('SalesDataset.csv')

# Ensure that the columns are numeric
sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')

# Instantiate the MinMaxScaler
min_max_scaler = MinMaxScaler()

# Normalize the 'Amount' and 'Profit' columns
sales_df[['Amount_normalized', 'Profit_normalized']] = min_max_scaler.fit_transform(
    sales_df[['Amount', 'Profit']]
)

# Display the first few rows to see the transformation
print("Min-Max Normalization:")
print(sales_df[['Amount', 'Amount_normalized', 'Profit', 'Profit_normalized']].head())
```

In this example, values in **Amount_normalized** and **Profit_normalized** now lie between 0 and 1.

### b. Using Standardization (Z-score Normalization)

```python
from sklearn.preprocessing import StandardScaler

# Instantiate the StandardScaler
standard_scaler = StandardScaler()

# Apply standardization to the 'Amount' and 'Profit' columns
sales_df[['Amount_standardized', 'Profit_standardized']] = standard_scaler.fit_transform(
    sales_df[['Amount', 'Profit']]
)

# Display results
print("Standardization (Z-score) Normalization:")
print(sales_df[['Amount', 'Amount_standardized', 'Profit', 'Profit_standardized']].head())
```

Here, the **Amount_standardized** and **Profit_standardized** columns show values transformed such that the mean is approximately 0 and the standard deviation is 1.

### 4. Manual Normalization with Pandas

Sometimes, you might also perform normalization without external libraries. For example, performing Min-Max scaling manually using pandas:

```python
# Manual Min-Max Normalization for the 'Amount' column
sales_df['Amount_manual_normalized'] = (
    sales_df['Amount'] - sales_df['Amount'].min()
) / (sales_df['Amount'].max() - sales_df['Amount'].min())

# Verify that values are scaled between 0 and 1.
print("Manual Min-Max Normalization:")
print(sales_df[['Amount', 'Amount_manual_normalized']].head())
```

### 5. When Not to Normalize

- **Categorical Features:**
    
    Normalization applies to numerical features. For columns like **Category** or **PaymentMode**, you will use other encoding methods (e.g., one-hot encoding or label encoding).
    
- **Already Scaled Data:**
    
    If your domain data is inherently scaled (or if you’re using models insensitive to feature scaling like tree-based algorithms), additional normalization might not be necessary.
    

---

## Binning in Python

Binning is a data pre-processing technique where continuous numerical values are grouped into discrete "bins" or intervals. This is particularly useful for:

- **Reducing noise:** By grouping similar values together, minor fluctuations in the data get smoothed out.
- **Simplifying models:** Many models or visualizations perform better with categorical or discretized data.
- **Identifying patterns:** Binning can reveal underlying distributions or thresholds in your data that might be hard to see otherwise.

In our **SalesDataset**, you might want to bin the **Amount** column into groups such as "Low", "Medium", and "High" sales, or bin **Profit** to understand segments of profitability.

### 1. Binning Using `pd.cut` (Equal Width Binning)

`pd.cut` divides the data into intervals (bins) of equal width. You can specify either the number of bins or the bin edges explicitly.

### Example: Binning the "Amount" Column

Suppose you want to create three bins for the **Amount** column:

```python
import pandas as pd

# For demonstration, let's create a sample DataFrame similar to our SalesDataset.
data = {
    'Order_Id': [1, 2, 3, 4, 5, 6],
    'Amount': [1500, 3000, 500, 7000, 4200, 1100],
    'Profit': [300, 500, 100, 800, 600, 200]
}
sales_df = pd.DataFrame(data)

# Define bin edges. Here we can use the min and max of the "Amount" column.
# For three bins, we'll define the edges accordingly.
bins = [sales_df['Amount'].min() - 1, 2500, 5000, sales_df['Amount'].max() + 1]

# Use pd.cut to bin the data and label the bins.
labels = ['Low', 'Medium', 'High']
sales_df['Amount_Bin'] = pd.cut(sales_df['Amount'], bins=bins, labels=labels)

print("Binned Amount Data:")
print(sales_df[['Order_Id', 'Amount', 'Amount_Bin']])
```

In this example, we defined custom bin edges and labeled them. The **Amount** values are then binned into "Low", "Medium", or "High" based on where they fall within the specified ranges.

### 2. Binning Using `pd.qcut` (Quantile-Based Binning)

`pd.qcut` creates bins based on quantiles, ensuring that each bin has (approximately) the same number of observations. This method is particularly useful when your data is skewed.

### Example: Quantile Binning the "Amount" Column

```python
# Use pd.qcut to create 3 bins of equal frequency.
sales_df['Amount_Quantile_Bin'] = pd.qcut(sales_df['Amount'], q=3, labels=['Q1', 'Q2', 'Q3'])

print("Quantile Binned Amount Data:")
print(sales_df[['Order_Id', 'Amount', 'Amount_Quantile_Bin']])
```

This code divides the **Amount** column into three quantiles. Each bin (labeled "Q1", "Q2", and "Q3") should contain roughly the same number of records.

### 3. Custom Binning Strategies

Sometimes, the bin edges need to reflect domain-specific thresholds rather than strict statistical quantiles or equal widths. For example, if you know that sales below $1,000 are unusually low, between $1,000 and $5,000 are average, and above $5,000 are high, you can define those thresholds:

```python
custom_bins = [0, 1000, 5000, sales_df['Amount'].max()]
custom_labels = ['Below Average', 'Average', 'Above Average']
sales_df['Custom_Amount_Bin'] = pd.cut(sales_df['Amount'], bins=custom_bins, labels=custom_labels)

print("Custom Binned Amount Data:")
print(sales_df[['Order_Id', 'Amount', 'Custom_Amount_Bin']])
```

### 4. Why Binning is Useful in Analysis

- **Enhanced Visualization:** Binned data is easier to visualize with bar plots or histograms. For example, you could easily display the frequency of orders within each bin.
- **Modeling Purposes:** Certain algorithms perform better with discrete features versus continuous ones. Binning can help in creating features for classification or decision trees.
- **Interpretability:** With bins, decision thresholds become clearer. Stakeholders may understand "High" vs. "Low" sales more intuitively than raw numbers.

---

## Turning categorial variables into quantitative variables in python

Transforming categorical variables into quantitative (numerical) ones is a crucial step, especially when feeding data into machine learning models. 

Many algorithms require numbers, not text, so converting categories like **Category**, **Sub-category**, or **PaymentMode** in the dataset like **SalesDataset** makes your data easier to work with and your models more effective.

### 1. Why Convert Categorical Variables?

- **Model Compatibility:** Algorithms like linear regression, logistic regression, and many others expect numerical input. Categorical features need conversion before they can be processed.
- **Better Feature Engineering:** Converting strings to numbers often unlocks more insightful patterns and allows you to experiment with interactions between features.
- **Reduce Dimensionality:** While one-hot encoding (creating dummy variables) can increase dimensionality, other techniques like label encoding or ordinal encoding offer efficient alternatives when natural ordering exists.

### 2. Techniques for Converting Categorical Variables

There are several popular approaches:

### a. Label Encoding

Label encoding assigns each unique category a unique integer value. This approach is straightforward but has its caveats. For example, numerical labels may imply an order (0 < 1 < 2, etc.), which may not be desirable if the variable is nominal (unordered).

**Example with SalesDataset:**

Suppose you want to convert the **PaymentMode** column (e.g., "Credit Card", "Debit Card", "Cash") into numerical labels.

```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder

# Load your SalesDataset.
sales_df = pd.read_csv('SalesDataset.csv')

# Create an instance of LabelEncoder.
label_encoder = LabelEncoder()

# Apply label encoding to the PaymentMode column.
sales_df['PaymentMode_Encoded'] = label_encoder.fit_transform(sales_df['PaymentMode'])

print("PaymentMode column after label encoding:")
print(sales_df[['PaymentMode', 'PaymentMode_Encoded']].head())
```

*Note:* Use label encoding when there is some inherent order or for non-modeling exploratory purposes. For many algorithms, especially tree-based models, label encoding may suffice, but caution is advised with linear models.

### b. One-Hot Encoding (Dummy Variables)

One-hot encoding creates a new binary (0/1) column for each unique category. This method avoids the potential misinterpretation of inherent order in label encoding and is generally preferred for nominal categorical variables.

**Example with SalesDataset:**

Here, we might want to convert **Category** (say, "Electronics", "Furniture", etc.) into dummy variables.

```python
# One-hot encode the 'Category' column using pandas get_dummies.
sales_df_onehot = pd.get_dummies(sales_df, columns=['Category'], prefix='Cat')

print("DataFrame after one-hot encoding on Category:")
print(sales_df_onehot.head())
```

This will create new columns such as `Cat_Electronics`, `Cat_Furniture`, etc., each having a value of 1 where the condition is met or 0 otherwise.

### c. Ordinal Encoding

If a categorical variable has a natural order (e.g., "Low", "Medium", "High"), you can map them manually to numerical values.

**Example:**

Suppose you decide to bin **Amount** into categories and then assign an ordinal scale. First, you bin the data (as shown in our binning concept), and then map those bins to numbers.

```python
# Let's assume you already have an 'Amount_Bin' column created from a previous binning exercise.
# For instance, if Amount_Bin has labels like "Low", "Medium", "High":
ordinal_mapping = {'Low': 1, 'Medium': 2, 'High': 3}

# Create an Ordinal encoded column based on Amount_Bin.
sales_df['Amount_Ordinal'] = sales_df['Amount_Bin'].map(ordinal_mapping)

print("DataFrame with ordinal encoding for Amount_Bin:")
print(sales_df[['Amount', 'Amount_Bin', 'Amount_Ordinal']].head())
```

Ordinal encoding is ideal when the categories carry intrinsic order—ensuring that your numerical conversion reflects reality.

### 3. Choosing the Right Method

- **Label Encoding:**
    
    Use for ordinal variables or tree-based models where the numeric order doesn't drastically affect performance. Beware of unintended ordinal relationships.
    
- **One-Hot Encoding:**
    
    Safer for nominal variables with no inherent order, at the cost of increasing the number of features (especially with many unique categories).
    
- **Ordinal Encoding:**
    
    Perfect when categories have a specific order that conveys real differences (e.g., quality ratings).
    

For example, if you have a column like **PaymentMode** without any natural order, one-hot encoding is typically more appropriate. However, if you have customer satisfaction ratings like ["Poor", "Average", "Good"], ordinal encoding reflects the natural progression in customer sentiment.

---