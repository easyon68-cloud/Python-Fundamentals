# 🐍 Python Fundamentals & Data Analysis — Complete Notebook

## 📌 Project Overview

This notebook is a **structured, hands-on guide** through Python's core programming concepts and the most widely-used data science libraries. It bridges the gap between Python syntax and real-world data workflows — combining classroom fundamentals with applied analysis on a real government salary dataset.

> **Dataset:** [San Francisco City Employee Salaries](https://raw.githubusercontent.com/Muralimekala/python/master/Salaries.csv)
> **Also Used:** Seaborn built-in datasets — `tips`, `fmri`
> **Notebook:** `Python_Fundamentals.ipynb`

---

## 📚 Table of Contents

| # | Section | Topics Covered |
|---|---------|---------------|
| 1 | 🔑 Python Keywords | Reserved words, `nonlocal`, scope |
| 2 | ➕ Mathematical Operations | Arithmetic & assignment operators |
| 3 | ✅ Boolean & Logical Operators | `and`, `or`, `not`, eligibility logic |
| 4 | 🚨 Exception Handling | `try/except/else/finally`, custom errors |
| 5 | 🐼 Pandas | Loading, cleaning, groupby, aggregation |
| 6 | 🔢 NumPy | Array indexing, slicing, `.values` |
| 7 | 📐 SciPy | Descriptive statistics on real data |
| 8 | 🧮 Math Module | `sqrt`, `log`, built-in math functions |
| 9 | 🎨 Matplotlib | Base plotting, grid, axis customization |
| 10 | 🌊 Seaborn | `relplot`, `displot`, KDE, line plots |
| 11 | 📊 Plotly | Interactive scatter, color, symbol mapping |

---

## 🔑 1. Python Keywords

```python
import keyword
print(keyword.kwlist)
# ['False', 'None', 'True', 'and', 'as', 'assert', 'async', ...]
```

Python has **35 reserved keywords** — this section covers what they are, why they can't be used as identifiers, and a deep-dive into `nonlocal` for closure-based variable scoping.

```python
def outer_function():
    x = 10
    def inner_function():
        nonlocal x   # Modify outer variable from inner scope
        x = 20
    inner_function()
    print(x)  # → 20
```

---

## ➕ 2. Mathematical Operations

All Python arithmetic and compound assignment operators demonstrated with practical examples:

| Operator | Meaning | Example |
|----------|---------|---------|
| `+=` | Add and assign | `a += 10` |
| `-=` | Subtract and assign | `a -= 10` |
| `*=` | Multiply and assign | `a *= 2` |
| `/=` | Divide and assign | `a /= 1000` |
| `%` | Modulo (remainder) | `b % 2` |
| `**=` | Power and assign | `a **= 2` |
| `//=` | Floor divide and assign | `b //= 2` |

---

## ✅ 3. Boolean & Logical Operators

A real-world **job eligibility system** was built using `and` / `or` logic to demonstrate compound conditionals:

```python
def evaluate_eligibility(age, has_degree, experience_years, project_score, is_manager):
    # Multi-condition logic using and / or combinations
    ...
```

**Truth tables covered:**

| `A` | `B` | `A and B` | `A or B` |
|-----|-----|-----------|----------|
| True | True | ✅ True | ✅ True |
| True | False | ❌ False | ✅ True |
| False | True | ❌ False | ✅ True |
| False | False | ❌ False | ❌ False |

---

## 🚨 4. Exception Handling

Four key patterns demonstrated with practical real-world scenarios:

```python
# Pattern 1 — ZeroDivisionError
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Pattern 2 — ValueError on type conversion
try:
    value = int("abc")
except ValueError:
    print("Invalid input!")

# Pattern 3 — else block (runs only if no exception)
try:
    num = int(input("Enter a number: "))
except ValueError:
    print("Not a valid number!")
else:
    print(f"You entered: {num}")

# Pattern 4 — finally block (always runs) + FileNotFoundError
try:
    file = open("my_file.txt", "r")
except FileNotFoundError:
    print("File not found!")
finally:
    file.close()  # Always close resources
```

---

## 🐼 5. Pandas — SF Salaries Dataset

### Dataset at a Glance
```
Rows    : 148,654 employee records
Columns : Id, EmployeeName, JobTitle, BasePay, OvertimePay,
          OtherPay, Benefits, TotalPay, TotalPayBenefits,
          Year, Notes, Agency, Status
```

### Assignment Tasks Completed

**Task 1 — Min / Average / Max BasePay per Job Title**
```python
basepay_summary = df.groupby('JobTitle')['BasePay'].agg(
    Min_BasePay='min',
    Average_BasePay='mean',
    Max_BasePay='max'
).sort_values(by='Average_BasePay', ascending=False)
```

**Task 2 — Handle Duplicate Employee Names**
```python
# Average all numeric values for duplicate names, reassign new IDs
averaged_duplicates = duplicated_names.groupby('EmployeeName')[numeric_cols].mean().reset_index()
```

**Task 3 — Overtime Analysis**
```python
overtime_emps = df[df['OvertimePay'] > 0]
# → Count of overtime workers + total $ paid + top 5 job titles by overtime
```

**Task 4 — BasePay Growth Over Time**
```python
overall_change_pct = ((avg_latest - avg_earliest) / avg_earliest) * 100
# → Yes, BasePay increased — percentage change calculated year-over-year
```

### In-Class Assignments Also Solved

- Null value detection per column
- Row & column count (`df.shape`)
- **66th percentile** for every numeric column programmatically
- Unique job titles, years, agencies, employee names

---

## 🔢 6. NumPy — Array Operations

NumPy's `.values` property was used to bridge Pandas DataFrames with array-level operations:

```python
# Access DataFrame as NumPy array
df_kevin = df[df['EmployeeName'] == "KEVIN LEE"]

df_kevin.values[0]       # All values for first row
df_kevin.values[0, -5:]  # Last 5 values
df_kevin.values[0, :5]   # First 5 values
```

---

## 📐 7. SciPy — Descriptive Statistics

```python
import scipy.stats as stats

basepay_cleaned = df['BasePay'].dropna()
description = stats.describe(basepay_cleaned)
```

**Key findings for SF BasePay column:**

| Statistic | Value |
|-----------|-------|
| Observations | 148,654 |
| Mean | $66,325.44 |
| Std Deviation | $46,323.86 |
| Minimum | $0.00 |
| Maximum | $319,275.01 |
| Skewness | 1.55 (right-skewed) |
| Kurtosis | 2.21 |

---

## 🧮 8. Math Module

```python
import math

math.sqrt(81)       # → 9.00
math.log(100)       # → 4.61  (natural log)
```

---

## 🎨 9–11. Visualizations

### Seaborn Plots

```python
# Relational plot — BasePay vs OvertimePay
sns.relplot(data=df, x="BasePay", y="OvertimePay")

# Multi-dimensional scatter — tips dataset
sns.relplot(data=tips, x="total_bill", y="tip", hue="smoker", style="sex")

# Distribution plots
sns.displot(df, x="BasePay")                       # Histogram
sns.displot(tips, x="total_bill", kind="kde")      # KDE curve

# Line plot with FMRI data
sns.relplot(data=fmri, kind="line", x="timepoint", y="signal", hue="region")
```

### Plotly Interactive Plots

```python
# Basic scatter
fig = px.scatter(tips, x="total_bill", y="tip")

# Color by day
fig = px.scatter(tips, x="total_bill", y="tip", color="day")

# Color + size + symbol — 3 variables at once
fig = px.scatter(tips, x="total_bill", y="tip",
                 color="smoker", size="size", symbol="sex")
```

### Visualization Summary

| # | Chart | Dataset | Key Insight |
|---|-------|---------|-------------|
| 1 | Scatter — BasePay vs OvertimePay | SF Salaries | High earners tend to have lower overtime |
| 2 | Scatter — Total Bill vs Tip | tips | Strong positive correlation |
| 3 | Scatter — Colored by Day | tips | Weekend tips are higher |
| 4 | Scatter — Smoker + Size + Sex | tips | Smokers show wider tip variance |
| 5 | Line — fMRI Signal over Time | fmri | Frontal vs parietal region divergence |
| 6 | Histogram — BasePay | SF Salaries | Right-skewed; most employees earn $40K–$90K |
| 7 | KDE — Total Bill | tips | Bimodal distribution around $15 and $25 |
| 8 | KDE — BasePay | SF Salaries | Long tail toward $300K+ |

---

## 🧰 Tech Stack

```
Python 3.x
├── keyword         — Python reserved words
├── math            — Built-in mathematical functions
├── pandas          — Data loading, cleaning, groupby, aggregation
├── numpy           — Array operations and numerical computing
├── scipy.stats     — Descriptive statistics and distributions
├── matplotlib      — Core plotting engine
├── seaborn         — Statistical visualizations
└── plotly.express  — Interactive browser-based charts
```

## 📝 Key Takeaways

- **Python keywords** form the structural backbone of every program — understanding their scope rules is essential for clean code
- **Exception handling** is not optional — it is the difference between a program that crashes silently and one that communicates clearly
- **Pandas `groupby` + `agg`** is the workhorse of any salary or HR-style analysis
- **SciPy's `stats.describe()`** provides skewness and kurtosis in a single call — critical for understanding data shape before modeling
- **Plotly** transforms static charts into interactive, shareable, web-ready visuals with minimal extra code
- **Vectorized operations** (Pandas/NumPy) are consistently faster and more readable than equivalent Python loops

---

## 🌱 Future Scope

- [ ] Add predictive modeling for salary estimation (Linear Regression)
- [ ] Build an interactive Streamlit dashboard for the SF Salaries data
- [ ] Add Plotly Dash for live filtering by year, job title, and agency
- [ ] Extend SciPy usage — hypothesis testing (t-tests, ANOVA)
- [ ] Add a Plotly animated scatter showing BasePay change across years

