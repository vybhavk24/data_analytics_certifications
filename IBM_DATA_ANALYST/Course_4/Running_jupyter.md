# Running Jupyter notebook

### Installation:

```tsx
1. Homebrew:
brew --version

2. Check if Miniforge is installed
conda --version

3. Check if it’s Miniforge (Apple Silicon-optimized)
which conda

remarks:
You’re using Anaconda, not Miniforge.
It works on M1 Macs (via Rosetta), though it’s not fully optimized for Apple Silicon like Miniforge is.

4. Create a Conda Environment for Data Science
conda create -n dsenv python=3.11

5. Then activate it:
conda activate dsenv

6.  Install Jupyter Notebook + Core Data Science Libraries
conda install jupyter pandas numpy matplotlib seaborn scikit-learn

7.  Launch Jupyter Notebook
jupyter notebook
```

## Opening Jupyter notebook

Jupyter and all ds related libraries are installed in the system.

1. Open terminal → go to the root directory:

```tsx
/Users/vybhavk24/Data/data_analytics_certifications
```

1. Give command:

```tsx
jupyter notebook
```

1. This will open Jupyter environment in a local server.
2. Navigate to the folder (manually) you want to create notebooks in, for eg:

```tsx
data_analytics_certifications/IBM_Data_Analyst/Course_4/practice/
```

1. Add files → commit to git.

### Detailed recommended work-flow:

### **Launch Jupyter Notebook via Terminal**

```
cd /Users/vybhavk24/Data/data_analytics_certifications
conda activate dsenv (if it is in base, change to dsenv)

//then launch the notebbook:

jupyter notebook
```

- Do your work in the browser interface (navigate to the right subfolder).
- Save notebooks frequently (Cmd + S).

### **2. Switch to VS Code**

- Let your terminal be still running.
- Open your repo folder in VS Code (code . if terminal is in that folder).
- Use the **Source Control panel** (Git icon in sidebar).

Here’s where VS Code shines:

- You’ll **see all file changes clearly** — new notebooks, modified files, .ipynb_checkpoints, etc.
- You can **stage only what you need**:
    - ✅ Right-click on files you want → *“Stage Changes”*
    - ❌ Right-click on junk files → *“Discard Changes”*

### **3. Commit and push in VS Code**

- Open terminal

```
git add .
git commit -m "message"
git push
```

Remember:

You’ll be in dsenv in terminal:

```tsx
(dsenv) Vybhavs-MacBook-Air:data_analytics_certifications vybhavk24$
```

And in base when running vs code (while using git or committing):

```tsx
(base) vybhavk24@Vybhavs-MacBook-Air data_analytics_certifications %
```

And it’s perfectly fine - since git is independent of conda environment.

And if you wanna run python or jupyter notebook in vs code, just do this in vs code:

```tsx
conda activate dsenv
```

And you can run it.

---