# TASK-2-
The House Price dataset was loaded using the Pandas library, and missing values were identified using the .isnull().sum() function. This step helped determine which features contained null values and the extent of missing data. In housing datasets, missing values often appear in variables related to property features such as basement.

# data_cleaning.py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# house-price-missing-value-analysis
df = pd.read_csv("/content/nominal-index.csv") 

# initial-data-exploration
df.info()

# missing-value-analysis
missing_values = df.isnull().sum()
print(missing_values)

# missing-data-visualization
missing_values[missing_values > 0].plot(
    kind='bar',
    figsize=(10, 5),
    title='Missing Values per Column'
)
plt.ylabel('Count of Missing Values')
plt.show()

# numerical-feature-identification 
numerical_cols = df.select_dtypes(include=['int64', 'float64']).columns
print(numerical_cols)

# numerical-missing-value-imputation
df[numerical_cols] = df[numerical_cols].fillna(df[numerical_cols].mean())

# categorical-feature-identification
categorical_cols = df.select_dtypes(include=['object', 'category']).columns
print(categorical_cols)

# categorical-missing-value-imputation
for col in categorical_cols:
    df[col].fillna(df[col].mode()[0], inplace=True)

# drop-high-missing-columns
threshold = 0.5 * len(df)
df = df.dropna(axis=1, thresh=threshold)
    
# dataset-validation
df.shape

# missing-value-detection
df.isnull().sum()

# total-missing-values-check
df.isnull().sum().sum()

# dataset-loading
original_df = pd.read_csv("/content/nominal-year.csv")

# missing-value-comparison
print("Before Cleaning Missing Values:")
print(original_df.isnull().sum())

print("\nAfter Cleaning Missing Values:")
print(df.isnull().sum())
