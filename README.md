# 📊 Sales and Profit Analysis Using Python

A complete data analytics project focused on uncovering trends and actionable insights from sales and profit data using Python. This project explores monthly/yearly sales performance, product profitability, customer segmentation, and more—aimed at helping businesses make data-driven decisions.

## 📁 Project Overview

This project answers key business questions like:
- Which months have the highest and lowest sales?
- Which product categories and sub-categories are most and least profitable?
- How does customer segmentation impact sales and profit?
- What seasonal trends can be leveraged for business growth?

---

## 🔧 Tools & Technologies Used

- **Python**
- **Pandas** – Data manipulation and preprocessing
- **Matplotlib / Seaborn / Plotly** – Data visualization
- **Jupyter Notebook** – Code development and analysis environment

---

## 🧹 Data Preparation Steps

- Checked for null values (✅ None found)
- Flagged outliers using the **IQR method**
- Converted date columns into `datetime` format
- Extracted `Month`, `Year`, and `Day of Week` for time-based analysis

---

## 📈 Key Insights

### 🔹 Sales Trends
- Sales **peaked in Q4**, suggesting seasonal buying behavior.
- **Continuous growth** observed year-over-year.

### 🔹 Category & Sub-Category Analysis
- **Technology** leads in sales; **Chairs** and **Paper** dominate sub-categories.
- **Copiers and Phones** showed highest profit margins.
- **Fasteners and Art** sub-categories underperform.

### 🔹 Profitability
- Profit fluctuated mid-year but recovered by year-end.
- **Office Supplies** and **Technology** were the most profitable categories.

### 🔹 Customer Segmentation
- High-value customer segments identified for **targeted marketing** and **sales strategies**.

---

## 🧠 Course of Action

- Increase stock and promotions in Q4.
- Promote high-margin products; reassess low performers.
- Target profitable customer segments with personalized offers.
- Automate reporting with Python scripts.

---

## 📂 Folder Structure

#Importing libraries to python 
import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objects as go
import plotly.io as pio
import plotly.colors as  colors
pio.templates.default = 'plotly_white'
import seaborn as sns


