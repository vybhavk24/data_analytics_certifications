# IBM_c7_m4

## Model development

Let's dive deep into model development in Python—a process that takes you from raw, cleaned data to a working predictive model.

1. **Problem Definition and Objective Setting**
    
    Before you write any code, frame exactly what you’re trying to achieve. For example, with our **SalesDataset**, you might wish to predict the **Profit** based on features like **Amount**, **Quantity**, and perhaps even categorical elements such as **Category** or **PaymentMode**. Setting clear objectives helps choose the right type of model (regression, classification, etc.) and metrics (R², RMSE, accuracy, etc.).
    
2. **Data Pre-Processing and Feature Engineering**
    
    Once you’ve cleaned and formatted your data (handling missing values, data types, and categorical encoding as we discussed earlier), you need to decide which features to use and—if necessary—create new ones. Feature engineering can include:
    
    - Creating new features (e.g., **Profit Margin** as Profit divided by Amount).
    - Transforming categorical features using one-hot encoding or label encoding.
    - Scaling numerical features so that they’re on comparable scales.
    
    For instance, suppose you want to build a model that predicts `Profit` based on `Amount` and `Quantity`. From prior steps, you may have also encoded `Category` into dummy variables.
    
3. **Splitting Data into Training and Testing Sets**
    
    It’s essential to evaluate your model on unseen data to gauge its real-world performance. Typically, your dataset is split into a training set (to fit the model) and a testing set (to evaluate its performance). Sometimes a validation set is carved out to fine-tune hyperparameters.
    
4. **Model Selection and Training**
    
    Depending on the problem, you might choose a simple model (like Linear Regression for regression tasks or Logistic Regression for binary classification) or more complex ones (decision trees, random forests, gradient boosting machines, etc.).
    
    For example, to predict **Profit** using a regression model, you might start with a simple linear regression:
    
    ```python
    import pandas as pd
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LinearRegression
    from sklearn.metrics import r2_score, mean_squared_error
    import numpy as np
    
    # Load the SalesDataset (make sure it's already cleaned and pre-processed)
    sales_df = pd.read_csv('SalesDataset.csv')
    
    # For simplicity, let's predict Profit based on Amount and Quantity.
    # Ensure these columns are numeric.
    sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
    sales_df['Quantity'] = pd.to_numeric(sales_df['Quantity'], errors='coerce')
    sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')
    
    # Drop rows with missing values in these key fields
    sales_df = sales_df.dropna(subset=['Amount', 'Quantity', 'Profit'])
    
    # Define features (X) and target variable (y)
    X = sales_df[['Amount', 'Quantity']]
    y = sales_df['Profit']
    
    # Split data into training and testing sets (e.g., 80% train, 20% test)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    
    # Initialize and train the model
    model = LinearRegression()
    model.fit(X_train, y_train)
    
    # Make predictions on the test set
    y_pred = model.predict(X_test)
    
    # Evaluate the model's performance
    r2 = r2_score(y_test, y_pred)
    rmse = np.sqrt(mean_squared_error(y_test, y_pred))
    
    print(f"R² Score: {r2:.3f}")
    print(f"RMSE: {rmse:.3f}")
    ```
    
    In this sample:
    
    - We load and clean the SalesDataset.
    - We select **Amount** and **Quantity** as predictors to estimate **Profit**.
    - After splitting our data, we fit a linear regression model and evaluate it with R² (explaining the proportion of variance) and RMSE (root-mean-square error), which tells us the average prediction error.
5. **Model Evaluation and Validation**
    
    Metrics such as R², RMSE (for regression), or accuracy, precision, and recall (for classification) determine whether your model meets your performance goals. You may also deploy cross-validation techniques to get a more robust estimate of performance. For example, using scikit-learn’s `cross_val_score` can help validate the model across different subsets of your training data.
    
6. **Hyperparameter Tuning and Iteration**
    
    Once you have a baseline model, you can start tuning hyperparameters (e.g., using grid search or randomized search) to further improve performance. Often, this iterative process leads to feature selection adjustments or even trying different algorithms.
    
7. **Deployment and Monitoring (Beyond Model Building)**
    
    After developing a satisfactory model, you prepare it for production—this involves deploying the model in a way that integrates with your data pipeline and setting up continuous monitoring to track performance over time.
    

### Real-World Considerations

- **Simplicity vs. Complexity:**
    
    Start simple—a linear regression can be a great baseline. As you better understand your data, you might try more complex models such as decision trees, random forests, or neural networks.
    
- **Interpretability:**
    
    For decisions driven by business stakeholders, models that provide interpretable insights (like linear regression with coefficients that explain the relationship between features and the target) can be valuable.
    
- **Feature Importance:**
    
    Once your model is trained, check which features are driving predictions. This can give you deeper insights into your data and inform future projects or data collection efforts.
    
- **Pipeline Integration:**
    
    Consider wrapping your pre-processing and model training steps into a pipeline (e.g., using scikit-learn’s `Pipeline` or `ColumnTransformer`) to ensure reproducibility and to simplify deployment.
    

---

## Simple and multiple linear regression

Let's dive into linear regression and multiple linear regression—two foundational techniques in predictive modeling. 

Both methods model the relationship between independent (predictor) variables and a dependent (target) variable. 

However, the difference lies in the number of predictors they use.

### 1. Linear Regression (Simple Linear Regression)

**Concept:**

- **Definition:** Simple linear regression models the relationship between one independent variable (predictor) and one dependent variable.
- **Mathematical Form:**
    
    ```tsx
    # Simple Linear Regression:
    # y = β0 + β1 * x + ε
    ```
    
    Here, y is the dependent variable (for example, **Profit**), x is the independent variable (for example, **Amount**), beta_0 is the intercept, beta_1 is the slope, and epsilon is the error term.
    
- **Interpretation:**
    - The slope beta_1 represents the change in  y for a one-unit change in x.
    - The intercept beta_0 is the predicted value of y when x is zero.

**When to Use:**

Use simple linear regression when you believe there is a linear relationship between a single predictor and your target variable.

### 2. Multiple Linear Regression

**Concept:**

- **Definition:** Multiple linear regression extends the idea of simple linear regression to include two or more independent variables.
- **Mathematical Form:**
    
    ```tsx
    # Multiple Linear Regression:
    # y = β0 + β1 * x1 + β2 * x2 + ... + βn * xn + ε
    ```
    
    Here, y is the target variable (again, for instance, **Profit**), and x_1, x_2, dots, x_n represent multiple predictors (for example, **Amount** and **Quantity**).
    
- **Interpretation:**
    - Each coefficient beta_i represents the change in the dependent variable for one unit change in the corresponding predictor x_i, assuming all other predictors remain constant.
    - This method captures more complexity and can lead to more accurate predictions if the additional features contribute valuable information.

**When to Use:**

Opt for multiple linear regression when your target variable is influenced by several factors at once. For example, predicting **Profit** using both **Amount** (the sale value) and **Quantity** (the number of items sold) often provides a more nuanced prediction.

### 3. Implementation in Python (Using Scikit-Learn)

Below are practical examples using our **SalesDataset**. In these examples, we assume that the dataset has been pre-processed, and columns like **Amount**, **Profit**, and **Quantity** are numeric.

### a. Simple Linear Regression Example (Predicting Profit from Amount)

```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score, mean_squared_error
import matplotlib.pyplot as plt
import seaborn as sns

# Load the SalesDataset
sales_df = pd.read_csv('SalesDataset.csv')

# Ensure relevant columns are numeric
sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')

# Drop rows with missing values in key fields
sales_df = sales_df.dropna(subset=['Amount', 'Profit'])

# Define predictor (X) and target (y)
X = sales_df[['Amount']]
y = sales_df['Profit']

# Split into training and testing sets (80% train, 20% test)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialize and train the simple linear regression model
simple_model = LinearRegression()
simple_model.fit(X_train, y_train)

# Predict using the trained model
y_pred = simple_model.predict(X_test)

# Evaluate model performance
r2 = r2_score(y_test, y_pred)
rmse = np.sqrt(mean_squared_error(y_test, y_pred))

print("Simple Linear Regression:")
print("Intercept:", simple_model.intercept_)
print("Coefficient for Amount:", simple_model.coef_[0])
print(f"R² Score: {r2:.3f}")
print(f"RMSE: {rmse:.3f}")

# Optional: Visualize the relationship and regression line
plt.figure(figsize=(8, 5))
sns.scatterplot(x=X_test['Amount'], y=y_test, label='Actual')
sns.lineplot(x=X_test['Amount'], y=y_pred, color='red', label='Predicted')
plt.title("Simple Linear Regression: Profit vs. Amount")
plt.xlabel("Amount")
plt.ylabel("Profit")
plt.legend()
plt.show()
```

### b. Multiple Linear Regression Example (Predicting Profit from Amount and Quantity)

```python
# Ensure the dataset has the necessary columns
sales_df['Quantity'] = pd.to_numeric(sales_df['Quantity'], errors='coerce')
sales_df = sales_df.dropna(subset=['Amount', 'Profit', 'Quantity'])

# Define predictors (X) and target (y) for multiple regression
X_multi = sales_df[['Amount', 'Quantity']]
y_multi = sales_df['Profit']

# Split the data
X_train_multi, X_test_multi, y_train_multi, y_test_multi = train_test_split(X_multi, y_multi, test_size=0.2, random_state=42)

# Initialize and train the multiple linear regression model
multi_model = LinearRegression()
multi_model.fit(X_train_multi, y_train_multi)

# Make predictions
y_pred_multi = multi_model.predict(X_test_multi)

# Evaluate model performance
r2_multi = r2_score(y_test_multi, y_pred_multi)
rmse_multi = np.sqrt(mean_squared_error(y_test_multi, y_pred_multi))

print("\\nMultiple Linear Regression:")
print("Intercept:", multi_model.intercept_)
print("Coefficients (Amount, Quantity):", multi_model.coef_)
print(f"R² Score: {r2_multi:.3f}")
print(f"RMSE: {rmse_multi:.3f}")
```

### 4. Comparison and Considerations

- **Feature Influence:**
    - In simple linear regression, you assess how changes in one predictor affect the target.
    - In multiple regression, each coefficient represents the partial impact of that predictor when other variables are held constant.
- **Assumptions:**
    
    Both methods assume a linear relationship between predictors and the target. Additional checks should be made for assumptions like homoscedasticity (constant variance of residuals), independence of errors, and normal distribution of residuals.
    
- **Model Complexity:**
    
    While adding more predictors can improve model accuracy, it also increases complexity. Beware of multicollinearity (high correlation between independent variables), which can destabilize coefficient estimates.
    
- **Interpretability:**
    
    Simple models are easier to interpret, whereas multiple regression provides deeper insights but may require domain expertise to explain the influence of individual predictors correctly.
    

---

## Model evaluation using Visualization

### 1. Importance of Visualizing Model Evaluation

Visualizations serve several roles in model evaluation:

- **Assessing Accuracy:** Comparing actual versus predicted values.
- **Diagnosing Errors:** Examining the pattern of residuals (errors) to ensure they are randomly distributed.
- **Checking Assumptions:** For linear regression, plots help check that residuals are normally distributed and homoscedastic (constant variance).
- **Communicating Results:** Graphs often reveal issues or strengths that summary statistics alone might hide.

### 2. Key Visualizations

### A. Actual vs. Predicted Scatter Plot

**Purpose:**

See how closely your predictions align with the actual data. The ideal scenario is when the data points lie along a 45° line (i.e., where actual equals predicted).

**Visualization Code:**

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(8, 5))
sns.scatterplot(x=y_test, y=y_pred, color='blue', alpha=0.6)
plt.plot([min(y_test), max(y_test)], [min(y_test), max(y_test)], color='red', linestyle='--')
plt.title("Actual vs. Predicted Values")
plt.xlabel("Actual Values")
plt.ylabel("Predicted Values")
plt.show()
```

### B. Residuals Plot

**Purpose:**

Plotting residuals (errors) versus predicted values helps identify patterns. Ideally, the residuals should scatter randomly around zero—indicating that the model captures the true relationship with no systematic error.

**Formula:**

```python
# Residual Calculation:
# residual = y_true - y_pred
```

**Visualization Code:**

```python
# Calculate residuals
residuals = y_test - y_pred

plt.figure(figsize=(8, 5))
sns.scatterplot(x=y_pred, y=residuals, color='purple', alpha=0.6)
plt.axhline(0, color='red', linestyle='--')
plt.title("Residuals vs. Predicted Values")
plt.xlabel("Predicted Values")
plt.ylabel("Residuals")
plt.show()
```

### C. Histogram (and Density Plot) of Residuals

**Purpose:**

This visualization checks whether the residuals have a normal distribution. A normally distributed residual is one of the assumptions in linear regression.

**Visualization Code:**

```python
plt.figure(figsize=(8, 5))
sns.histplot(residuals, bins=30, kde=True, color='green')
plt.title("Distribution of Residuals")
plt.xlabel("Residuals")
plt.ylabel("Frequency")
plt.show()
```

### D. Q-Q Plot of Residuals

**Purpose:**

A Q-Q (quantile-quantile) plot assesses if the residuals follow a normal distribution by plotting their quantiles against the expected quantiles of a normal distribution. Data points lying on the 45° line indicate normality.

**Visualization Code:**

```python
import scipy.stats as stats

plt.figure(figsize=(8, 5))
stats.probplot(residuals, dist="norm", plot=plt)
plt.title("Q-Q Plot of Residuals")
plt.show()
```

### E. R² (Coefficient of Determination)

**Purpose:**

R² provides a numerical measure of how much variation in the dependent variable is captured by the model. Higher R² values (up to 1) indicate a better fit.

**Formula in Code:**

```python
# R² Formula:
# R² = 1 - (SS_res / SS_tot)
#
# Where:
# SS_res = sum((y_true - y_pred)^2)
# SS_tot = sum((y_true - mean(y_true))^2)
```

You typically calculate R² programmatically (e.g., using scikit-learn’s `r2_score`), but the formula above is key for understanding its derivation.

---

## Polynomial regressions and pipelines

### 1. Polynomial Regression Overview

Polynomial regression is an extension of linear regression that allows for modeling non-linear relationships between the independent variable(s) and the target variable by adding polynomial terms.

### Formula:

```python
# Simple (Linear) Regression Formula:
# y = β0 + β1 * x + ε

# Polynomial Regression Formula (Degree d):
# y = β0 + β1 * x + β2 * x^2 + ... + βd * x^d + ε
```

In the above, the model is still linear in the parameters (β's), even though it is non-linear in terms of the raw input x.

### 2. Using PolynomialFeatures in Scikit-Learn

The `PolynomialFeatures` transformer in scikit-learn helps you automatically generate these polynomial (and interaction) terms.

For example, setting `degree=2` on a single feature (x) will transform it into:

- 1 (bias term, if requested),
- x,
- x².

### 3. Why Use Pipelines?

Pipelines let you chain together the entire model workflow—from preprocessing (like generating polynomial features and scaling) to model fitting—with one unified interface. This provides several benefits:

- **Reproducibility:** All steps are executed in the same order every time.
- **Less Error-Prone:** You don’t need to worry about manually applying the same transformations to your training and testing data.
- **Integration with Grid Search:** Pipelines work seamlessly with cross-validation and hyperparameter tuning.

### 4. Building a Polynomial Regression Pipeline: A Practical Example

Below is an end-to-end example using our **SalesDataset**. In this example, we predict **Profit** using **Amount** as the single feature but allow the relationship to be non-linear via polynomial transformation.

### Code Example

```python
import numpy as np
import pandas as pd
from sklearn.preprocessing import PolynomialFeatures, StandardScaler
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import Pipeline
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score, mean_squared_error

# Load the SalesDataset (ensure file exists in your working directory)
sales_df = pd.read_csv('SalesDataset.csv')

# Convert relevant columns to numeric (using errors='coerce' to handle non-numeric entries)
sales_df['Amount'] = pd.to_numeric(sales_df['Amount'], errors='coerce')
sales_df['Profit'] = pd.to_numeric(sales_df['Profit'], errors='coerce')

# Drop rows with missing Amount or Profit
sales_df = sales_df.dropna(subset=['Amount', 'Profit'])

# Define feature (X) and target (y)
X = sales_df[['Amount']]
y = sales_df['Profit']

# Split data into training and testing sets (80% training, 20% testing)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create a pipeline that:
# 1. Generates polynomial features up to degree 2 (excluding the bias which is handled by LinearRegression),
# 2. Scales the features,
# 3. Fits a Linear Regression model.
pipeline = Pipeline([
    ('poly', PolynomialFeatures(degree=2, include_bias=False)),
    ('scaler', StandardScaler()),
    ('lin_reg', LinearRegression())
])

# Train the pipeline on the training data
pipeline.fit(X_train, y_train)

# Make predictions on the test set
y_pred = pipeline.predict(X_test)

# Evaluate the model performance
r2 = r2_score(y_test, y_pred)
rmse = np.sqrt(mean_squared_error(y_test, y_pred))

print(f"Polynomial Regression (degree 2) R²: {r2:.3f}")
print(f"Polynomial Regression (degree 2) RMSE: {rmse:.3f}")
```

### Explanation

1. **Data Preprocessing:**
    
    We load and clean the SalesDataset to ensure **Amount** and **Profit** are numeric and remove any missing values.
    
2. **Pipeline Creation:**
    - **PolynomialFeatures:** Transforms the feature **Amount** into polynomial terms (x, x²).
    - **StandardScaler:** Scales the features to have zero mean and unit variance, which is helpful for many models.
    - **LinearRegression:** Fits the linear model on the transformed features.
3. **Model Evaluation:**
    
    The R² score and RMSE (Root Mean Squared Error) are computed to assess how well the model fits the test data.
    

### 5. Extending the Pipeline

You can easily extend the pipeline to include additional features, or try different polynomial degrees, and even integrate other preprocessing steps. For example, if you had multiple predictors, you could modify the pipeline to:

- Generate polynomial features for all predictors.
- Use `ColumnTransformer` to apply polynomial transformation only to numerical columns.
- Integrate cross-validation and grid search to optimize the polynomial degree or other hyperparameters.

This approach using polynomial regression and pipelines encapsulates the entire workflow from feature engineering to model training and evaluation—ensuring a robust, reproducible, and efficient modeling process.

If you need further details on extending pipelines or tuning hyperparameters in polynomial regression, let me know!

---

## Measures for in-sample evaluation

These metrics help you assess how well your model fits the training data (i.e. in-sample).

### 1. Common In-Sample Evaluation Metrics

### A. Residuals

- **Definition:** The difference between the observed values and the model’s predictions.
- **Formula:**
    
    ```python
    # residual = y_true - y_pred
    ```
    

### B. Residual Sum of Squares (RSS)

- **Definition:** The sum of the squared differences between the actual and predicted values.
- **Formula:**
    
    ```python
    # RSS = sum((y_true - y_pred)^2)
    ```
    

### C. Total Sum of Squares (TSS)

- **Definition:** The total variation in the observed data, computed as the sum of squared differences from the mean of the target variable.
- **Formula:**
    
    ```python
    # TSS = sum((y_true - mean(y_true))^2)
    ```
    

### D. Coefficient of Determination (R²)

- **Definition:** Indicates the proportion of the variance in the dependent variable that is predictable from the independent variable(s).
- **Formula:**
    
    ```python
    # R² = 1 - (RSS / TSS)
    ```
    

### E. Adjusted R²

- **Definition:** Adjusts R² to account for the number of predictors relative to the number of observations. This prevents overestimating the goodness-of-fit when many predictors are used.
- **Formula:**
    
    ```python
    # Adjusted R² = 1 - ((1 - R²) * (n - 1) / (n - p - 1))
    # where n = number of observations and p = number of predictors
    ```
    

### F. Mean Squared Error (MSE)

- **Definition:** The average of the squared residuals.
- **Formula:**
    
    ```python
    # MSE = sum((y_true - y_pred)^2) / n
    # where n = number of observations
    ```
    

### G. Root Mean Squared Error (RMSE)

- **Definition:** The square root of the MSE, giving a measure of error in the same units as the target variable.
- **Formula:**
    
    ```python
    # RMSE = sqrt(MSE)
    ```
    

### H. Mean Absolute Error (MAE)

- **Definition:** The average of the absolute differences between the actual and predicted values.
- **Formula:**
    
    ```python
    # MAE = sum(|y_true - y_pred|) / n
    ```
    

### I. Mean Absolute Percentage Error (MAPE)

- **Definition:** The average percentage difference between the predicted and actual values, expressed as a percentage.
- **Formula:**
    
    ```python
    # MAPE = 100 * (1/n) * sum(|(y_true - y_pred) / y_true|)
    ```
    

### 2. Practical Example in Python

Here’s an example that shows how you might calculate these metrics for in-sample evaluation using scikit-learn and numpy. (Assume that `y_train` are the actual target values for the training set and `y_pred_train` are the predictions generated by your model on the training set.)

```python
import numpy as np
from sklearn.metrics import r2_score, mean_squared_error, mean_absolute_error

# Example arrays for illustration (replace these with your actual training data and predictions)
# y_train = array of actual training target values
# y_pred_train = array of predicted values from the in-sample model
# For example:
y_train = np.array([100, 200, 300, 400, 500])
y_pred_train = np.array([110, 190, 310, 410, 480])
n = len(y_train)  # number of observations

# 1. Calculate Residuals
residuals = y_train - y_pred_train
#   residual = y_true - y_pred

# 2. Residual Sum of Squares (RSS)
RSS = np.sum((y_train - y_pred_train) ** 2)
#   RSS = sum((y_true - y_pred)^2)

# 3. Total Sum of Squares (TSS)
TSS = np.sum((y_train - np.mean(y_train)) ** 2)
#   TSS = sum((y_true - mean(y_true))^2)

# 4. R-squared (R²)
R2 = 1 - (RSS / TSS)
#   R² = 1 - (RSS / TSS)
print("R²:", R2)

# 5. Adjusted R-squared (For example, assume p predictors; here p=1 for simple regression)
p = 1
Adjusted_R2 = 1 - ((1 - R2) * (n - 1) / (n - p - 1))
#   Adjusted R² = 1 - ((1-R²)*(n-1))/(n-p-1)
print("Adjusted R²:", Adjusted_R2)

# 6. Mean Squared Error (MSE)
MSE = mean_squared_error(y_train, y_pred_train)
#   MSE = sum((y_true - y_pred)^2) / n
print("MSE:", MSE)

# 7. Root Mean Squared Error (RMSE)
RMSE = np.sqrt(MSE)
#   RMSE = sqrt(MSE)
print("RMSE:", RMSE)

# 8. Mean Absolute Error (MAE)
MAE = mean_absolute_error(y_train, y_pred_train)
#   MAE = sum(|y_true - y_pred|) / n
print("MAE:", MAE)

# 9. Mean Absolute Percentage Error (MAPE)
MAPE = 100 * np.mean(np.abs((y_train - y_pred_train) / y_train))
#   MAPE = 100 * (1/n)*sum(|(y_true - y_pred)/y_true|)
print("MAPE:", MAPE, "%")
```

---

## Prediction and decision making

In practice, prediction and decision making go hand in hand—once you build a model that can generate accurate predictions, you need a framework to turn those predictions into actionable decisions.

### 1. Overview

**Prediction** is the process of using a model to forecast future outcomes or estimate unknown values. These predictions (point estimates or even probability distributions) serve as the inputs for **decision making**, which is the process of choosing actions based on those predictions, expected outcomes, costs, risks, and benefits.

In decision making, you often face uncertainty. The typical goal is to maximize expected value or utility, balancing the potential gains against the likelihood and cost of adverse outcomes.

### 2. Generating Predictions

After you’ve developed and validated your model (for instance, using linear, polynomial, or logistic regression), you generate predictions on new (unseen) data. For a regression model that predicts profit, your model outputs a point prediction for each instance, such as:

```python
# Example:
# predicted_profit = model.predict(new_data)
```

If you need to incorporate uncertainty, you might also generate prediction intervals that reflect the variability of your estimates.

### 3. Turning Predictions into Decisions

### A. Setting Decision Rules

In many applications, you establish a rule—often a threshold—that tells you which action to take based on the prediction. For example, you might decide to invest in marketing only if the predicted profit exceeds a certain amount.

```python
# Decision Rule Example:
# If predicted profit > threshold, then "Invest", else "Do not invest"

threshold_profit = 500  # example threshold

# 'y_pred' is a NumPy array or list of predicted profit values.
decisions = ["Invest" if pred > threshold_profit else "Do not invest" for pred in y_pred]
```

This simple rule converts continuous predictions into discrete, actionable decisions.

### B. Expected Utility Framework

In a more formal decision-making environment, you can calculate the expected utility for each decision alternative. The goal is to select the decision that maximizes your expected benefit while considering risk.

```python
# Expected Utility Formula:
# EU = Σ(probability_i * utility_i)
```

For example, if you have several possible actions (e.g., "Invest", "Do not invest", "Wait") with associated probabilities and utilities, you can compute the EU for each:

```python
# Suppose:
# probabilities = [p1, p2, ...] for different outcomes,
# utilities = [u1, u2, ...] representing the benefits or costs.
# Then, for each decision alternative:

def expected_utility(probabilities, utilities):
    return sum(p * u for p, u in zip(probabilities, utilities))

# Example for a decision alternative:
EU_invest = expected_utility([0.6, 0.4], [1000, -200])
EU_not_invest = expected_utility([1.0], [0])  # no gain, no loss

print("Expected Utility of Investing:", EU_invest)
print("Expected Utility of Not Investing:", EU_not_invest)
```

By comparing these expected utilities, you can choose the alternative with the highest value.

### C. Risk and Uncertainty Analysis

Decisions under uncertainty often include a risk analysis part. For example, you can generate prediction intervals:

```python
# Prediction Interval Concept:
# Lower_Bound = predicted_value - constant * standard_error
# Upper_Bound = predicted_value + constant * standard_error
```

Using these intervals, you can decide not only on the mean prediction but also consider the range of possible outcomes. In a pipeline, you might integrate bootstrapping or Bayesian methods to quantify uncertainty.

### 4. Incorporating Predictions into Business Decisions

Let’s say your SalesDataset model predicts profit based on features (such as **Amount**, **Quantity**, etc.). Here’s how you might proceed:

1. **Generate Predictions:**
    
    Use your model to predict profit.
    
    ```python
    y_pred = model.predict(X_new)  # X_new holds your new data
    ```
    
2. **Define a Decision Rule:**
    
    For instance, implement additional marketing only if the predicted profit is high enough.
    
    ```python
    threshold_profit = 500
    decisions = ["Market Aggressively" if profit > threshold_profit else "No Change" for profit in y_pred]
    ```
    
3. **Analyze Risk:**
    
    Calculate prediction intervals or simulate various scenarios. For example, you might use a Monte Carlo simulation to see how often the profit exceeds your threshold under uncertainty.
    
4. **Implement & Monitor:**
    
    Turn decisions into actions and set up a feedback loop (e.g., measure actual profit versus predicted profit) so that you can refine your thresholds and update your models.
    

### 5. Visualizing Predictions and Decisions

Visualizations can clarify how predictions inform decisions. Some common visualization strategies include:

### A. Decision Boundaries on Scatter Plots

If you’re working with one feature (or a feature pair for higher dimensions), you can plot the predictions and overlay the decision threshold.

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(8, 5))
sns.scatterplot(x=X_new['Amount'], y=y_pred, label="Predicted Profit")
plt.axhline(threshold_profit, color='red', linestyle='--', label="Decision Threshold")
plt.title("Predicted Profit vs. Amount with Decision Threshold")
plt.xlabel("Amount")
plt.ylabel("Predicted Profit")
plt.legend()
plt.show()
```

### B. Uncertainty Visualization

Plot prediction intervals to display the degree of uncertainty in your predictions.

```python
# Example: Assume lower and upper bounds are computed for each prediction.
# lower_bounds and upper_bounds are arrays of the same length as y_pred.

plt.figure(figsize=(8, 5))
plt.plot(y_pred, label="Predicted Profit", color='blue')
plt.fill_between(range(len(y_pred)), lower_bounds, upper_bounds, color='lightblue', alpha=0.5, label="Prediction Interval")
plt.axhline(threshold_profit, color='red', linestyle='--', label="Decision Threshold")
plt.title("Predictions with Uncertainty")
plt.xlabel("Observation Index")
plt.ylabel("Profit")
plt.legend()
plt.show()
```

---