# IBM_c10_m2

## Generative AI for Data Insights

### 1. What & Why

**What**

Generative-AI for data insights uses large language models (LLMs) (e.g., GPT-4, LLaMA) or specialized analytics models to:

- **Summarize** datasets in plain-English narratives
- **Highlight** top correlations, trends, and outliers
- **Explain** statistical metrics and model outputs
- **Recommend** next analyses or visualizations

**Why It Matters**

- **Speed:** Auto-generate slide-ready insights in seconds.
- **Consistency:** Uniform narrative style across reports.
- **Accessibility:** Lowers barrier for non-technical stakeholders.
- **Focus:** Frees you to dive deeper into root-cause analysis, not boilerplate summaries.

### 2. Core Capabilities & Use-Cases

| Capability | Example Use-Case |
| --- | --- |
| Narrative EDA | “Tell me the top 3 takeaways from this sales dataset.” |
| Correlation Detection | “Which features most influence purchase volume?” |
| Anomaly & Outlier Flags | “List transactions that deviate significantly from mean.” |
| Automated Reporting | “Generate a weekly summary of site metrics.” |
| Scenario Recommendations | “Based on seasonality, suggest optimal inventory levels.” |

### 3. Hands-On: Narrative EDA with OpenAI

### 3.1. Setup

```bash
pip install openai pandas
```

```python
import os, openai, pandas as pd

# 1. Load DataFrame
df = pd.read_csv("your_data.csv")

# 2. Prep a small sample (head) or stats
stats = df.describe(include='all').to_dict()

# 3. Configure OpenAI
os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
openai.api_key = os.getenv("OPENAI_API_KEY")
```

### 3.2. Craft & Call

```python
prompt = f"""
You are a data analyst. Here are summary stats of my DataFrame:
{stats}

Please provide:
1. Three key insights (bullet points).
2. Any anomalies or outliers.
3. Suggested next visualizations to explore.
"""

response = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content": prompt}],
    temperature=0.3,
    max_tokens=400
)

print(response.choices[0].message.content)
```

> What you get:
> 
> 
> • “Sales peaked in Q4 likely due to holiday promotions.”
> 
> • “Transactions above \$5,000 are <1% — investigate those VIP customers.”
> 
> • “Plot revenue vs. marketing spend by month.”
> 

### 4. Prompt Patterns for Insight Generation

1. **Few-Shot Insight Prompt**
    
    ```
    Here is a DataFrame summary:
    {stats}
    
    Example Insight:
    - “Feature X has a strong positive correlation (0.85) with Target Y—consider using X in your model.”
    
    Now, generate three similar insights.
    ```
    
2. **Chain-of-Thought**
    
    ```
    Think step by step: examine means, medians, outliers, then draw conclusions.
    ```
    
3. **Function Calling (Structured JSON)**
Define a function schema so the model returns structured insights:
    
    ```python
    functions = [{
      "name":"report_insights",
      "parameters":{
        "type":"object",
        "properties":{
          "insights": {"type":"array","items":{"type":"string"}},
          "anomalies":{"type":"array","items":{"type":"string"}},
          "recommendations":{"type":"array","items":{"type":"string"}}
        },
        "required":["insights"]
      }
    }]
    # Call with functions=... and parse JSON for programmatic use.
    ```
    

### 5. Advanced: Correlation & Anomaly Detection

### 5.1. Auto-Detect Correlations

```python
# Compute correlations
corrs = df.corr().abs().unstack().sort_values(ascending=False)
top_pairs = corrs[corrs<1].drop_duplicates().head(5).to_dict()

# Prompt the LLM
prompt = f"Here are the top 5 absolute correlations:\\n{top_pairs}\\nExplain why these might exist."
resp = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role":"user","content":prompt}],
    temperature=0
)
print(resp.choices[0].message.content)
```

### 5.2. Flagging Outliers

```python
# Z-score method
from scipy import stats
import numpy as np

z_scores = np.abs(stats.zscore(df.select_dtypes(include=[np.number])))
outlier_rows = (z_scores > 3).any(axis=1)
sample_outliers = df[outlier_rows].head().to_dict(orient='records')

# Narrate
prompt = f"These rows are statistical outliers:\\n{sample_outliers}\\nDescribe possible reasons."
resp = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content":prompt}],
    temperature=0
)
print(resp.choices[0].message.content)
```

---

## Generative AI for Visualization

### 1. What & Why

- **What:** Use LLMs to suggest chart types, generate plotting code (Matplotlib, Seaborn, Plotly), auto-style themes, and even write captions.
- **Why:**
    - **Speeds prototyping**: no more hunting syntax in docs.
    - **Standardizes style**: consistent colors, fonts, layouts across reports.
    - **Democratizes viz**: teammates can ask in plain English and get code.
    - **Enhances storytelling**: AI-drafted captions highlight key insights.

### 2. Core Capabilities

| Capability | Example Use-Case | Tech Stack |
| --- | --- | --- |
| Chart-type recommendation | “What’s best for showing revenue vs. time?” | GPT-4, LLMs |
| Code generation | “Write Plotly code for a dual-axis line/bar” | `openai-python`, Codex models |
| Theme & styling | “Apply a dark theme with gridlines off” | Seaborn/Mpl style configs |
| Narrative captions | “Explain this scatter plot in 2 bullets” | GPT-3.5-turbo / GPT-4 |
| Interactive dashboards | “Generate a Streamlit app with 3 charts” | Streamlit + LLM for code snippets |

### 3. Hands-On: From Prompt to Plot

### 3.1. Setup

```bash
pip install openai pandas matplotlib seaborn plotly
```

```python
import os, openai, pandas as pd
openai.api_key = os.getenv("OPENAI_API_KEY")

# Sample DataFrame
df = pd.DataFrame({
    "date": pd.date_range("2024-01-01", periods=12, freq="M"),
    "revenue": [1200, 1500, 1100, 1800, 2000, 2100, 2300, 2200, 2400, 2600, 2800, 3000],
    "cost":    [800,  900,  850,  950,  980, 1000, 1100, 1050, 1150, 1200, 1300, 1400]
})
```

### 3.2. Ask the AI for Plot Code

```python
prompt = f"""
You are a Python plotting assistant.
Given a pandas DataFrame `df` with columns ['date','revenue','cost'],
write a Plotly Express script to show revenue and cost over time
with two lines and a custom title "Monthly P&L Trend".
Include axis labels and a legend.
"""

response = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user", "content": prompt}],
    temperature=0
)
code = response.choices[0].message.content
print(code)
```

> What you’ll typically get:
> 
> 
> ```python
> import plotly.express as px
> fig = px.line(df, x='date', y=['revenue','cost'],
>               title='Monthly P&L Trend',
>               labels={'value':'USD','variable':'Metric'})
> fig.update_layout(template='plotly_dark')
> fig.show()
> ```
> 

Copy–paste into a cell to render the interactive chart.

### 4. Prompt Patterns & Variations

1. **Few-Shot Styling**
    
    ```
    Example:
    - Chart: px.bar(df, x='region', y='sales', color='region')
    - Theme: plotly_white
    
    Now write similar code for a line chart of date vs. profit with plotly_white.
    ```
    
2. **Function Calling (Structured JSON)**
    
    ```python
    functions=[{
      "name":"generate_plot",
      "description":"Return Python code for a chart",
      "parameters":{
        "type":"object",
        "properties":{
          "language":{"type":"string"},
          "code":{"type":"string"}
        },
        "required":["language","code"]
      }
    }]
    ```
    
3. **Caption Generation**
    
    ```
    “Given this Plotly figure object, write two bullet-point captions explaining the trends.”
    ```
    

---

## Generative AI for Creating Dashboards

### 1. What & Why

**What:**

Use an LLM to produce full-fledged dashboard scripts (Streamlit, Dash, Voila, Panel) or configuration files (Power BI, Tableau) from a simple prompt describing your data and requirements.

**Why:**

- **Speed:** No more wrestling with layout APIs—get a working prototype in seconds.
- **Consistency:** Enforce your team’s style guide automatically (colors, fonts, naming conventions).
- **Accessibility:** Non-developers can spin up dashboards by writing plain-English requests.
- **Iteration:** Rapidly tweak prompts to add filters, change visuals, or adjust layouts without hand-coding.

### 2. Core Capabilities & Tools

| Capability | Tool/Library | What It Does |
| --- | --- | --- |
| Full code generation | OpenAI GPT + Streamlit | Builds a complete `.py` dashboard with widgets |
| Interactive callbacks | OpenAI GPT + Dash | Generates Flask+React code for dynamic filtering |
| No-code config creation | GPT + Power BI REST API | Produces JSON PBIX templates or JSON theme files |
| Layout & styling | GPT + Panel/HoloViz | Suggests grid layouts, styling and theming |
| Narrative annotations & exports | GPT + Voila + nbconvert | Embeds explanatory text, exports to HTML/PDF |

### 3. Example: Streamlit Dashboard via OpenAI

This example prompts GPT-4 to generate a Streamlit app for a sales CSV with filters and charts.

```bash
pip install openai streamlit pandas plotly
```

```python
import os, openai

# 1. Configure
os.environ["OPENAI_API_KEY"] = "YOUR_KEY"
openai.api_key = os.getenv("OPENAI_API_KEY")

# 2. Describe your data & goals
schema = """
Data file: sales_data.csv
Columns: date (YYYY-MM-DD), region (str), product (str), sales (float), units (int)
Goal: Interactive dashboard with:
- Date range filter
- Region multiselect
- Line chart of monthly sales
- Bar chart of units by product
"""

prompt = f"""
You’re a Streamlit dashboard generator. Given the schema below, write a complete Python script:

{schema}

Requirements:
1. Read CSV into pandas.
2. Create sidebar filters for date range and region.
3. Display metrics: total sales, total units.
4. Plot a line chart (monthly sales) and a bar chart (units by product).
5. Use Plotly for charts, set page title to "Sales Dashboard".
6. Include comments explaining each section.
"""

# 3. Generate code
resp = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content":prompt}],
    temperature=0
)
code = resp.choices[0].message.content

# 4. Save to file
with open("dashboard.py", "w") as f:
    f.write(code)

print("Dashboard script generated: dashboard.py")
```

Then run:

```bash
streamlit run dashboard.py
```

You’ll get a fully interactive dashboard without writing a single widget manually.

### 4. Prompt Patterns & Function Calling

1. **Few-Shot Example**
    
    ```
    Example:
    ```python
    import streamlit as st
    df = st.file_uploader("Upload CSV")
    ```
    
2. **Function Calling (Structured Output)**
    
    ```python
    functions = [{
      "name": "generate_dashboard",
      "description": "Return code and dependencies for a dashboard",
      "parameters": {
        "type": "object",
        "properties": {
          "language": {"type":"string"},
          "code": {"type":"string"}
        },
        "required": ["language","code"]
      }
    }]
    # Call ChatCompletion with functions=functions & parse JSON.
    ```
    
3. **Layout Specification**
    
    ```
    “Place filters in sidebar, metrics at top, charts below in two columns.”
    ```
    

---

## Generative AI for Storytelling

### 1. What & Why

**What**

Generative-AI for storytelling uses LLMs (like GPT-4) to craft coherent, engaging narratives from data, charts, or bullet-point insights.

**Why It Matters**

- **Bridge the gap** between technical analysis and non-technical stakeholders.
- **Save hours** writing reports, blog drafts, or presentation scripts.
- **Ensure consistency** in tone, brand voice, and quality.
- **Personalize** storytelling for different audiences (executives, customers, partners).

### 2. Core Capabilities & Use-Cases

| Capability | Use-Case |
| --- | --- |
| Executive Summaries | One-page business impact report |
| Blog & Article Drafts | SEO-friendly posts riffing on your data trends |
| Slide Deck Scripts | Speaker notes and narrative flow for PowerPoint |
| Customer Stories | Case studies with personalized recommendations |
| Interactive Narratives | Chatbot-style data exploration |

### 3. Hands-On: From Stats to Executive Summary

### 3.1. Setup

```bash
pip install openai pandas
```

```python
import os, openai, pandas as pd

os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
openai.api_key = os.getenv("OPENAI_API_KEY")

# Sample DataFrame
df = pd.DataFrame({
    "month": ["Jan","Feb","Mar","Apr","May"],
    "sales": [1200,1500,1100,1800,2000],
    "cost":  [800,900,850,950,980]
})
stats = df.describe(include='all').to_dict()
```

### 3.2. Prompt & Generate

```python
prompt = f"""
You are an executive summary writer.
Based on these summary stats:
{stats}

Write a 3-paragraph summary highlighting:
1. Key trends
2. Business impact
3. Recommendations

Use a professional, concise tone.
"""

resp = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content":prompt}],
    temperature=0.3,
    max_tokens=300
)

print(resp.choices[0].message.content)
```

> You’ll get something like:
> 
> 
> “In the first quarter, revenue grew by X% month-over-month…
> 
> This trend improved our gross margin by…
> 
> We recommend reallocating budget to…”
> 

### 4. Prompt Patterns & Function Calling

1. **Few-Shot Style Guide**
    
    ```
    Example Summary:
    “In Q1, we saw a 20% lift in sales driven by product X launch…”
    Now write in a similar style for our dataset.
    ```
    
2. **Structured Output with Function Calling**
    
    ```python
    functions = [{
      "name":"generate_story",
      "description":"Craft narrative from dataset stats",
      "parameters":{
        "type":"object",
        "properties":{
          "summary":{"type":"string"},
          "insights":{"type":"array","items":{"type":"string"}},
          "next_steps":{"type":"array","items":{"type":"string"}}
        },
        "required":["summary","insights"]
      }
    }]
    
    resp = openai.ChatCompletion.create(
      model="gpt-4o-mini",
      messages=[{"role":"user","content":prompt}],
      functions=functions,
      function_call={"name":"generate_story"}
    )
    story = resp.choices[0].message.function_call.arguments
    ```
    
    You now have JSON you can render into a report template.
    

### 5. Advanced: Embedding Charts & Personalized Narratives

1. **Embed Chart Context**
    
    ```python
    chart_json = fig.to_json()  # Plotly figure from previous viz
    prompt = f"""
    Here is a Plotly chart config:
    {chart_json}
    
    Write two bullet-point insights and a single narrative paragraph explaining key takeaways.
    """
    ```
    
2. **Audience-Aware Tone**
    - **Executives:** “Emphasize high-level ROI and strategic risks.”
    - **Engineers:** “Focus on data integrity checks and anomaly root-causes.”
    - **Customers:** “Highlight benefits, call-to-action, and next steps.”
3. **Automated Slide Deck Generation**
    - Generate PowerPoint XML or use `python-pptx` via AI-written code:
        
        ```
        “Write Python code using python-pptx to create a slide titled ‘Q1 Highlights’ with three bullet points: …”
        ```
        

---

## Challenges in Using Generative AI

Generative AI promises to automate content creation and supercharge workflows, but it comes with critical hurdles:

- **Data Quality & Quantity**: These models crave massive, high-fidelity datasets. Biased, incomplete or low-volume data leads to poor or even harmful outputs.
- **Bias & Fairness**: If training data reflects historical prejudices—racial, gender or cultural—models will amplify them, risking unethical or discriminatory results.
- **Hallucinations**: LLMs often “make up” facts or bogus code snippets; without human oversight, you can’t trust every generated token.
- **Intellectual-Property & Legal Risks**: Outputs can unknowingly mimic copyrighted text or imagery, raising ownership disputes and compliance issues.
- **Interpretability & Explainability**: Deep generative architectures are black boxes. Tracing *why* a model produced a certain result is notoriously difficult, limiting trust in sensitive domains.
- **Resource Intensity**: Training or fine-tuning large models demands vast compute (GPUs/TPUs), driving up costs and environmental footprint unless carefully optimized.

## Responsible-AI Use for Data Professionals

Building and deploying AI responsibly means embedding ethics and governance throughout the data lifecycle:

- **Transparency & Governance**: Maintain clear records of data sources, model versions, prompt templates and who has access—using scorecards or audit logs to satisfy internal and external audits.
- **Fairness & Bias Mitigation**: Proactively test for demographic skews. Employ fairness-aware algorithms and diverse review panels to catch and correct biases before deployment.
- **Privacy & Security**: Sanitize or anonymize PII/PHI, encrypt data at rest and in transit, and follow data-handling frameworks like GDPR or HIPAA. Never feed sensitive records into public APIs without proper controls.
- **Explainability & Interpretability**: Incorporate model-explanation tools (SHAP, LIME) so stakeholders can see *how* a prediction was made, not just *what* it is.
- **Accountability & Auditing**: Assign clear AI-ownership roles (data stewards, risk officers) and use checklists or Responsible-AI scorecards to track compliance against ethical principles and regulatory requirements.
- **Multi-Stakeholder Alignment**: Engage legal, HR, operations and business teams early to align AI capabilities with organizational values, risk appetite and user expectations.

## Key Challenges in Healthcare

Healthcare’s complexity magnifies every AI and operational pain point:

- **Infrastructure Deficiencies**: A Union Health Ministry report highlights critical shortages of ICU beds, dedicated transplant OTs and HLA labs, delaying surgeries and crushing capacity in government hospitals.
- **Workforce Shortages & Burnout**: Chronic understaffing of physicians, nurses and specialists—especially in rural or under-resourced areas—leads to overwork, high turnover and compromised patient care.
- **Rising Costs & Funding Gaps**: U.S. healthcare is set to exceed \$5 trillion in 2025, straining budgets at payers and providers alike. Hospitals juggle expensive technologies, compliance demands and shrinking margins.
- **Data Management & Security**: With growing volumes of e-records, imaging and IoT streams, health systems must secure PHI against rampant cyberattacks while ensuring interoperability across EMRs, labs and third-party apps.
- **Regulatory & Compliance Complexity**: Evolving mandates—from data-privacy laws to FDA approvals for AI diagnostics—force providers to invest heavily in legal, IT and quality-assurance teams to stay compliant.
- **Equity & Access**: Persistent rural–urban divides and out-of-pocket payment burdens (over 60 % of healthcare spend in India) leave millions without affordable, high-quality care, driving preventable morbidity and mortality.

---