# Python Project on Sales & Profit Analysis
A Comprehensive Analysis of Sales Performance, Profitability, Market Trends, and Regional Insights


## Overview
This project conducts an in-depth analysis of sales performance, profitability, market dynamics, and regional trends in international markets. By examining key metrics and patterns across global regions, the study aims to uncover actionable insights that can drive strategic decision-making and business growth.

The dataset used for this project was sourced from Qamar Mehmood's python project, which includes order details, shipping details, customer details, product details, costs, etc. I have used this dataset to build this project and enchance my skills.

## QUESTIONS EXPLORED
The question I have explored in the project are given below:

1. What are the year-over-year trends in sales and profit growth?
2. Which regions and markets have generated the highest sales & highest profits in international markets?
3. What are the top cities by profit?
4. What are the products with most sales?
5. What are the sales and profit figures across different international markets?

## Data Preparation and Cleanup:

This step involves data preparation, including importing libraries, loading the dataset, and performing essential cleanup to ensure the data is ready for analysis.

### Import Libraries and dataset
I started wwith loading neccesary libraries and dataset.

```python
import pandas as pd
from datasets import load_dataset
import matplotlib.pyplot as plt 
import ast
import seaborn as sns
import matplotlib.ticker

#loading dataset
data = pd.read_csv("C:/Users/gnikh/Downloads/Super_International_Market.csv", encoding='latin1')

#cleanup (transforming date column)
df1['Order Date'] = pd.to_datetime(df1['Order Date'], format='mixed').dt.strftime('%d-%m-%Y')
df1['Ship Date'] = pd.to_datetime(df1['Ship Date'], format='mixed').dt.strftime('%d-%m-%Y')

df1['Order Date'] = pd.to_datetime(df1['Order Date'])
df1['Ship Date'] = pd.to_datetime(df1['Ship Date'])

#dropping unwanted column:
df1 = df1.drop(columns='Postal Code')

#Assigning correct data types:
df1[['Ship Mode', 'Segment', 'Country',
       'Market', 'Region', 'Category', 'Sub-Category', 'Order Priority']] = df1[['Ship Mode', 'Segment', 'Country',
       'Market', 'Region', 'Category', 'Sub-Category', 'Order Priority']].astype('category')
```

## ANALYSIS:

I approached each question using Jupyter Notebooks, performing data cleaning, EDA, and visualizations to provide meaningful insights and support data-driven conclusions.

### 1. What are the year-over-year trends in sales and profit growth?
This analysis focuses on evaluating the sales and profit trends over the years across international markets. By examining year-over-year changes, the goal is to uncover growth patterns and provide insights into the financial performance and market dynamics of global regions.

Check out my notebook for detailed steps: 
[YoY_&_Top_markets](project.ipynb)

#### Visualising 

```python
sales_trend.plot(kind='line', linewidth=2, marker='o')

plt.title('Sales and Profit Trend Chart', fontsize=16, fontweight='bold', color='#600818')
plt.ylabel('Amount($)', fontsize=10, fontweight='bold', color='#600818')
plt.xlabel('Year', fontsize=10, fontweight='bold', color='#600818')
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${x/1000000}M'))
sns.despine()

```

#### Results
![Sales & profit chart](images\sales_profit_trend.png)

#### Insights

1. Consistent Growth in Sales and Profit:

From 2011 to 2014, both sales and profit have shown steady year-over-year growth, indicating a strong and stable upward business trajectory in international markets.

2. Sales Increased by Over 80%:

Sales grew from approximately $2.3M in 2011 to over $4.2M in 2014, marking an increase of more than 80% over four years.

3. Profit More Than Doubled:

Profit rose from around $0.5M in 2011 to over $1.0M in 2014, demonstrating a 100%+ increase, which suggests improved efficiency and profitability alongside growing revenue.

4. Widening Gap Between Sales and Profit:

Although both metrics are growing, the gap between sales and profit is widening slightly, indicating potential areas to improve profit margins or control operational 

### 2. Which regions and markets have generated the highest sales & highest profits in international markets?
This analysis highlights the top 5 regions and markets by the highest sales and by the highest profits in international markets. A stacked bar chart was used to visualize profit over sales, offering a clear comparison of financial performance across key areas.

Check out my notebook for detailed steps: 
[YoY_&_Top_markets](project.ipynb)

#### Visualising 

```python
fig, ax = plt.subplots(2, 1, figsize=(8, 8))

top_region_sales.plot(kind='bar', stacked=True, ax=ax[0])
ax[0].yaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${x/1000000}M'))
ax[0].set_title('Top Region & Markets by Most Sales', fontsize=16, fontweight='bold', color='#600818')
ax[0].set_ylabel('Amount($)', fontsize=10, fontweight='bold', color='#600818')
ax[0].set_xlabel('Region, Market', fontsize=10, fontweight='bold', color='#600818')
ax[0].tick_params('x', rotation=45)
sns.despine()

top_market_profit.plot(kind='bar', stacked=True, ax=ax[1])
ax[1].yaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${x/1000000}M'))
ax[1].set_title('Top Region & Markets by Most Profit', fontsize=16, fontweight='bold', color='#600818')
ax[1].set_ylabel('Amount($)', fontsize=10, fontweight='bold', color='#600818')
ax[1].set_xlabel('Region, Market', fontsize=10, fontweight='bold', color='#600818')
ax[1].tick_params('x', rotation=45)

plt.tight_layout()
```

#### Results
![Top 5 Regions by sales & profit](images\Top_regions_by_sales_profit.png)

#### Insights 

1. **Central Europe Leads in Both Sales and Profit:**
   The **Central European market** (Central, EU) stands out as the top performer in both total sales and profit, indicating its dominant role and strong return on sales in international markets.

2. **Disparity Between Sales and Profit Leaders:**
   Some markets like **North Asia (APAC)** and **EMEA (EMEA)** appear in the top 5 for sales but not for profit, suggesting lower profitability or higher costs in those regions.

3. **Emerging Markets Show High Profitability:**
   Regions such as **Africa (Africa)** and **EMEA (EMEA)** rank among the top 5 for profit, even though they don't lead in sales—highlighting their efficiency and high margins despite lower revenue volumes.

4. **Oceania (APAC) Shows Balanced Performance:**
   The **Oceania** market consistently appears in both charts, showing strong, balanced performance with relatively high sales and healthy profit, making it a well-rounded contributor.

### 3. What are the top 5 cities by profit?
This analysis focuses on identifying the top five cities that generate the highest profits across international markets. By evaluating profit margins and overall revenue contributions from various global cities, the goal is to uncover geographic trends in market performance, providing insights into where business operations are most financially successful.

Check out my notebook for detailed steps: 
[Top_cities_products](project(1.2).ipynb)

#### Visualising 

```python
city_state_profit.plot(kind='bar', x='City', y='Profit', ax=ax)

ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
plt.title('Top Cities by Profit', fontsize=16, fontweight='bold', color='#600818')
plt.ylabel('Profit', fontsize=10, fontweight='bold', color='#600818')
plt.xlabel('City', fontsize=10, fontweight='bold', color='#600818')
ax.tick_params('x', rotation=45)
ax.get_legend().remove()
sns.despine()
```

#### Results
![Top_cities_by_profit](images\top_ctites.png)

#### Insights

1. **New York City dominates in profitability**, generating nearly double the profit of the second-highest city, Los Angeles. This suggests a highly lucrative market environment and potentially more mature business infrastructure.

2. **U.S. cities occupy the top three positions** (New York City, Los Angeles, and Seattle), highlighting the strong financial performance of North American markets in comparison to their international counterparts.

3. **Asian cities like Manila and Jakarta are emerging profit centers**, contributing significantly despite being in developing economies. This indicates potential for future growth and investment opportunities in these regions.

4. **The profit distribution shows a steep drop after New York City**, emphasizing a concentrated profit trend where one city contributes disproportionately to overall performance. This may point to risks related to over-reliance on a single geographic market.

### 4. What are the products with most sales?
This analysis focuses on identifying the top five products with the highest sales across international markets. By visualizing their share in total sales using a pie chart, it offers a clear perspective on which products are driving the most revenue, supporting better product strategy and inventory decisions.

Check out my notebook for detailed steps: 
[Top_cities_products](project(1.2).ipynb)

#### Visualising 

```python
fig, ax = plt.subplots(figsize=(10,6))

ax.pie(top_products['Quantity'], labels=top_products['Product Name'], autopct='%1.1f%%', startangle=90)
ax.set_title('Products with Most Quantity Sold', fontsize=18, fontweight='bold', color='#600818')
```

#### Results
![Top_products_by_sales](images\top_products.png)

#### Insights

1. **Staples is the clear market leader**, accounting for over 42% of total sales volume among the top five products—more than double that of any other item. This suggests it is a core product driving overall performance.

2. **Sales are significantly skewed**, with Staples alone contributing nearly as much as the other four products combined. This concentration may warrant a deeper analysis of customer demand and supply chain priorities for this product.

3. **The remaining four products have a relatively even distribution**, each capturing between 12% and 16% of total sales, indicating a competitive secondary tier of high-performing items.

4. **Diversification opportunities may exist**, as heavy reliance on a single product could pose risks. Encouraging sales of other high-volume items might help balance the product portfolio.

### 5. What are the sales and profit figures across different international markets?
This analysis examines sales and profit figures across various international markets to evaluate regional performance. By comparing revenue generation and profitability, it aims to identify high-performing markets, uncover growth opportunities, and support strategic decision-making for global expansion.

Check out my notebook for detailed steps: 
[Sales_&_profit_market](project(1.2).ipynb)

#### Visualising 

```python
market_sprofit = df2.groupby('Market')[['Sales', 'Profit']].sum().reset_index()

fig, ax = plt.subplots(figsize=(10,6))

market_sprofit.set_index('Market').plot(kind='bar', stacked=True, ax=ax)
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${x/1000000}M'))
ax.set_title('Sales & Profits by Markets', fontsize=20, fontweight='bold', color='#600818')
ax.set_ylabel('Amount', fontsize=14, fontweight='bold', color='#600818')
ax.set_xlabel('Market', fontsize=14, fontweight='bold', color='#600818')

plt.tight_layout()
```

#### Results
![Sales & Profit by market](images\Sales_profit_market.png)

#### Insights

1. **APAC leads in overall performance**, generating the highest combined sales and profit figures, indicating it is the most lucrative market among all regions analyzed.

2. **EU and US markets also show strong profitability**, with both regions demonstrating a healthy balance between high sales and solid profit margins—suggesting mature and stable operations.

3. **Canada lags significantly behind**, with minimal sales and negligible profit contribution, highlighting it as a potential area for strategic reassessment or market exit consideration.

4. **Africa and EMEA show similar profiles**, with moderate sales and lower profit, suggesting possible growth markets that may require investment or operational optimization to improve returns.

## TOOLS USED:

### **Tools Used**  

- **Python** – The core programming language for data analysis and manipulation.  

 **LIBRARIES** 

 *Pandas* – Used for data cleaning, transformation, and analysis.  
*Matplotlib* – Employed for creating detailed and customizable visualizations.  
 *Seaborn* – Utilized for advanced statistical and aesthetically appealing data visualizations.  
- **Jupyter Notebooks** – The tool I used for writing, testing, and visualizing Python code.  
- **VS Code** – Software I used for writing and running python scripts.  
- **GitHub** – Used for version control and sharing project code.  


Here’s a professional and concise conclusion for your project:

## **Conclusion:**

This project analyzes different markets and regions across the globe, focusing on key performance indicators such as profits, sales, and top-selling products. By examining geographic trends and product-level performance, it provides deeper insights into which areas and offerings drive the most business value. These findings support data-driven decisions for strategic planning, resource allocation, and future market expansion.
