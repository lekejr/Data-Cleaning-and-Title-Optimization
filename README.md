# DATA CLEANING AND TITLE OPTIMIZATION

## Introduction
The data cleaning and preparation procedure carried out on the supplied Product Data dataset is documented in this report. The goal was to improve the quality of the data by solving problems which include duplicate records, missing values and inconsistent formatting.
For better readability and SEO (Search Engine Optimization), a `SHORT_TITLE` function was created to enhance the product titles. 

## Data Overview
![image](https://github.com/user-attachments/assets/a091bb34-1c2e-4161-83d1-d9583fada02d)

The raw dataset consists of **3847 rows** and **6 columns**, which initially had missing values and inconsistencies. Key columns include:

- `PRODUCT_ID`
- `Title`
- `BULLET_POINTS`
- `Description`
- `PRODUCT_TYPE_ID`
- `PRODUCT_LENGTH`

## Data Cleaning Optimization

### Handling Missing Values
![image](https://github.com/user-attachments/assets/d0aef64d-022a-4b7d-84b2-bfc6a0af1839)

The dataset was inspected for inconsistencies, missing values and inaccuracies. The following issues were identified and addressed:

- **BULLET_POINTS**: Originally had 37% missing values. These were replaced with "N/A" for consistency.
- **Description**: Contained null values, which were replaced with "None".
- **PRODUCT_TYPE_ID** and **PRODUCT_LENGTH**: Had 89 missing values each. These were resolved after applying the "Remove Duplicate" function, then converted to integer format.

### Removing Duplicate Entries
![image](https://github.com/user-attachments/assets/9ebf422b-4907-4557-92e2-aac3f2cc3006)

The dataset was checked for duplicates. **306 duplicate records** were identified and removed based on `PRODUCT_ID`, ensuring data integrity across all columns.

### Standardizing Column Names
Column names were reviewed and standardized:
- Underscores were added where needed
- Converted some columns from lowercase to uppercase
No major renaming was required.

### Verifying Data Accuracy
- **Negative or Invalid Values**: No negative or invalid values were found in numerical columns.
- **Data Types**: Ensured proper formatting by converting `PRODUCT_TYPE_ID` and `PRODUCT_LENGTH` to integers.

## Short Title Creation

### Objective
The `SHORT_TITLE` feature was introduced to create brief, SEO-friendly product titles while maintaining essential keywords from the original title.

### Steps Taken:

- **Remove redundant words** like "includes", "set of" and "for" using this function:
   `Text.Replace(Text.Replace(Text.Replace([Title], " Set of ", "") " for " "") " Includes " "")`

- Limit title length between 30–50 characters using:
`if Text.Length([SHORT_TITLE]) > 50 then Text.Start([SHORT_TITLE], 50) else [SHORT_TITLE]`

- Create SHORT_TITLE column using first 3 words and last 2 words of the main title:
`Text.Combine(
  List.FirstN(Text.Split([Title], " "), 3)
  & List.LastN(Text.Split([Title], " "), 2),
  " "
)`

![Screenshot (497)](https://github.com/user-attachments/assets/cd7bf47e-caa5-46f9-ac55-5fd126a86bc5)

## Overview of Cleaned Dataset
The dataset was thoroughly cleaned. Identified and resolved issues include:

- Missing values in BULLET_POINTS: Replaced with N/A
- Null values in DESCRIPTION: Replaced with "None"
- Missing values in PRODUCT_TYPE_ID and PRODUCT_LENGTH: Resolved by removing duplicates
- Duplicates: 306 duplicates removed, resulting in 3541 rows
- Standardized data types
- Optimized lengthy titles using SHORT_TITLE

After completing the process, the cleaned dataset was loaded into an Excel sheet.
Total Rows: 3541

Total Columns: 7

Key Columns: 
`PRODUCT_ID`
`TITLE`
`BULLET_POINTS`
`DESCRIPTION`
`PRODUCT_TYPE_ID`
`PRODUCT_LENGTH` 
`SHORT_TITLE`

## Insights Generated

Count of PRODUCT_ID: 3541
![image](https://github.com/user-attachments/assets/50f40e38-0be5-42b8-a7e0-d0e878e43841)
![image](https://github.com/user-attachments/assets/b8a30ff7-89ed-46af-abef-623a67f18ec1)

## Conclusion
This report provides an overview of the data cleaning and title optimization process for the Product Data dataset. The cleaning focused on:
- Handling duplicates
- Resolving missing values
- Correcting inconsistencies

A new column `SHORT_TITLE` was created to enhance SEO and readability by extracting keywords from the main title. Column names were standardized and duplicate records removed. The dataset is now reliable for further marketing analysis and insights.

