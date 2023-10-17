# Data Analyst Associate Practical Exam Submission: Pet Supplies

# Introduction

## 1.1 Background
PetMind is a retailer of products for pets. They are based in the United States. PetMind sells products that are a mix of luxury items and everyday items. Luxury items include toys. Everyday items include food.
The company wants to increase sales by selling more everyday products repeatedly. They have been testing this approach for the last year. They now want a report on how repeat purchases impact sales.


## 1.2 Dataset
The dataset contains the sales records in the stores last year. The original dataset can be found [here](https://s3.amazonaws.com/talent-assets.datacamp.com/pet_supplies_2212.csv).

**Tool Used for the Analysis**: Microsoft Power BI

# Data Cleaning

## 2.1 Data Overview

### 2.1.1 Data Structure

![Data Structure](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Data_Structure.png)

The dataset has a long format with 1500 rows and 8 columns.

### 2.1.2 Data Types

![Data Types](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Data_Types.png)

The dataset contains 2 columns of integer data type, 5 columns of text data type and 1 column of decimal number data type, as shown in the table below:
| Column Name | Data Type |
| -------- | -------- |
| product_id | integer |
| category | text |
| animal | text |
| size | text |
| price | text |
| sales | decimal number |
| rating | text |
| repeat_purchase | integer |

### 2.1.3 Duplicates and Missing Values

![Duplicates and Missing Values](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Duplicates_and_Missing_Values.png)

From the overview above, it is clear that there are no duplicate values (products) in the dataset. A quick check of the column profiles showed that there are several columns that should have missing values but have initial values that are not appropriate, such as:
| Column Name | Initial Value | Count |
| -------- | -------- | -------- |
| category | - | 25 |
| price | unlisted | 150 |
| rating | NA | 150 |


## 2.2 Data Issues

The quality issues found with the dataset include:
- Inconsistent variable cases in `size`.
- Wrong data types in `rating` and `price`.
- Missing values in `category`, `price` and `rating`.

These data quality issues were fixed following the [Exam Instructions](https://s3.amazonaws.com/talent-assets.datacamp.com/Practical+-+DAA+-+Pet+Supplies+-+2212.pdf).

### 2.2.1 Inconsistent Variable Cases in `size`
Values in this column were changed to title case.

### 2.2.2 Wrong Data Types in `rating` and `price`
Values in `rating` were converted to whole number while those in `price` were converted to decimal number.

### 2.2.3 Missing Values in `category`, `price` and `rating`
- Missing values in `category` were replaced with 'Unknown'.
- Missing values in `price` were initially replaced with null values (that is, no values were imputed) and, after changing the data type, replaced with the overall median price of 28.06.
- Missing values in `rating` were replaced with 0.

Here is what the cleaned dataset looks like:

![Cleaned Dataset](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Cleaned_Dataset.png)

# Tasks

## Task 1

For every column in the data:
- State whether the values match the description given in the table above.
- State the number of missing values in the column.
- Describe what you did to make values match the description if they did not match.

*Solution*

**product_id**: There were 1500 unique values in this column. There were neither duplicates nor missing values in this column, which is expected since this is a unique identifier. No changes were made to this column.

**category**: This column had 7 unique values. All of the values were one of the six stated categories with the exception of the value '-' which is seen as a missing value. These missing values, totaling 25 rows, were replaced with 'Unknown'.

**animal**: There were 4 unique values which matched the four given in the data dictionary. There were no missing values and no changes were made to this column.

**size**: There were no missing values but the entries in this column were restructured into title case for uniformity and to suit the description given for 3 unique sizes.

**price**: The price column had 150 values as 'unlisted', which are seen as missing values. The values ranged from 12.85 to 54.16. The data type was changed to decimal number and these values were replaced with the overall median price of 28.06. The values of this column were rounded to two decimal places.
 
**sales**: This column contained only positive values rounded to two decimal places. There were no missing values and all values ranged from 286.94 to 2255.96.

**rating**: The values of this column were between 1 and 10, which is consistent with the description given. There were 150 missing values which were replaced with 0 as per the data description.

**repeat_purchase**: All values in the repeat_purchase column were either 0 or 1, as expected. There were no missing values, hence no changes were made to this column.

## Task 2

Create a visualization that shows how many products are repeat purchases. Use the visualization to:
- State which category of the variable repeat purchases has the most observations.
- Explain whether the observations are balanced across categories of the variable repeat purchases.

*Solution*

Since PetMind is focused on the impact of repeat purchases, it is important to establish how many products currently have repeat purchases. Below, we can see that the difference between repeat purchases and one-off purchases is as much as 312 purchases, with repeat purchases accounting for 60.4% of products.

![Comparison of Repeat Purchases to One-off Purchases](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Comparison_of_Repeat_Purchases_to_One_off_Purchases.png)

_There were more repeat purchases made which had over 800 observations._

This suggests that the company already sells a large amount of its products repeatedly, but it does not give insight into the categories these products fall under or how they affect sales. Let's further explore how these repeat purchases are spread across the categories.

**How Many Products are Repeat Purchases in Each Category?**

![Repeat Purchases by Product Category](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Repeat_Purchases_by_Product_Category.png)

_The observations of repeat purchases by category are not evenly distributed. Equipment has the most repeat purchases followed by Medicine,  Housing, Food, and Toys. The Unkown category is the least purchased._

The Equipment category has the highest number of repeat purchases, suggesting that customers are satisfied with the quality and usefulness of these products. The Medicine, Housing and Food categories also have relatively high number of repeat purchases, indicating customer loyalty to PetMind for their pet needs. The Toys category has a similar number of repeat purchases, while the Accessory category has a lower number. However, when compared as a whole, the Equipment and Accessory categories differ significantly.

**Are the Observations Balanced Across the Categories of Repeat Purchases?**

It is clear to see that the observations are not balanced across the categories, with Equipment having the most repeat purchases at 221 and Unknown having the lowest at 14, indicating that certain categories have a higher frequency of repeat purchases than others. It is important to know that this imbalance is independent of the Unknown category's composition and would not change even if the products in this category were reclassified.
Understanding which specific equipment products are being resold will give PetMind a clearer picture of the daily needs of their customers.

## Task 3

Describe the distribution of all of the sales. Your answer must include a visualization that shows the distribution. 

*Solution*

Since the company wants to increase sales by selling more everyday products repeatedly, we need to look at how the number of sales is distributed. This gives an idea of how often items were purchased throughout the year.

![Sales Distribution](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Sales_Distribution.png)

_The median value for the sales is 1,000.83 which means that most products were sold about 1,000 times._

Looking at the graph, the distribution is mesokurtic with a high peak around the 943.28 to 1074.54 bin. There also seems to be a number of sales that are outliers, with values much higher than the rest of the data. This may indicate that certain products or events (such as species, price, or category) had a significant impact on sales during those periods. 
I would suggest to further investigate which products fall in this outlier section and whether they should be included in future analyses.
 
From previous analysis, we have seen that products in the Equipment category are repeatedly purchased. We can split the sales by animal species to get a clearer picture of what type of pet owners the company caters to most.

![Sales by Animal and Category](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Sales_by_Animal_and_Category.png)

_At PetMind, cat items are the most frequently bought items._

The graph shows that cat products are very popular. This suggests that the company offers high quality cat products that cat owners prefer above other companies. This can be an area for the marketing team to look at.
However, given the limitations of our data, it is still unclear whether or not this outcome is due to cats being more accessible to products than other animals. It is necessary to point out that a large number of transactions in one category or animal species does not guarantee a high volume of overall sales.
Each animal has a distinct market under each category, with cats falling under the category of Equipment and Toys, dogs under Food, cats and fish under Medicine, birds under Accessory, and cats, dogs and fish in Housing.

## Task 4

Describe the relationship between repeat purchases and sales. Your answer must include a visualization to demonstrate the relationship.

*Solution*

Since the company is interested in how repeat purchases affect sales, it makes more sense to look at the sales distribution between one-off and repeat purchases.

![Repeat Purchases vs Sales](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Repeat_Purchases_vs_Sales.png)

_The minimum sales was about 250 and the maximum was about 1750 with few outliers outside the maximum value. The median sales was about 1000._

In the plot above, we can see that the median for both categories is close together, and the interquartile ranges are fairly similar. This suggests that repeat purchases don't have a strong influence over sales compared to one-off purchases, even though, as presented in our first graph, there are more repeat purchase products than one-off purchase products. This could be due to lower prices for the repeat purchase products.

Lastly, we look at how the sales are affected by price.

![Sales vs Average Price by Animal](https://github.com/adeolaosibajo/datacamp-associate-certification/blob/098facc1a26a91a2e903000f4a5e7e2730b933fb/assets/Sales_vs_Average_Price_by_Animal.png)

_At PetMind, bird products are the most expensive items._

Disregarding the straight line of bubbles at 28.06, which is our median price used to fill in missing values, we can see that the species actually drive the increase in sales and not the price. This also shows that fish products tend to have lower prices compared to birds and that most dog and cat product prices fall in the middle. It is easy to see that across all the categories, cat items are not pricey making it easy for pet owners to purchase them repeatedly, leading to the high sales frequency earlier uncovered.

# Conclusion

Based on the information above, repeat purchases do not affect product sales in a significant way. Identifying which items were repeat purchases would give a more accurate idea of why this is so. Analysis should continue with other variables affecting sales to identify optimal adjustments for increased revenue.
However, based on the information we have, it makes sense that everyday items like food and equipment is only repurchased a certain number of times in a year. Animals tend to eat a number of portions a day and that number rarely increases once an animal reaches adulthood. I would recommend that PetMind focus on using their popular items to attract more pet owners in order to increase sales. Attracting pet owners with younger pets might increase repeat purchases, on things like food, for the first couple years of the pet's life.