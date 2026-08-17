# DJS-CodeAI
Solving DJ Sanghvi CodeAI comitee tasks.
# Data Preprocessing and EDA

## Overview

The goal of this project was to explore and clean the dataset before using it for machine learning. I focused on understanding the data first and then making reasonable preprocessing decisions rather than trying to create a "perfect" dataset.

## 1. Initial Data Inspection

The dataset contains 33,049 rows and 16 columns. I first checked:

- Dataset shape and column names
- Data types
- Missing values
- Basic statistics using `describe()`

Although `isnull()` showed no missing values, I noticed that some categorical columns used `?` to represent missing or unknown values.

## 2. Exploratory Data Analysis

I used histograms, KDE plots, boxplots, count plots, and a correlation heatmap to understand the data.

This helped me identify:

- The distribution of numerical variables
- Possible outliers
- Categorical variable distributions
- Relationships between numerical features

I did not automatically remove every outlier because an unusual value is not necessarily an incorrect value.

## 3. Handling Unrealistic Ages

The `age_years` column contained some unrealistic values above 122. I considered these to be data-quality issues and removed those rows:
`df_cleaner = df[df["age_years"] < 122].copy()`

After cleaning, the maximum age was 90.

## 4. Handling Missing Gender Values

The gender_code column contained `?` values. Since `?` represents missing information rather than an actual category, I replaced it with NaN and removed those rows:
`df_cleaner["gender_code"] = df_cleaner["gender_code"].replace("?", np.nan)`<p>
`df_cleaner = df_cleaner.dropna(subset=["gender_code"])`

I chose to handle this column specifically rather than deleting the entire column.

## 5. Outliers

Some variables, such as sample_weight_index and financial features, contained extreme values. I did not remove all of them because they may represent valid observations. I only removed values that could reasonably be considered unrealistic based on the data and domain context.

## 6. Conclusion

Overall, the preprocessing was based on understanding the data first and then making practical decisions. The main steps were checking the data, exploring distributions and relationships, removing clearly unrealistic ages, and handling missing gender values.

The goal was to keep as much useful information as possible while making the dataset more suitable for the next stages of the machine learning pipeline.