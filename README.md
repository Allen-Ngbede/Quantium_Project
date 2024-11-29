# Chips Customer Insights and Sales Analysis

## Overview
This project focuses on analyzing customer purchasing behaviors and sales trends for the chips category. By leveraging transaction and customer data, the goal is to uncover actionable insights that can inform the supermarket’s strategic plans for the next half-year.

The analysis aims to identify sales trends, understand the impact of various factors like pack size and brand preferences, and segment customers based on their spending habits. The findings will guide targeted marketing strategies and improve the overall performance of the chips category.

All credit for the dataset goes to the original creator, and I extend my gratitude to Quantium for making it accessible for analysis.

## Background
The analysis focuses on answering the following questions:

1. **What is the trend of transactions over time?**
2. **What is the trend of transactions in December only?**
3. **Does the size of the pack influence sales?**
4. **What are the top 5 purchased brands?**
5. **What are the top 10 most purchased products?**
6. **Who spends the most on chips, describing their lifestage and premium segments?**
7. **Who are the top 5 customers that purchase chips the most?**
8. **What is the average chip price by customer segment?**
9. **What are the most purchased brands by Mainstream - Young Singles/Couples?**
10. **What is the most preferred pack size by Mainstream - Young Singles/Couples?**

These questions form the core objectives of the analysis and are designed to uncover both broad and specific insights into customer purchasing behavior.

## Tools Used
- **Python**: For data cleaning, transformation, and analysis.
- **Pandas and NumPy**: For data manipulation and numerical computations.
- **Matplotlib and Seaborn**: For data visualization.
- **Jupyter Notebook**: As the primary environment for coding and documenting the analysis.
- **Excel/CSV Files**: For saving processed datasets and sharing insights.

## Methodology and Process
1. **Data Cleaning and Preparation**:
   - Examined transaction and customer datasets for inconsistencies, missing values, and outliers.
   - Corrected anomalies, such as duplicate entries or invalid data points.
   - Ensured that all numeric and date fields were correctly formatted and categorical fields were consistent.

2. **Data Merging**:
   - Merged transaction data with customer data to create a unified dataset for analysis.

3. **Analysis**:
   - **Sales Trends**: Explored transaction trends over time and focused specifically on December sales.
   - **Impact of Pack Size**: Analyzed sales distribution across various pack sizes.
   - **Top Brands and Products**: Identified the most purchased brands and products.
   - **Customer Segmentation**:
     - Segmented customers by lifestage and premium segments.
     - Examined spending habits, average chip prices, and preferences for pack size and brand.
   - **High-Spending Customers**: Highlighted top customers based on total chip purchases.

4. **Visualization**:
   - Created charts and graphs to illustrate trends, comparisons, and customer segments.

5. **Insights and Recommendations**:
   - Summarized findings and proposed strategies to enhance sales and target key customer segments.

## Challenges Faced
- **Data Quality Issues**:
  - Encountered missing and inconsistent data entries.
  - Addressed these issues by applying imputation techniques and filtering invalid data.

- **Complex Merging of Datasets**:
  - Merging transaction and customer data required careful handling of mismatched records and duplicates.

- **Handling Outliers**:
  - Significant outliers in sales data needed to be identified and either corrected or excluded from analysis to avoid skewing results.

- **Segment-Specific Analysis**:
  - Segmenting data by lifestage, premium tiers, and preferences required creating derived metrics and ensuring accurate classification.

- **Visualization Clarity**:
  - Balancing the need for detailed insights with the simplicity of visual representation posed a challenge in designing effective charts.


## Analysis

### 1. What is the trend of transactions over time?
### Methodology
To analyze the trend of transactions over time, a comprehensive approach was taken. A complete date range from July 1, 2018, to June 30, 2019, was established, and a DataFrame was created to hold this range. The transaction data was grouped by date to calculate the number of transactions per day. This grouped data was then merged with the full date range to ensure all dates were included in the final dataset. Missing transaction counts were filled with 0 to account for days with no transactions. Finally, the dataset was filtered to identify and list dates with zero transactions, enabling further investigation or reporting of potentially inactive periods. This approach provided a complete view of transaction trends over the specified period.

View my notebook with detailed steps here: [EDA_Quantium_Store.ipynb](EDA_Quantium_Store.ipynb])


### Visualize Data
```py
# Plot transaction over time
plt.figure(figsize=(10, 6))
sns.lineplot(data=merged_data, x='DATE', y='TRANSACTION_COUNT', color='blue')

# Set plot titles and labels
plt.title('Number of Transactions Over Time', fontsize=14, fontweight='bold')
plt.xlabel('Date', fontsize=12)
plt.ylabel('Number of Transactions', fontsize=12)

# Rotate x-axis labels for better readability
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

### Results
#### Visualization of trend of transaction over time
![image](images/transaction_trend.png)

### Insights
- Pre-Christmas Surge: The sharp peak in November/December shows a significant increase in transactions, likely driven by holiday shopping.
- Magnitude of the Spike: The December peak far exceeds typical transaction volumes, highlighting the importance of the holiday season and the need for robust operational planning.
- Revenue Opportunity: The December surge likely translates to a major revenue boost. Preparing inventory and optimizing operations during this period can drive significant financial gains.
- Overall Growth: Aside from seasonal variations, the data shows a consistent upward trend in transaction volumes, indicating overall business growth and an expanding customer base.

### 2. What is the trend of transactions in December only?
### Methodology
I focused on analyzing transaction data specifically for December 2018. I filtered the dataset to isolate entries for this month and year. To visualize the trends, I created a line plot that displayed the number of transactions over time, highlighting the fluctuations throughout December. The plot was customized with clear labels and a bold title to ensure readability, and I adjusted the x-axis labels for better clarity. This approach allowed me to effectively highlight and interpret the transaction trends during that month.

### Visualize Data
```py
# Filter the data to only include December 2018
december_data = merged_data[(merged_data['DATE'].dt.month == 12) & (merged_data['DATE'].dt.year == 2018)]

# Plot the number of transactions in December
plt.figure(figsize=(9, 6))
sns.lineplot(data=december_data, x='DATE', y='TRANSACTION_COUNT', marker='o', color='blue')

# Set plot titles and labels
plt.title('Number of Transactions in December 2018', fontsize=14, fontweight='bold')
plt.xlabel('Date', fontsize=12)
plt.ylabel('Number of Transactions', fontsize=12)

# Rotate x-axis labels for better readability
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```
### Results
#### Visualization of trend of transaction in December
![image](images/december_trans.png)

### Insights
- Overall Increase in Transactions: Throughout December, there is a noticeable upward trend in the number of transactions, peaking towards the end of the month. This suggests a growing level of customer activity as the holiday season progresses.
- Sharp Dip Around December 25th: A significant drop in transaction volume is observed around December 25th. This could be due to reduced business activity on Christmas Day, where many businesses are closed or customers are less likely to shop.
- Post-Christmas Recovery: After the dip on Christmas Day, the number of transactions rebounds, returning to levels similar to those seen in the earlier part of December. This could indicate a resurgence in post-holiday shopping, including post-Christmas sales or last-minute purchases.
- Peak Transaction Period: The highest volume of transactions occurs just before Christmas, around December 21st–22nd, indicating a pre-Christmas shopping rush. This peak aligns with customer preparations for the holiday, highlighting the importance of this period for retail or service-based businesses.


### 3. Does the size of the pack influence sales?

Methodology
I extracted the pack size from the PROD_NAME column by identifying and extracting the first numeric value within each product name. This was achieved using a regular expression to capture the number, which typically represents the pack size. A new column, PACK_SIZE, was created and used to analyze the distribution of transactions based on pack size. The distribution was visualized using a count plot, highlighting the number of transactions for each unique pack size.

### Visualize Data

```py
# Plot size pack over sales
plt.figure(figsize=(10, 6))
sns.countplot(data=transaction_data, x='PACK_SIZE', palette='dark:b', hue='PACK_SIZE', legend = False)

plt.title('Number of Transactions by Pack Size', fontsize=14, fontweight='bold')
plt.xlabel('Pack Size', fontsize=12)
plt.ylabel('Number of Transactions', fontsize=12)

plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```
### Results
#### Visualization of trend of transaction in December
![image](images/trans_by_pack_size.png)

### Insights
- Dominant Pack Size: The 170g pack size is the clear leader in terms of transaction volume, indicating strong customer preference. This highlights the importance of focusing production and inventory management on this pack size to meet demand and ensure product availability.
- Demand for Larger Packs: Transaction activity for larger pack sizes, such as 160g, 165g, and 175g, also showed significant levels of engagement. This suggests a clear demand for bulk or family-sized products. Adjusting pricing strategies and exploring promotional opportunities for these larger sizes could help drive further sales growth.
- Underperformance of Smaller Packs: Smaller pack sizes, ranging from 70g to 135g, showed much lower transaction volumes compared to their larger counterparts. This underperformance indicates that these sizes may not be as appealing to customers. A review of these smaller pack offerings could help optimize the product mix, potentially phasing out underperforming sizes or adjusting their market positioning.




What are the top 5 purchased brands?

What are the top 10 most purchased products?

Who spends the most on chips, describing their lifestage and premium segments?

Who are the top 5 customers that purchase chips the most?

What is the average chip price by customer segment?

What are the most purchased brands by Mainstream - Young Singles/Couples?

What is the most preferred pack size by Mainstream - Young Singles/Couples?



