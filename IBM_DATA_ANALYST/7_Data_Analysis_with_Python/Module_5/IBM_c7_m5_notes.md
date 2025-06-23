# IBM_c7_m5

## Model refinement and evaluation

Model evaluation and refinement is the phase of the machine learning pipeline where insights, accountability, and performance intersect. It answers two critical questions:

1. *How well is my model performing—objectively and statistically?*
2. *How can I improve it to perform better or generalize more reliably?*

### 1. **Model Evaluation: What It Means and Why It Matters**

Model evaluation refers to quantitatively and qualitatively assessing a model’s performance on data, primarily focusing on:

- **In-sample performance:** Accuracy on training data (can indicate underfitting).
- **Out-of-sample performance:** Accuracy on test/validation data (determines generalizability).
- **Domain alignment:** Does the model make business sense? Are outputs interpretable?

Models should not just fit—they should make meaningful, reliable predictions across real-world conditions.

### 📊 2. **Key Evaluation Metrics (for Regression)**

Let's focus on regression models as in your SalesDataset workflow.

### **A. Residual-Based Metrics**

These quantify the “errors” between predictions and ground truth:

```python
# Residual = y_true - y_pred
# MSE = mean((y_true - y_pred)^2)
# RMSE = sqrt(MSE)
# MAE = mean(abs(y_true - y_pred))
# MAPE = 100 * mean(abs((y_true - y_pred) / y_true))
```

### **B. Variance-Based Metrics**

These measure how much of the target’s variance the model explains:

```python
# R² = 1 - (sum((y_true - y_pred)^2) / sum((y_true - mean(y_true))^2))
# Adjusted R² = 1 - ((1 - R²) * (n - 1) / (n - p - 1))
# where n = number of observations, p = number of predictors
```

### 📈 3. **Visual Evaluation Techniques**

Visuals often reveal what metrics conceal:

### **A. Actual vs. Predicted Scatter Plot**

Detects bias and systemic deviation.

```python
sns.scatterplot(x=y_test, y=y_pred)
plt.plot([min(y_test), max(y_test)], [min(y_test), max(y_test)], 'r--')  # 45° line
```

### **B. Residuals vs. Predicted Plot**

Ideal pattern: residuals scattered randomly around 0.

```python
residuals = y_test - y_pred
sns.scatterplot(x=y_pred, y=residuals)
plt.axhline(0, color='red', linestyle='--')
```

### **C. Histogram or KDE of Residuals**

Check for normality; large skews may violate model assumptions.

```python
sns.histplot(residuals, kde=True)
```

### **D. Q-Q Plot**

Confirms whether residuals follow a normal distribution.

```python
import scipy.stats as stats
stats.probplot(residuals, dist="norm", plot=plt)
```

### 🔧 4. **Refining the Model: What to Do When It’s Not Good Enough**

Once you’ve evaluated the model, refinement is all about **diagnosing and improving**.

### **A. Check for Underfitting or Overfitting**

- Underfitting: Bad on both training and testing sets.
- Overfitting: Great on training but poor on testing.

Use cross-validation:

```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(model, X, y, cv=5, scoring='r2')
print("Cross-validated R² scores:", scores)
```

### **B. Feature Engineering**

Ask: Are your features truly predictive?

- Add interaction terms or nonlinear terms (e.g., with `PolynomialFeatures`)
- Bin continuous features (e.g., Amount → "Low", "Medium", "High")
- Remove irrelevant or noisy predictors

### **C. Transform the Target or Predictors**

If residual plots suggest nonlinearity or heteroscedasticity:

```python
# Log-transform the target
y_transformed = np.log1p(y)

# Or apply log to skewed predictors
X['Amount'] = np.log1p(X['Amount'])
```

### **D. Try Other Models**

Don’t stick to one model—each has different inductive biases.

- Linear → Ridge/Lasso for regularization
- Linear → Polynomial for curve fitting
- Tree-based (Random Forest, XGBoost) if relationships are complex

### **E. Hyperparameter Tuning**

Use grid search or random search to find better settings:

```python
from sklearn.model_selection import GridSearchCV
param_grid = {'alpha': [0.1, 1, 10]}
grid = GridSearchCV(Ridge(), param_grid, scoring='neg_mean_squared_error')
grid.fit(X_train, y_train)
print("Best Params:", grid.best_params_)
```

### 🔁 5. **Iterative Model Development Framework**

Here’s how to cycle through improvement loops effectively:

1. **Build and train baseline model**
2. **Evaluate with metrics + residual plots**
3. **Diagnose specific problems:**
    - Bias? Variance? Outliers? Misleading features?
4. **Try refinements (features, transforms, models)**
5. **Re-evaluate with same tools**
6. **Document findings, retrain, redeploy**

This cyclical workflow ensures rigor and results that hold up to scrutiny.

### 🧭 6. **When Is a Model "Good Enough"?**

That depends on:

- Business goals (Is 10% error acceptable? Is interpretability more important?)
- Risk appetite (Can a wrong prediction cost us a lot?)
- Benchmarking against previous or simpler models
- Diminishing returns (Is improvement worth the complexity?)

Always align your evaluation with **practical usefulness**, not just theoretical soundness.

---

## Underfitting, overfitting and model selection

### 📉 1. Underfitting

**Definition:**

Underfitting happens when your model is too simplistic to capture the underlying patterns in the training data. It performs poorly on both training and testing sets.

**Symptoms:**

- Low training accuracy
- High bias
- Missed patterns

**Code Insight:**

```python
# Underfitting Example: fitting a straight line to curved data
# y = β0 + β1 * x + ε
```

**Solutions:**

- Add features or interaction terms
- Increase model complexity (e.g., higher-degree polynomial)
- Use a more flexible algorithm

### 📈 2. Overfitting

**Definition:**

Overfitting occurs when your model learns the noise and peculiarities in the training data, rather than the general pattern. It performs well on training data but poorly on unseen data.

**Symptoms:**

- Very high training accuracy
- Low test/validation accuracy
- High variance

**Code Insight:**

```python
# Overfitting Example: high-degree polynomial capturing noise
# y = β0 + β1 * x + β2 * x^2 + ... + βn * x^n + ε
```

**Solutions:**

- Reduce model complexity
- Add regularization (e.g., Ridge, Lasso)
- Use more data or apply data augmentation
- Use cross-validation to generalize better

### ⚖️ 3. The Bias-Variance Tradeoff

This tradeoff lies at the heart of overfitting and underfitting.

```python
# Total Error = Bias² + Variance + Irreducible Error
```

- **High bias → underfitting**
- **High variance → overfitting**
- The goal is to find the sweet spot that minimizes total error.

### 🧠 4. Model Selection

This is the process of identifying the model and hyperparameters that best balance accuracy, interpretability, and generalization.

**Tools & Techniques:**

- **Train/test split:** Basic starting point
- **Cross-validation (CV):** More robust estimate of model generalizability
    
    ```python
    from sklearn.model_selection import cross_val_score
    scores = cross_val_score(model, X, y, cv=5, scoring='r2')
    ```
    
- **Grid Search or Random Search:** To find the best hyperparameters
    
    ```python
    from sklearn.model_selection import GridSearchCV
    grid = GridSearchCV(model, param_grid, scoring='neg_mean_squared_error', cv=5)
    grid.fit(X_train, y_train)
    ```
    

**What You're Tuning:**

- Type of model (linear, tree-based, etc.)
- Degree of polynomial (for polynomial regression)
- Regularization strength (alpha in Ridge, Lasso)
- Tree depth, number of estimators, and other hyperparameters

---

## Ridge regression

Ridge regression is a powerful technique that enhances the performance of linear regression models by addressing one of their biggest weaknesses: sensitivity to multicollinearity and overfitting. 

If you're tackling a predictive task with many features, especially those that are correlated, Ridge regression can stabilize your estimates and improve generalization.

### 🧠 1. What Is Ridge Regression?

Ridge regression is a form of **regularized linear regression** that adds a penalty to the loss function to **shrink model coefficients**. This helps to:

- Prevent overfitting by discouraging large weights.
- Handle multicollinearity by adding bias to reduce variance.

Also known as **L2 regularization**, Ridge regression modifies the cost function used in ordinary least squares (OLS).

### 📐 2. Mathematical Foundation

Standard linear regression minimizes only the residual sum of squares:

```python
# Linear Regression Objective:
# J(β) = sum((yᵢ - y_predᵢ)²)
```

Ridge regression adds a penalty term proportional to the sum of squared coefficients:

```python
# Ridge Regression Objective:
# J(β) = sum((yᵢ - y_predᵢ)²) + λ * sum(βⱼ²)
```

Where:

- yᵢ are the true values,
- y_predᵢ are the predicted values,
- βⱼ are the model coefficients (excluding the intercept),
- λ (alpha in scikit-learn) is the **regularization strength** (≥ 0),
- The higher the λ, the more you shrink the coefficients.

### 🔁 3. When Should You Use Ridge Regression?

- You suspect **multicollinearity** among predictors.
- Your dataset has **more features than samples** (high dimensionality).
- You want to **reduce model complexity** while keeping all predictors.
- You seek a balance between **bias and variance**.

### ⚙️ 4. Implementation in Python (with Scikit-Learn)

Let’s walk through a Ridge regression example based on a sales prediction context.

```python
import pandas as pd
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.preprocessing import StandardScaler

# Load your dataset
sales_df = pd.read_csv('SalesDataset.csv')

# Example features and target
X = sales_df[['Amount', 'Quantity']]
y = sales_df['Profit']

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Scale features (very important for Ridge regression)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train Ridge regression model
ridge = Ridge(alpha=1.0)
ridge.fit(X_train_scaled, y_train)

# Predict and evaluate
y_pred = ridge.predict(X_test_scaled)
rmse = mean_squared_error(y_test, y_pred, squared=False)
r2 = r2_score(y_test, y_pred)

print("Ridge Coefficients:", ridge.coef_)
print(f"RMSE: {rmse:.3f}")
print(f"R²: {r2:.3f}")
```

### 🔍 5. Understanding the Regularization Parameter (`alpha`)

- `alpha = 0`: Equivalent to ordinary least squares.
- `alpha → ∞`: Coefficients shrink toward 0, model becomes simpler.
- **Hyperparameter tuning** is essential to find the best alpha.

```python
from sklearn.linear_model import RidgeCV

alphas = [0.01, 0.1, 1, 10, 100]
ridge_cv = RidgeCV(alphas=alphas, cv=5)
ridge_cv.fit(X_train_scaled, y_train)

print("Best Alpha:", ridge_cv.alpha_)
```

### 🧠 6. Key Characteristics of Ridge Regression

| Feature | Ridge Regression |
| --- | --- |
| Regularization Type | L2 penalty (squares of coefficients) |
| Effect on Coefficients | Shrinks them toward zero, but doesn't zero them |
| Handles Multicollinearity | Yes |
| Variable Selection | No (keeps all features) |
| Ideal For | Preventing overfitting, improving generalization |

### 📚 7. Ridge vs Lasso vs ElasticNet (at a glance)

| Feature | Ridge | Lasso | ElasticNet |
| --- | --- | --- | --- |
| Penalty | λ \sum βⱼ² |  λ \sum | βⱼ |
| Shrinks Coefficients | Yes | Yes | Yes |
| Can Set Coefficients to 0 | No | Yes (feature selection) | Yes |
| Use Case | Multicollinearity, all features useful | Sparse features | Hybrid settings |

### 🔄 8. Common Pitfalls and Tips

- **Always standardize your features** before applying Ridge regression—especially if the predictors are on different scales.
- Don't just pick a default `alpha`. Use cross-validation to tune it.
- Ridge doesn't eliminate features. If interpretability or sparsity matters, Lasso or ElasticNet might be better.
- Coefficients are biased (due to penalty) but variance is reduced—a key point in reducing overfitting.

---

## Grid Search

Grid search is a powerful hyperparameter tuning technique used in machine learning to systematically find the optimal combination of model parameters that yield the best performance.

### 🔧 1. What Is Grid Search?

In any algorithm, **hyperparameters** are settings that govern the model's structure or learning process (e.g., the regularization strength `alpha` in Ridge regression, or `max_depth` in decision trees). These are not learned from the data—they must be set before training.

**Grid search** exhaustively evaluates all combinations from a specified grid of hyperparameter values. It is often used alongside **cross-validation** to assess each setting’s performance.

### 🔍 2. How Grid Search Works

1. **Define a parameter grid** (combinations of hyperparameter values).
2. **Train the model** for each combination using cross-validation.
3. **Evaluate** each model using a scoring metric (e.g., RMSE, R², accuracy).
4. **Select** the combination with the best score.

### 🧪 3. Code Example: Ridge Regression + Grid Search

```python
from sklearn.linear_model import Ridge
from sklearn.model_selection import GridSearchCV
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline
import pandas as pd

# Load the dataset
sales_df = pd.read_csv('SalesDataset.csv')

# Preprocess features and target
X = sales_df[['Amount', 'Quantity']]
y = sales_df['Profit']

# Create a pipeline with scaling and Ridge regression
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('ridge', Ridge())
])

# Define the grid of alpha values to search
param_grid = {
    'ridge__alpha': [0.01, 0.1, 1.0, 10.0, 100.0]
}

# Perform GridSearch with 5-fold cross-validation
grid_search = GridSearchCV(pipeline, param_grid, cv=5, scoring='neg_mean_squared_error')
grid_search.fit(X, y)

# Output best parameters and performance
print("Best Alpha:", grid_search.best_params_)
print("Best CV Score (MSE):", -grid_search.best_score_)
```

### ⚙️ 4. GridSearchCV Key Parameters

```python
# GridSearchCV(..., param_grid, cv, scoring, ...)
```

- `param_grid`: Dictionary of hyperparameters to search.
- `cv`: Number of cross-validation folds.
- `scoring`: Metric to optimize, e.g. `'r2'`, `'neg_mean_squared_error'`, `'accuracy'`.

### ⚖️ 5. Trade-offs

| Pros | Cons |
| --- | --- |
| Exhaustive and simple to implement | Computationally expensive |
| Guarantees best grid combination | Doesn’t scale well with many parameters |
| Easy to parallelize | Ignores performance outside the grid |

### ✅ 6. When to Use

- You have a relatively small number of hyperparameters.
- You want an interpretable, systematic approach to tuning.
- You want to integrate it into pipelines for reproducible workflows.

---