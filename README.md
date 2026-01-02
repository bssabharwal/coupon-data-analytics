# coupon-data-analytics

Data Exploration
----------------
1. Dataset contains 12684 reows and 26 columns
2. Most of the columns are categorical. The numeric colums like temperature have fixed discrete values out of fixed set and not continuous range. All other numeric columns have a binary values of 0 or 1.
3. Calling describe() on the dataset does not provide any useful information for the numeric columns for the reason mentioned above in point 2.
4. Investigating the missing values shows that the Column "car" is missing values in 99% of the rows, while columns Bar, CoffeeHouse, CarryAway, ResturantLEssThan20, Resturant20To50 have very small number of missing values of around 1 to 1.7% of total rows. All other colums have no missing data.
5. Exploring column "age" shows the mix of numeric and string values with age above 50 as 50plus and below 21 as below21. The column will need data transformation to be used more effectively in the analysis
6. Exploring column "income" shows the distribution of dataset in range of incomes. The column will need data transformation to be used more effectively in the analysis
7. Exploring column "coupon" shows that the maximun coupons in the dataset are of CoffeeHouse followed by ResturantLEssThan20, CarryAway, Bar, Resturant20To50

Data Preparation
----------------
The following two activities are performed for data preparation

Handling Missing values
1. For column "Car", since 99% of the values are missing from the dataset, it does not make sense to populate the column with values using some strategy so the whole column is dropped from the dataset.
2. For the columns with small number of missing values either we can drop those rows but it will lead to information loss from other columns or we fill the missing values based on the probability distribution of the existing values so that the overall distribution of the data is maintained. For this assignment we decided to use probability distribution to fill the missing values.

Data Transformations
1. For the column "age", we need this column to be numeric so we need to convert the values in the column like 50plus and below21 to numeric values like 50plus to 50 and below21 to 20 using pandas string operations and converting the whole column datatype to integer
2. For the column "income", we need to convert the range to min and max values and creating two new columns in the dataset as Income_Min_Value and Income_Max_Value

Data Visualizations
-------------------
1. From the heatmap between coupon and destination, a strong corelation is observed between Destination as No Urgent Place and ResturantLEssThan20 and CoffeeHouse
2. From the heatmap between coupon and passanger, a strong corelation is observed between Alone and Carryout and CoffeeHouse copouns and somewhat strong corelation between Alone and ResturantLEssThan20. Also there was medium correlation between passangers as friends and ResturantLEssThan20 and CoffeeHouse coupons. 
3. From the heatmap between coupon and weather, a strong correlation is observed between Sunny weather and ResturantLEssThan20 and CoffeeHouse.
4. From the heatmap between coupon and time, a strong correlation is observed between ResturantLEssThan20 and time 2pm and 6pm and for CoffeeHouse 10am followed by medium corelation with 2pm and 6pm.
5. From the heatmap between coupon and marticalStatus and has_children, a strong correlation is observed between Single and CoffeeHouse followed by somewhat strong between Single and CarryAway and ResturantLEssThan20.
6. Strong relation is observed between Unemployed and Student with CoffeeHouse
7. Strong relation is observed between age 21-26 for CoffeeHouse, CarryAway and ResturantLEssThan20

Data Analysis for CoffeeHouse coupon
------------------------------------
1. The overall acceptance rate for coffee coupon is 49.92%
2. The acceptance rate increase if the drivers visit the coffee house 4 or more times in a month with 67% compared to 45% otherwise
3. The drivers are more likely to accept the coupon when driving to Home/Work when it is in the same direction compared to coupon in opposite direction with 53% to 31%
4. The distance to the coupon shows influence on the acceptance rate of the coupon with 5 min distance as 43%, 15 min as 45% and 25 min as 35%. Also the age impacts the acceptance rate for the coupon distance with drivers under the age of 30 having higher acceptance rate for the coupons with 5/15/25 min distance.
5. The time of the day also shows influence on the acceptance rate with the morning hours as 54% compared to 41% for evening hours. Also the destination impacts the acceptance rate in the morning hours when not driving to work is 64% compared to 44% when destination is work. Similarly the acceptance rate in the evening hours is 52% when not going to home compared to 36% when going to home.
6. The expiration of the coupon also impacts acceptance rate with drivers preferring longer duration coupon. The acceptance rate for 1d coupon is 58% compared to 43% for 2h coupon.
7 The five top most occuptance based on acceptance rate are Healthcare Practitioners & Technical, Building & Grounds Cleaning & Maintenance, Student, Transportation & Material Moving, Healthcare Support with acceptance rate above 60%


Hypothesis about drivers who accept CoffeeHouse coupons
-------------------------------------------------------
Based on the Data Visualizations and Data Analysis performed above, we can hypothesize that the drivers most likely to accept CoffeeHouse coupon will be the ones
- Who visit the CoffeeHouse at least once a month
- Who are not going to any urgent place
- With time of the day in morning or afternoon (10am,2pm)
- Have passengers as Friends or Partner
- With weather conditions as Sunny or Rainy
- Coupon has 1d validity
- And they work in following occupations - ['Healthcare Practitioners & Technical', 'Building & Grounds Cleaning & Maintenance', 'Student', 'Transportation & Material Moving', 'Healthcare Support', 'Installation Maintenance & Repair', 'Architecture & Engineering', 'Farming Fishing & Forestry', 'Unemployed', 'Arts Design Entertainment Sports & Media', 'Computer & Mathematical', 'Personal Care & Service']

When we combine all these conditions we see the acceptance rate of the CoffeeHouse coupon goes up to 91%.