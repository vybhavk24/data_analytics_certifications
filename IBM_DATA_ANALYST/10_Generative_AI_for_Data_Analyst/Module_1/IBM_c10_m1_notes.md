# IBM_c10_m1

## Generative AI for Data analytics

Here’s a deep-dive into “Generative AI for Data Analytics,” broken into bite-sized, no-jargon chunks—with hands-on code you can run right in Jupyter or VS Code.

### What Is Generative AI?

• At its core, generative AI learns patterns in existing data and then **creates new, similar data**.

• Think of it like a super-smart mimic: show it thousands of customer reviews, and it can craft brand-new reviews that “sound” real.

• Unlike a classifier (which answers yes/no), a generative model **outputs new content**—text, images, tabular rows, even code.

### Why It Matters for Data Analysts

• **Speed up routine tasks**: auto-generate SQL queries, draft slide-ready summaries, suggest visualizations.

• **Augment scarce data**: synthesize extra rows to train predictive models or fill gaps in survey responses.

• **Consistent formatting**: turn messy free-text fields into structured summaries or categories.

• **Creative insight**: propose “what-if” scenarios by simulating different data distributions.

### Common Generative Models (High-Level)

a. Language Models (e.g., GPT-family)

– Given a prompt (“Write me an SQL query…”), they continue the text.

b. Variational Autoencoders (VAEs) & GANs

– Often used for images but can be adapted to tabular: learn latent structure, then sample new points.

c. Diffusion Models

– Emerging for images/audio; less common in day-to-day analytics—focus on VAEs/GANs and LLMs first.

### Hands-On Example: Generating Synthetic Tabular Data with an LLM

We’ll use the OpenAI Python SDK to create 100 fake customer records based on your real dataset’s schema.

```python
# 1. Install & import
!pip install openai pandas
import os, openai, pandas as pd

# 2. Set your API key (store securely!)
os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY_HERE"

# 3. Define your schema & prompt
schema = {
  "age": "integer between 18 and 70",
  "country": "one of ['USA','Canada','UK']",
  "annual_income": "float in USD between 20k and 200k",
  "purchased": "yes or no"
}

prompt = f"""
Generate 100 JSON records of synthetic customer data.
Follow this schema exactly: {schema}
Output a JSON array, each element a record.
"""

# 4. Call the model
response = openai.ChatCompletion.create(
    model="gpt-4o-mini",       # or gpt-3.5-turbo
    messages=[{"role":"user","content":prompt}],
    temperature=0.7,            # controls randomness
    max_tokens=2000
)

# 5. Parse & load into DataFrame
import json
data = json.loads(response.choices[0].message.content)
df_synth = pd.DataFrame(data)
print(df_synth.head())
```

What this does:

- Defines your columns and their value ranges
- Asks the LLM for a JSON array of 100 rows
- Parses into a pandas DataFrame for you to analyze further

### Exercises to Try

• **Summarize a real CSV**: Load any small dataset, then prompt the model:

“Give me a bullet-point summary of this DataFrame: describe distributions, missingness, and top correlations.”

• **Auto-generate SQL**: Copy–paste your table schema and ask:

“Write SQL to compute average annual income by country.”

• **Visual suggestions**: Show the model your DataFrame’s column names and ask:

“Suggest three plots to reveal key trends.”

• **Quality check**: Compare your synthetic data’s distributions to the real one. Plot histograms side by side.

---

## Generative AI tools

### 1. Quick Comparison Table

| Tool / Platform | Core Strengths | Common Use-Cases | Free Tier / Pricing |
| --- | --- | --- | --- |
| OpenAI GPT (via API) | Best-in-class text & code generation | SQL generation, narrative summaries, synthetic tabular data | $5–18 per 1 M tokens; free trial credits |
| Azure OpenAI Service | Enterprise-grade, integrated with Azure | Same as OpenAI + secure enterprise data connectors | Pay-as-you-go (token-based) |
| Google Vertex AI | Pretrained multimodal models + AutoML | Text generation, tabular synthesis, “what-if” scenarios | $0.01–$0.07 per 1 K chars |
| Hugging Face Hub | Open-source model zoo & inference API | On-prem tabular VAEs/GANs, fine-tune for domain data | Free for infra; paid HF Inference API |
| AWS SageMaker | End-to-end model training + deployment | Custom generative models (VAEs/GANs), prompt-based notebooks | $0.07–$0.18 per CPU-hr; GPU extra |
| DataRobot | No-code AutoML + generative insights | Automated narrative reports, synthetic features | Subscription only |
| [H2O.ai](http://h2o.ai/) (Driverless AI + H2O GPT) | AutoML + LLM for enterprise | Synthetic tabular rows; auto explainer stories | Contact sales |
| RapidMiner | Visual workflows + generative drafts | Data prep code snippets, summary text | Free tier up to 10 K rows; paid tiers |

### 2. LLM-Driven APIs

### 2.1. OpenAI GPT (openai-python)

1. Install & import:
    
    ```bash
    pip install openai pandas
    ```
    
2. Generate SQL or text:
    
    ```python
    import os, openai, pandas as pd
    os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
    
    # Example: Draft an SQL query for average sales
    prompt = """
    Table name: sales_data
    Columns: region (str), sales (float), date (YYYY-MM-DD)
    Write a SQL query to compute average sales per region in 2024.
    """
    resp = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role":"user","content":prompt}],
        temperature=0
    )
    print(resp.choices[0].message.content)
    ```
    
3. Synthetic tabular data (see prior example).

**Why it matters:** instant drafts save hours of boilerplate coding, letting you focus on insight.

### 2.2. Azure OpenAI Service

- **Setup:** Spin up an Azure OpenAI resource in the Azure Portal.
- **Use-Case:** Securely call GPT models against your Azure data lakes.
- **Code difference:** just swap `openai.api_base = "https://<YOUR-RESOURCE>.openai.azure.com/";` and add `api_version`.

### 3. Cloud-Native Generative Pipelines

### 3.1. Google Vertex AI

- **Models:** PaLM-2 for text, TabNet for tabular.
- **Notebook demo:**
    1. Go to Vertex AI Workbench
    2. Create a Jupyter notebook
    3. Install: `pip install google-cloud-aiplatform`
    4. Sample snippet (generate a text summary of a DataFrame):
        
        ```python
        from google.cloud import aiplatform
        client = aiplatform.AIPlatformClient()
        prompt = f"Summarize this DataFrame: {df.head(10).to_dict()}"
        result = client.predict(
            endpoint="projects/…/endpoints/…",
            instances=[{"content": prompt}]
        )
        print(result.predictions[0])
        ```
        
- **Why use it:** Native integration with BigQuery, Looker, and AutoML pipelines.

### 3.2. AWS SageMaker JumpStart

- **Built-In Models:** Pretrained diffusion, tabular VAEs/GANs, and Hugging Face endpoints.
- **Example:** Spin up a Hugging Face tabular-generation model with one click, then call via SageMaker SDK:
    
    ```python
    import boto3
    sagemaker = boto3.client("sagemaker-runtime")
    payload = {"prompt": "Generate 50 customer records with columns ..."}
    resp = sagemaker.invoke_endpoint(
        EndpointName="hf-tabular-gen-endpoint",
        ContentType="application/json",
        Body=json.dumps(payload)
    )
    df_gen = pd.DataFrame(json.loads(resp["Body"].read()))
    ```
    
- **Real-World:** Use synthetic data to augment imbalanced classes before model training.

### 4. Open-Source & AutoML Generative

### 4.1. Hugging Face

- **Models to explore:**
    - `tabular-diffusion-pytorch` for realistic tabular data
    - T5/GPT variants fine-tuned on code for SQL
- **Quick start (Inference API):**
    
    ```python
    from transformers import pipeline
    gen = pipeline(
      "text-generation",
      model="tiiuae/falcon-7b-instruct",
      trust_remote_code=True
    )
    print(gen("Write SQL to find top 5 customers by revenue in 2023", max_new_tokens=100))
    ```
    
- **Advantage:** full control over weights, on-premise deployment.

### 4.2. DataRobot & [H2O.ai](http://h2o.ai/)

- **DataRobot Paxata**: drag-and-drop UI that auto-generates feature pipelines and narrative summaries.
- **H2O GPT**: auto-explainers—upload your DataFrame, get written reports plus synthetic row suggestions.
- **When to pick these:** if you need strict MLOps, audit-ready pipelines, or no-code interfaces.

---

## Generative AI examples in DA

### Synthetic Tabular-Data Generation

• What It Is: Produce realistic-looking rows to augment small or imbalanced datasets.

• Why It Matters: Bolsters model training when real samples are scarce or sensitive (e.g., medical or financial).

• How to Try It:

```python
from openai import OpenAI
import pandas as pd, os, json

os.environ["OPENAI_API_KEY"] = "YOUR_KEY"
client = OpenAI()

schema = {
  "age":"int 18–80",
  "gender":"male/female",
  "income":"float 20k–150k"
}
prompt = f"Generate 50 JSON records with schema: {schema}"
resp = client.chat.completions.create(model="gpt-3.5-turbo",
  messages=[{"role":"user","content":prompt}],
  temperature=0.3
)
data = json.loads(resp.choices[0].message.content)
df = pd.DataFrame(data)
print(df.head())
```

- Exercise: Compare histograms of “age” and “income” between real vs. synthetic rows.

### Automated SQL-Query Drafting

• What It Is: LLMs turn table schemas and analysis questions into ready-to-run SQL.

• Why It Matters: Saves hours of boilerplate, avoids syntax errors, and speeds prototyping.

• How to Try It:

```python
import openai, os
os.environ["OPENAI_API_KEY"] = "YOUR_KEY"

schema = "sales(region, sales_amount, sales_date)"
request = f"""
Given table {schema}, write a SQL query to find top 3 regions by total sales in 2024.
"""
resp = openai.ChatCompletion.create(
  model="gpt-3.5-turbo", messages=[{"role":"user","content":request}]
)
print(resp.choices[0].message.content)
```

- Exercise: Feed in your own table definitions and ask for GROUP BY, JOINs, window-functions, etc.

### Natural-Language EDA Reports

• What It Is: Auto-written summaries of distributions, correlations, missingness, and top outliers.

• Why It Matters: Instantly generate slide-ready insights, ensuring you never miss a data-quality issue.

• How to Try It:

```python
import pandas as pd, openai, os
os.environ["OPENAI_API_KEY"]="YOUR_KEY"

df = pd.read_csv("your_data.csv").head(100).to_dict()
prompt = f"Summarize these 100 rows. Mention key stats, missing values, and correlations: {df}"
resp = openai.ChatCompletion.create(
  model="gpt-4o-mini",
  messages=[{"role":"user","content":prompt}],
  temperature=0
)
print(resp.choices[0].message.content)
```

- Exercise: Tweak “temperature” and max_tokens to see how concise vs. detailed you can make it.

### Missing-Value Imputation with VAEs

• What It Is: Train a Variational Autoencoder on your numeric features; let it predict (impute) missing entries.

• Why It Matters: Often yields more realistic estimates than mean/median fill, especially when features interact nonlinearly.

• How to Try It:

1. Use PyTorch Lightning’s `VAE` tutorial on tabular data.
2. Mask 10–20% of values in a CSV, train the VAE, then compare imputed vs. actual.
• Exercise: Compute RMSE of VAE imputation vs. simple-fill to see improvement.

### “What-If” Scenario Generation

• What It Is: Given your historical data, ask an LLM to simulate how key metrics change under hypothetical shifts (e.g., 10% price increase).

• Why It Matters: Rapidly test pricing, marketing, or policy “experiments” before running them in real life.

• How to Try It:

```python
import pandas as pd
df = pd.read_csv("transactions.csv")
# e.g., manually code multiplier, then ask LLM to summarize:
df["price_up_10"] = df["price"] * 1.10
prompt = f"Compare total revenue before vs. after 10% price hike for this sample: {df.head().to_dict()}"
# feed prompt to LLM as in prior examples
```

- Exercise: Automate scenario-generation loops (e.g., 5%, 10%, 20%) and have the LLM recommend the sweet spot.

---

## Generative AI for Data Generation & Augmentation

### 1. Generation vs. Augmentation: What’s the Difference?

- **Data Generation**
You create entirely new synthetic records that resemble your real data.
• Example: Produce 1,000 fake customer profiles matching your schema.
- **Data Augmentation**
You apply systematic transformations to existing records to create variations.
• Example: For text reviews, you swap synonyms, shuffle clauses, or insert typos.

Both expand your dataset—but generation gives you new points, augmentation gives you variations on what you already have.

### 2. Why It Matters for a Data Analyst

1. **Scarce or Imbalanced Data**
• Fraud cases, rare diseases, edge-case logs. Synthetic rows can rebalance your classes.
2. **Privacy & Compliance**
• Generate “look-alike” data that preserves statistical properties but contains no real PII.
3. **Robustness & Generalization**
• Expose models to slightly different scenarios so they don’t overfit one distribution.
4. **Rapid Prototyping**
• Simulate “what-if” scenarios (price hikes, feature shifts) without waiting on business teams.

### 3. Core Techniques & Tools

| Technique | Ideal For | Key Libraries/Tools |
| --- | --- | --- |
| LLM-Driven Tabular AI | Quick synthetic rows | OpenAI GPT (via `openai`), Azure OAI |
| GANs (Tabular GAN) | High-fidelity synthesis | SDV (`ctgan`), PyTorch, TensorFlow |
| Variational AEs | Imputation & synthesis | Keras/TensorFlow, PyTorch Lightning |
| SMOTE & Variants | Minor-class oversample | `imbalanced-learn` |
| Text Augmentation | NLP tasks | `nlpaug`, Hugging Face |
| Image Augmentation | CV tasks | `albumentations`, `imgaug` |

### 4. Hands-On: Synthetic Tabular Data with SDV

**Step 1. Install & Import**

```bash
pip install sdv pandas
```

```python
from sdv.tabular import CTGAN
import pandas as pd

# 1. Load your real dataset
real = pd.read_csv("your_data.csv")

# 2. Train a CTGAN on it
model = CTGAN(epochs=300)
model.fit(real)

# 3. Sample synthetic rows
synthetic = model.sample(500)
print(synthetic.head())

# 4. Combine & inspect
combined = pd.concat([real, synthetic], ignore_index=True)
print("Original size:", len(real), "Augmented size:", len(combined))
```

**Why CTGAN?**

CTGAN (Conditional Tabular GAN) learns both numerical and categorical distributions, preserving relationships between columns.

### 5. Hands-On: Augmenting Text Data

**Use-Case:** You have 1,000 customer reviews but need 5,000 for a sentiment model.

```bash
pip install nlpaug
```

```python
import pandas as pd
import nlpaug.augmenter.word as naw

df = pd.read_csv("reviews.csv")
augmenter = naw.SynonymAug(aug_src='wordnet')

augmented_texts = []
for text in df['review_text']:
    augmented_texts.append(augmenter.augment(text, n=3))  # 3 variants

# Convert list of lists into flat DataFrame
rows = []
for originals, variants in zip(df['review_text'], augmented_texts):
    rows.append({'text': originals, 'label': df['sentiment']})
    for var in variants:
        rows.append({'text': var, 'label': df['sentiment']})
aug_df = pd.DataFrame(rows)
print(aug_df.shape)  # ~4× original
```

**Why It Works:**

Swapping synonyms or paraphrasing diversifies language patterns without altering sentiment.

---

## Generative AI for Data Preparation

### 1. Why It Matters

- **Speed**: Auto-correct typos, fill gaps, standardize formats in seconds.
- **Consistency**: One prompt produces uniform rules across thousands of rows.
- **Context-awareness**: Models infer patterns (e.g., country → currency) rather than applying blind rules.
- **Scalability**: Apply the same “intelligent” cleaning logic to new data with minimal tweaks.

### 2. Core Prep Tasks & Generative Techniques

| Task | Generative Technique | Benefit |
| --- | --- | --- |
| Text cleaning & standardization | LLM prompt “normalize abbreviations, fix typos” | Consistent, context-driven corrections |
| Missing-value imputation | LLM or VAE “predict plausible values” | Respects multivariate relationships |
| Categorical encoding | LLM “map variants to canonical labels” | Dynamically handles new/unseen labels |
| Feature suggestion | LLM “derive 3 features from these columns” | Rapid ideation of ratios, buckets, flags |
| Outlier detection & handling | LLM “flag anomalous rows with reasons” | Human-readable anomaly explanations |

### 3. Example 1: Text Cleaning & Normalization

Imagine a “location” column with messy entries like “nyc”, “New York”, “NewYork City”. Let’s standardize.

```python
# 1. Install & imports
!pip install openai pandas
import os, openai, pandas as pd

# 2. Load sample data
df = pd.DataFrame({
    "location": ["nyc", "New York", "Nw Yrk", "NewYork City", "Los Angeles"]
})

# 3. Set API key
os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"

# 4. Craft prompt
prompt = f"""
You are a data cleaner. Normalize these location names
to full city names:
{df['location'].tolist()}
Return a JSON array of cleaned names in the same order.
"""

# 5. Call the model
resp = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role":"user","content":prompt}],
    temperature=0
)

# 6. Parse & assign
import json
cleaned = json.loads(resp.choices[0].message.content)
df['location_clean'] = cleaned
print(df)
```

**What’s happening**

- The LLM infers that “nyc” → “New York City”, “Nw Yrk” → “New York City”.
- You get a uniform column without writing regex or lookup tables.

### 4. Example 2: Missing-Value Imputation

Say 15% of “age” and “income” are null. Use an LLM to guess realistic values.

```python
import pandas as pd, openai, os, json

# 1. Sample data with missing
df = pd.DataFrame([
    {"age": 34, "income": 58000},
    {"age": None, "income": 72000},
    {"age": 52, "income": None},
    {"age": None, "income": None}
])

os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"

prompt = f"""
Fill missing 'age' (18–80) and 'income' (20k–200k)
based on other fields. Return complete JSON records.
Records: {df.to_dict(orient='records')}
"""

resp = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content":prompt}],
    temperature=0
)

completed = pd.DataFrame(json.loads(resp.choices[0].message.content))
df.update(completed)
print(df)
```

**Why this beats mean-fill**

The model uses correlations: e.g., high income suggests older age, yielding more plausible imputations.

### 5. Example 3: Feature Engineering Suggestions

Let’s ask the model to propose new features:

```python
import openai, os, pandas as pd

df = pd.DataFrame({
    "visits": [5, 12, 3],
    "spent": [120, 450, 80],
    "days_active": [30, 90, 15]
})

os.environ["OPENAI_API_KEY"]="YOUR_API_KEY"

prompt = f"""
Given these numeric columns: visits, spent, days_active,
suggest three new features (with formula) that could help a
model predict customer lifetime value.
"""

resp = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role":"user","content":prompt}],
    temperature=0.5
)

print(resp.choices[0].message.content)
```

**You might get**

- `avg_spend_per_visit = spent / visits`
- `visit_frequency = visits / days_active`
- `spend_velocity = spent / log(days_active + 1)`

Implement them in pandas and immediately enrich your dataset.

---

## Generative AI for Querying Databases

### 1. What & Why

- **What**
Generative AI models (like GPT-4, open-source LLMs) take a description of your tables, columns, and analysis goal, then output a syntactically correct SQL query.
- **Why**
• Cuts down hours of trial-and-error typing.
• Speeds prototyping—ask “top 5 products by churn rate” and get code back.
• Lowers barrier for non-SQL experts on your team.
• Ensures consistency in style (formatting, naming conventions).

### 2. Core Components

1. **Database Schema Description**
You need table names, column names/types, relationships.
2. **Prompt Engineering**
Clearly communicate context:
    
    ```
    “Table users(id INT, name TEXT, country TEXT),
     orders(id INT, user_id INT, amount FLOAT, created_at DATE).
     Write SQL to find each country’s total order amount in 2024.”
    ```
    
3. **LLM Invocation**
Call an API or local model to generate the `SELECT ...` statement.
4. **Query Execution**
Use a Python DB driver (e.g., psycopg2, SQLAlchemy) to run the generated SQL.
5. **Result Validation**
• Sanity-check row counts, column types.
• Spot-check a few rows against known answers.

### 3. Example: Natural-Language → SQL → Pandas

### Prerequisites

- Python 3.8+, Jupyter Notebook or VS Code
- `openai`, `sqlalchemy`, `pandas`, `psycopg2` (for Postgres)

```bash
pip install openai sqlalchemy pandas psycopg2-binary
```

### Step 1. Define Your DB Connection

```python
from sqlalchemy import create_engine
import os

# e.g., Postgres connection string
DB_URI = "postgresql+psycopg2://user:pass@localhost:5432/mydb"
engine = create_engine(DB_URI)
```

### Step 2. Describe Your Schema

```python
schema = """
Tables:
  users(
    id INT PRIMARY KEY,
    name TEXT,
    country TEXT
  )
  orders(
    id INT PRIMARY KEY,
    user_id INT REFERENCES users(id),
    amount FLOAT,
    created_at DATE
  )
"""
```

### Step 3. Craft & Send the Prompt

```python
import openai
openai.api_key = os.getenv("OPENAI_API_KEY")

def generate_sql(nl_query: str) -> str:
    prompt = f"""
You are a SQL generator.
Given the schema:
{schema}
Write a single SQL query (compatible with PostgreSQL) for:
{nl_query}

Only output the SQL statement, without explanation.
"""
    resp = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role":"user", "content": prompt}],
        temperature=0
    )
    return resp.choices[0].message.content.strip()
```

### Step 4. Execute & Load into Pandas

```python
import pandas as pd

nl = "Find the top 5 countries by total order amount in 2024."
sql = generate_sql(nl)
print("Generated SQL:\\n", sql)

# Execute
df = pd.read_sql(sql, engine)
print(df)
```

### 4. Advanced: Function-Calling with OpenAI (GPT-4)

Use the [function-calling](https://platform.openai.com/docs/guides/gpt/function-calling) feature so the model returns structured JSON:

```python
functions = [
  {
    "name": "create_sql",
    "description": "Generate a SQL query",
    "parameters": {
      "type": "object",
      "properties": {
        "query": {"type": "string", "description": "The SQL statement to execute"}
      },
      "required": ["query"]
    }
  }
]

resp = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content": nl}],
    functions=functions,
    function_call={"name":"create_sql"}
)
sql = resp.choices[0].message.function_call.arguments["query"]
```

---

## Generative AI for Q & A and Model Insights

### 1. What & Why

**Q & A models** combine a **retrieval** layer (to fetch relevant data) with a **generative** layer (to craft answers).

- You can query a CSV, database, or document corpus in plain English (e.g., “Which region saw highest growth in Q1?”).
- Analysts get instant insights without manual querying or static dashboards.
- Embeds business rules, context and explanations—making insights more actionable.

### 2. Core Components

1. **Data Ingestion**
• Load tables, documents or code into memory or a vector store.
2. **Embedding & Indexing**
• Convert text (e.g., row descriptions, report sections) into vector embeddings (OpenAI, Hugging Face).
• Store in a vector database (Pinecone, Weaviate, PGVector) for fast similarity search.
3. **Retriever**
• Given a question, fetch top-k relevant chunks via embedding similarity.
4. **Prompt Construction**
• Combine retrieved context with the user’s question into a prompt template.
5. **Generative LLM**
• Feed the prompt to an LLM (GPT-4, gpt-3.5-turbo, or open-source) to generate a coherent answer.
6. **Post-Processing & Insights**
• Optionally parse LLM output into structured JSON, charts or recommendations.

Architecture Diagram (ASCII):

```
[ User Question ]
        ↓
 [ Retriever ] ← Embedding Store ← Preloaded Data
        ↓
[ Prompt Template + Context ]
        ↓
   [ LLM Model ]
        ↓
 [ Natural‐Language Answer ]
```

### 3. Hands-On: Simple Q&A over a Pandas DataFrame

Let’s build a notebook that:

1. loads sales data,
2. embeds row summaries,
3. answers questions via OpenAI.

```python
# 1. Install & Imports
!pip install openai pandas sentence-transformers faiss-cpu
import os, openai, pandas as pd
from sentence_transformers import SentenceTransformer
import faiss, numpy as np

# 2. Load Data
df = pd.read_csv("sales_data.csv")  # columns: region, date, sales_amount
df['text'] = df.apply(lambda r: f"On {r.date}, {r.region} sold ${r.sales_amount}", axis=1)

# 3. Embed Rows
embedder = SentenceTransformer("all-MiniLM-L6-v2")
embeddings = embedder.encode(df['text'].tolist(), show_progress_bar=True)

# 4. Build FAISS Index
d = embeddings.shape[1]
index = faiss.IndexFlatL2(d)
index.add(np.array(embeddings))

# 5. Define Retriever
def retrieve(question, top_k=5):
    q_emb = embedder.encode([question])
    D, I = index.search(np.array(q_emb), top_k)
    return df.iloc[I[0]]['text'].tolist()

# 6. Query + LLM Prompt
os.environ["OPENAI_API_KEY"] = "YOUR_KEY"
def answer(question):
    context = "\\n".join(retrieve(question))
    prompt = f"""
You are a data analyst assistant.
Use the context below to answer the question.
If data isn’t present, say “Data not available.”

Context:
{context}

Question:
{question}
"""
    resp = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role":"user","content":prompt}],
        temperature=0
    )
    return resp.choices[0].message.content.strip()

# 7. Try It
print(answer("What was the total sales in Europe in January 2024?"))
```

### 4. Advanced: RAG with LangChain & Pinecone

Switch to a managed vector store and LangChain’s abstractions:

```python
# pip install langchain pinecone-client openai
from langchain import OpenAI, PromptTemplate, LLMChain
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import Pinecone
from langchain.docstore.document import Document

import pandas as pd, pinecone, os

os.environ["PINECONE_API_KEY"] = "YOUR_KEY"
pinecone.init(index="sales-idx", environment="us-west1-gcp")

# 1. Load & embed
df = pd.read_csv("sales_data.csv")
docs = [Document(page_content=r.text) for _,r in df.iterrows()]

embeddings = OpenAIEmbeddings()
vector_db = Pinecone.from_documents(docs, embeddings, index_name="sales-idx")

# 2. Chain setup
template = """
Context:
{context}

Question:
{question}

Answer concisely with numbers where relevant.
"""
prompt = PromptTemplate(input_variables=["context","question"], template=template)
llm = OpenAI(temperature=0)
qa = LLMChain(llm=llm, prompt=prompt, verbose=False)

# 3. Ask
res = qa.run({"context": "\\n".join(
         [doc.page_content for doc in vector_db.similarity_search("Europe January 2024", k=5)]
       ), "question":"Total sales in Europe in January 2024?"})
print(res)
```

### 5. Model Insights & Evaluation

1. **Answer Accuracy**
• Compare LLM answers against ground-truth sums or known KPIs.
• Automate with unit tests: fetch a fixed question and `assert` expected result.
2. **Relevance of Retrieved Chunks**
• Log retrieval hits; manually inspect if top-k contain needed info.
3. **Latency & Cost**
• Measure average response time and token usage per query.
4. **Explainability**
• Ask the model “How did you compute that?”—get chain-of-thought for auditing.

---