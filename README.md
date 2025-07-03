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


 #Importing a CSV file into a pandas DataFrame for analysis.

df_esales= pd.read_csv("C:/Users/91854/Downloads/Sample - Superstore.csv", encoding='latin1')
#Exploring The Dataset
df_esales
df_esales.head()
df_esales.info()
#Generating descriptive statistics
df_esales.describe()
#Checking for the null values in the dataset
df_esales.isnull().sum()
df_esales.head()
# Outlier Detection Using IQR Method
Q1 = df_esales['Sales'].quantile(0.25)
Q3 = df_esales['Sales'].quantile(0.75)
IQR = Q3-Q1
Lowerbound= Q1 - 1.5*IQR
Upperbound= Q3 + 1.5*IQR
outlier_sales =df_esales[(df_esales['Sales']<Lowerbound) | (df_esales['Sales']>Upperbound)]
print(outlier_sales.shape[0])
# Since the no. of outliers is significantly more , I will flag the outliers instead of removing it.
df_esales['Outlier_Flag'] = df_esales['Sales'].apply(
    lambda x: 'Yes' if x < Lowerbound or x > Upperbound else 'No'
)

df_esales
df_esales.info()
#Converting Order Date and Ship Date to Datetime Format
df_esales['Order Date'] = pd.to_datetime(df_esales['Order Date'])
df_esales['Ship Date'] = pd.to_datetime(df_esales['Ship Date'])
df_esales.info()
df_esales.head()

#Creating Day Of Week,Month and Year Column for Further Analysis
df_esales['Order Month'] = df_esales['Order Date'].dt.month
df_esales['Order Year'] = df_esales['Order Date'].dt.year
df_esales['Order Day Of Week'] = df_esales['Order Date'].dt.dayofweek
df_esales
df_esales.head()
#Monthly Sale Analysis
Monthly_Sales = df_esales.groupby('Order Month')['Sales'].sum().reset_index()
Monthly_Sales
#Monthly Sales Analysis Using Line Chart
fig = px.line(Monthly_Sales,
             x = 'Order Month',
             y = 'Sales',
              color_discrete_sequence= px.colors.qualitative.Pastel,
             title= 'Monthly Sales Analysis')
fig.show()
#Yearly Sales Analysis
Yearly_sales =df_esales.groupby('Order Year')['Sales'].sum().reset_index()
Yearly_sales
#Yearly Sales Analysis Using Line Chart
fig2= px.line( Yearly_sales ,
             x = 'Order Year',
             y = 'Sales',
                            color_discrete_sequence= px.colors.qualitative.Pastel,

title= 'Yearly Sales Analysis')
fig2.show()
#Sales Analysis by Category
Sales_by_Category =df_esales.groupby('Category')['Sales'].sum().reset_index()

Sales_by_Category
#Sales Analysis by Category Using Pie-Chart
fig = px.pie(Sales_by_Category, 
             values='Sales', 
             names='Category',  
             color_discrete_sequence=px.colors.qualitative.Pastel)

fig.update_traces(textposition='inside', textinfo='percent+label')
fig.update_layout(title_text='Sales Analysis by Category', title_font=dict(size=24))

fig.show()
#Sales_by_Sub-Category
Sales_by_subcategory = df_esales.groupby('Sub-Category')['Sales'].sum().reset_index()
Sales_by_subcategory
#Sales Analysis By Sub- Category Using Bar Graph
fig4=px.bar(Sales_by_subcategory,
                x = 'Sub-Category',
                y='Sales',
                title= 'Sub-Category Sales Analysis',
                color_discrete_sequence=px.colors.qualitative.Pastel)
fig4.show()
#Monthly Profit 
Monthly_Profit=df_esales.groupby('Order Month')['Profit'].sum().reset_index()
Monthly_Profit
#Monthly Profit Analysis Using Line Chart
fig5= px.line(Monthly_Profit,
             x='Order Month',
             y='Profit',
title='Monthly Profit Analysis',
              color_discrete_sequence=px.colors.qualitative.Pastel)
fig5.show()
# Profit By Category
Profit_by_Category =df_esales.groupby('Category')['Profit'].sum().reset_index()
Profit_by_Category
# Profit Analysis By Category Using Donut Chart
fig6 = px.pie(Profit_by_Category,
             values='Profit',
             names = 'Category',
              hole = 0.7,
             color_discrete_sequence=px.colors.qualitative.Pastel)
fig6.update_traces( textposition='outside', textinfo='percent+label')
fig6.update_layout(title_text='Profit Analysis by Category', title_font =dict(size=24))
fig6.show()

#Profit By Sub-Category
Profit_by_SubCategory = df_esales.groupby('Sub-Category')['Profit'].sum().reset_index()
Profit_by_SubCategory
#Profit Analysis By Sub-Category
fig7 = px.bar(Profit_by_SubCategory,
             x='Sub-Category',
             y='Profit',
             title='Profit Analysis by Sub-Category',
             color_discrete_sequence=px.colors.qualitative.Pastel)
fig7.show()
df_esales
#Sales and Profit Analysis by Customer Segment
sales_profit_by_segment = df_esales.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()

color_palette = colors.qualitative.Pastel

fig = go.Figure()
fig.add_trace(go.Bar(x=sales_profit_by_segment['Segment'], 
                     y=sales_profit_by_segment['Sales'], 
                     name='Sales',
                     marker_color=color_palette[0]))

fig.add_trace(go.Bar(x=sales_profit_by_segment['Segment'], 
                     y=sales_profit_by_segment['Profit'], 
                     name='Profit',
                     marker_color=color_palette[1]))

fig.update_layout(title='Sales and Profit Analysis by Customer Segment',
                  xaxis_title='Customer Segment', yaxis_title='Amount')

fig.show()
