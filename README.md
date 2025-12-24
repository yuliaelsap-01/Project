# Portfolio

This repository contains various past projects, including Data Analyst (SQL, Python), Data Visualization, and IoT SMART Manufacturing

# [Project 1: E-Commerce Sales Analysis using MySQL]

## Table of Contents

- [Project Overview](#project-overview)
- [Recommendations](#recommendations)
- [Data Sources](#data-sources).

### Project Overview

This data analysis project utilized MySQL to evaluate data on e-commerce transactions from 2021 to 2022. The goal is to provide recommendations on marketing budget and business insights.

### Data Sources

- Order data: The primary dataset used for this analysis is the "order_detail.csv" file, containing detailed sales information.
- Payment data: The sub-dataset used for this analysis is the "payment_detail.csv" file, containing information about payment methods used in transactions.
- Customer data: The sub-dataset used for this analysis is the "customer_detail.csv" file, containing customer IDs and customer registration dates.
- SKU (Stock-Keeping Unit): The sub-dataset used for this analysis is the "sku_detail.csv" file, containing detailed product prices and cost details.

### Tools

- Excel - Data Cleaning
  [Order data](https://raw.githubusercontent.com/dataskillsboost/FinalProjectDA11/main/order_detail.csv)
  [Payment data](https://raw.githubusercontent.com/dataskillsboost/FinalProjectDA11/main/payment_detail.csv)
  [Customer data](https://raw.githubusercontent.com/dataskillsboost/FinalProjectDA11/main/customer_detail.csv)
  [SKU data](https://raw.githubusercontent.com/dataskillsboost/FinalProjectDA11/main/sku_detail.csv)
- MySQL - Data Analysis
- Looker - Creating reports

### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.
4. Making CTE for combining 4 datasets.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- Which month had the highest transaction volume in 2021?
- Which category had the highest transaction volume in 2022?
- How do transaction volumes by category compare between 2021 and 2022?
- What are the five most widely used payment methods?
- What is the ranking of categories based on transaction value?

### Data Analysis

Include some interesting code/features worked with

```sql
--table name with case_1, case_2, case_3, etc

SELECT * FROM case_1;
```

### Results/Findings

The analysis results are summarized as follows:
1. Overall, transaction trends have steadily increased from mid-year to the end of the year, with a noticeable surge starting in July 2021.
2. In August 2021, total transactions reached Rp 227,862,744.00, marking the peak of sales for that year.
3. The Mobiles & Tablets category ranked first as the category with the highest total transaction value in 2022, amounting to Rp 918,451,576.00.
4. The Others category declined by 46.27%, while the Books category decreased by 32.91%.
5. Cash on Delivery ranked as the most popular payment method.

### Recommendations

Based on the analysis, we recommend the following actions:
1. Optimize targeted marketing (ads) toward young professionals and students who require devices.
2. Plan inventory and SKUs based on sales trends by model and capacity to ensure product availability during peak demand.
3. Evaluate the performance and market trends of physical books.
4. Improve the user experience (UX) of e-wallet applications.

### Limitations

In the SKU_detail table, several iPhone, MacBook, and Mac Mini products in the sku_name column do not include the brand name “Apple,” which should be considered during data processing.
   


# [Project 2: E-Commerce data insights analysis using Python]

