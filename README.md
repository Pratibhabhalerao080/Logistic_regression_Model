## Predicting Customer Purchase Decisions for Additional Insurance Products

### Introduction

This project aims to predict customer purchase decisions regarding an additional insurance product. Accurate predictions in this context can help insurance companies tailor their marketing strategies, allocate resources efficiently, and enhance customer satisfaction. The project involves several key steps:

### Key Points

1. **Problem Significance**: Predicting customer purchase decisions enables insurance companies to tailor their marketing strategies, optimize resource allocation, and enhance customer satisfaction.

2. **Data Exploration**: The project starts with loading and exploring the dataset to gain insights into customer characteristics and historical purchase patterns.

3. **Class Imbalance**: A class imbalance issue is observed in the 'TARGET' variable, which necessitates specialized handling to avoid model bias.

4. **Data Preparation**: The data is preprocessed by converting variables into suitable formats, removing uninformative features, and applying feature scaling where necessary.

5. **Model Selection**: The project involves creating and evaluating multiple logistic regression models with different feature sets to determine the most effective approach for predicting customer purchase decisions.

### Getting Started

The code begins by loading the dataset from a remote source and performing some initial data exploration:

```python
import pandas as pd

# Load the dataset
df = pd.read_csv("https://raw.githubusercontent.com/Pratibhabhalerao080/DAV-6150/main/M7_Data.csv")

# Exploratory Data Analysis
df.info()
df.describe()
df.isnull().sum()
```

### Class Imbalance

The class imbalance issue is addressed by visualizing and analyzing the distribution of the 'TARGET' variable:

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Visualize the distribution of the target variable
sns.countplot(df['TARGET'])
plt.title('Distribution of Target')
plt.show()

# Calculate the class distribution of the 'TARGET' variable
class_distribution = df['TARGET'].value_counts()
print(class_distribution)
```

### Data Preparation

Data preparation involves various steps, including handling uninformative features, converting target labels, and feature scaling:

```python
# Convert 'TARGET' values to binary form
df['TARGET'] = df['TARGET'].map({'Y': 1, 'N': 0})

# Drop uninformative columns
df.drop('contract', axis=1, inplace=True)
df.drop('ID', axis=1, inplace=True)

# Remove rows where 'loyalty' is 'Unclassified' (99)
df = df[df['loyalty'] != 99]

# Perform one-hot encoding for 'loyalty'
df = pd.get_dummies(df, columns=['loyalty'], drop_first=True)

# Scale specific features
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
columns_to_scale = ['turnover_A', 'turnover_B', 'LOR', 'lor_M']
df[columns_to_scale] = scaler.fit_transform(df[columns_to_scale])
```

### Feature Selection

Feature selection is performed using the SelectKBest method with a chi-squared test to choose the top 'K' features:

```python
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import chi2

# Define the number of top features to select
k = 13

# Perform feature selection with the chi-squared test
selector = SelectKBest(score_func=chi2, k=k)
X_new = selector.fit_transform(X, y)
```

### Model Evaluation

Multiple logistic regression models are created and evaluated, and the preferred model is selected based on performance metrics:

```python
# Evaluate Model 1: Using Selected Features
# Evaluate Model 2: Using Different Features
# Evaluate Model 3: Using Scaled Features

# Display results
```

The preferred model is chosen based on performance metrics and domain-specific considerations.

### Testing Subset Evaluation

The selected model is evaluated on a testing subset to ensure its consistency and reliability:

```python
# Apply the selected model to the testing subset
# Evaluate the selected model on the testing subset
```

The model's performance on the testing subset is consistent with the validation subset, ensuring its reliability.

### Conclusions

In conclusion, this project's objective is to provide insurance companies with a powerful predictive tool to optimize marketing strategies and resource allocation, ultimately enhancing customer satisfaction and overall business outcomes. The steps taken in this project, from data exploration to model selection and evaluation, contribute to achieving this goal.﻿# Logistic_regression_Model
