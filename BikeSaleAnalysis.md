# Bike Sales Data Exploratory Analysis: Understanding Consumers  
### Author: Dylan Viyar
### Last Updated: 2023-09-28

This project was motivated by the final Excel case study in Alex Freberg's Data Analysis bootcamp. We want to understand more about what motivates people to purchase a bike.

# 1. Background Information

### 1.0 The Setting

In an effort to understand the bike industry and market, we can look at a dataset that contains information on bike consumers and determine if there are any underlying trends worth noting. We then can make marketing strategy suggestions to supplement sales growth.

### 1.1 Guiding Questions

1. What are some trends and patterns in bike consumers vs. non-consumers?
2. Are certain demographics or audiences more likely to purchase bikes?
3. How can understanding these trends influence marketing strategies for bike stores?


### 1.2 The Business Task

*Analyze bike consumer data to better understand the targeted audience and provide insightful marketing suggestions.*


# 2. The Data

### 2.0 Gathering the dataset

The data is made publicly available [here](https://github.com/AlexTheAnalyst/Excel-Tutorial/blob/main/Excel%20Project%20Dataset.xlsx)

### 2.1 A Quick Glance

When opening the Excel file, we can see the data looks like this:

  ![Uncleaned Preview BikeSales](https://github.com/dylanviyar/Excel-Projects/assets/81194849/4b99ddb2-2cec-4145-9ebf-f2a0c0d61cfb)

Key Takeaways:
- There are 13 columns and 1027 rows in our dataset
- Each row is a description of a person, with the final column distinguishing if they ended up purchasing a bike
- Each column contains different attributes of an individual, possibly certain attributes to motivate a bike purchase

### 2.2 Possible Limitations of the Dataset

1. We only have a limited amount of characteristics, we do not know if these are truly the most influencial aspects when deciding to purchase a bike
2. We are unaware of the collection method of the data, we do not know if there is bias in the data or data collection
3. We do not know if these trends that we discover are still relevant to the current audience

# 3. Data Preparation

### 3.1 Data Cleansing

*Note: Before manipulating our data, it is good convention to copy the raw data into another sheet, so we maintain a copy of the original data while we clean our data. Accordingly, all the following steps are done in a copy of the original dataset*

While getting our data ready for analysis,
some **Key Steps** include:
1. Removing duplicates
2. Checking for data type errors (inconsistent/mismatched data types)
3. Making the data more accessible
4. Ensuring the data stays relevant to the business task
5. Dealing with NULL or empty values

Using Conditional Formatting, I searched for duplicate IDS, as there is not supposed to be any duplicate values: 

![Duplicate IDS Bikesales](https://github.com/dylanviyar/Excel-Projects/assets/81194849/a11f3603-facd-44f6-b515-28793e00464f)

Here, we can see that despite the IDs being the same, the user information is different. This either means that the ID is not a unique identifier for the individual (unlikely) or there was an error in data collection. This is important to note. 

Regardless, completely duplicated rows are usually irrelevant in data analysis (as it is in our case) so we can use the "remove duplicates" in Excel to remove such values:

<img src ="https://github.com/dylanviyar/Excel-Projects/assets/81194849/39dc5740-1282-412f-8c7b-5f2ac4883129" width="400">

We can see that our sheet had 26 duplicate rows and Excel successfully removed those rows.

For the rest of the data cleansing we can go column by column and determine if the particular data in the column needs adjusting.

- ID: We want to ensure that all the values in this column are numbers, so using `=ISNUMBER(A2)` we can see that all the values in the ID column are in fact numbers and no further cleansing is necessary
- Martial Status/Gender: The "M" signifying "Married" and also signifying "Male" can be misleading during analysis and visualization. Using Find and Replace for each of the two rows, we can change the abbreviations to spell out the entire word to avoid confusion
- Income: We remove the decimal places to make the values easier to read
- Income Bracket: To allow for easier visualization for the income, we create a new column labeled `Income Bracket` to group the incomes in certain categories. We use the following nested IF: `=IF(D2>80000,"Greater than $80000",IF(D2>=30000,"Between $30000 and $80000",IF(D2<30000,"Less than $30000")))`
- Children: Using the same method as ID, we can attest that all the values are numbers
- Education, Occupation and Home Owners: Using the filter, we can see that all the values in the two columns are spelled correctly and no NULL or empty values, thus there is no need for any data manipulation 
- Cars: We can see that there are only numerical values, which is what we expect, so no further cleansing necessary
- Commute: When we hit filter, we see that `10+ Miles` value is listed second, which can we confusing in data visualization. Using Find and Replace, we can change `10+ Miles` to `More than 10 Miles` which gets placed last in the filter as desired
- Region: All values are spelled correctly, no further cleansing necessary
- Age: The age spread contains many values, making it difficult to notice trends, to deal with this, we can create a new column called `Age Group` to sort certain ages in a category. Ages 25-31 will be `Young Adult`, 31-65 will be `Adult` and 65+ will be `Old`. We can use a nested IF statement in another column to populate these values: `=IF(M2>65,"Old",IF(M2>31,"Adult",IF(M2<=31,"Young Adult")))`
- Purchased Bike: All values are either `Yes` or `No` as expected, no further manipulation necessary

After cleansing, our data looks like this:

![Cleaned BikeSales](https://github.com/dylanviyar/Excel-Projects/assets/81194849/c8717d85-1ecf-448b-95c9-647f816830fc)

Our data has been cleaned and now is ready for analysis.

# 4. Analysis

### 4.1 Pivot Tables

Some trends that we can use pivot tables to analyze include:
- Relationship between commute distance and bike purchases
- Relationship between Gender and income
- Relationship between Age Group and bike purchases
- Relationship between Income and bike purchases


Commute distance and Bike Purchases:

<img src="https://github.com/dylanviyar/Excel-Projects/assets/81194849/c7be0eb4-800b-45b9-a086-66214016cfc9" width="300">

Gender and Income: 

<img src="https://github.com/dylanviyar/Excel-Projects/assets/81194849/d1cf4611-459c-4be1-b27b-0b3e72dc0c3e" width="300">

Age Group and Bike Purchases:

<img src="https://github.com/dylanviyar/Excel-Projects/assets/81194849/9cf320e2-1e47-41cb-86d9-11f0488c6a22" width="300">

Income and Bike Purchases:

<img src="https://github.com/dylanviyar/Excel-Projects/assets/81194849/2e522c7f-2914-49bb-b6bd-a6a2b38da5b0" width ="300">

Some **Key Takeaways:**
- Men seem to be making more than women on average
- Adults (ages 31-65) are the most likely to be interested in bikes (regardless if they end up puchasing a bike or not)
- Commute and age seems to be most decisive attribute in regards to making the decision to buy a bike

# 5. Data Visualization

### 5.1 Dashboard

![Updated BikeSales Dashboard](https://github.com/dylanviyar/Excel-Projects/assets/81194849/df8c64c4-5ca7-4776-93be-dbc665ddb9e7)

*Note: We provide three additional slicers: Martial Status, Amount of Cars and Occupation, to provide more on-demand analysis*

### 5.2 Visualization Insights

1. Married individuals have an higher average income compared to their single counterparts
2. There is a spike in interest in bikes for adults and in people whose income is between $30000 and $80000
3. No one in the `Professional` occupation is making less than $30000
4. The lower the commute time, the more likely an individual is interested in purchasing a bike.

# 6. Moving Forward

### 6.0 Recall Guiding Questions

1. What are some trends and patterns in bike consumers vs. non-consumers?
2. Are certain demographics or audiences more likely to purchase bikes?
3. How can understanding these trends influence marketing strategies for bike stores?

### 6.1 Notable Trends

- Bike consumers tend to live closer to their work and are middle-aged
- Non-consumers are in the minority of the sample, people already interested in a bike are liely to puchase a unit
- Income seems to have no direct effect on whether or not an individual buys a bike, the trend lines follow the same pattern between a purchase or non-puchase

### 6.2 Target Audience for Bike Purchases

- From our data and visualization, the demographic most likely to purchase a bike is in the age group between 31 and 65 and works within a mile of their work
- Single people also had a higher amount of bike purchases

### 6.3 Data-Driven Marketing Suggestions

- Target the middle-aged! This age group clearly purchases the most bicycles. Targeted advertisements to this age group can support sales growth.
- Adjust bike pricing to consider the middle class. People earning between $30000 and $80000 are the most interested in buying a bike, however there is no evidence to show that they are in fact buying more bikes. Tailor the pricing of bicycles to make them affordable for people making this amount to hopefully turn their interest into purchases.
- Set up shop in between the workplace and the residential! People living close to their work bought the most amount of bikes, so placing stores that are located between a person's work and house could possibly motivate them to consider biking to work.





