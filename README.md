# Transaction Data Outlier Detection using IQR (Python)

## Project Overview
This project focuses on detecting, visualizing, and removing outliers from a transaction dataset using the **Interquartile Range (IQR)** method in Python. It demonstrates a real-world **data cleaning and exploratory data analysis (EDA)** workflow commonly used in analytics projects.

## Tools & Technologies
- Python
- Pandas
- Matplotlib
- Google Colab

## Dataset
- **File Name:** `transaction_dataset.csv`
- **Column Used:** `transaction_amount`
- Contains transaction values where extreme values may negatively impact analysis.

## Methodology
1. Upload and load dataset
2. Perform basic EDA
3. Detect outliers using IQR
4. Visualize outliers using boxplot
5. Remove outliers
6. Export cleaned dataset

## Python Code

```python
# Upload file in Google Colab
from google.colab import files
uploaded = files.upload()

# Import required libraries
import pandas as pd
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv("transaction_dataset.csv")

# Preview data
df.head()

# Summary statistics
df.describe()

# Calculate IQR
Q1 = df['transaction_amount'].quantile(0.25)
Q3 = df['transaction_amount'].quantile(0.75)
IQR = Q3 - Q1

# Define bounds
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

# Identify outliers
df['outlier_iqr'] = (df['transaction_amount'] < lower) | (df['transaction_amount'] > upper)

# View outliers
df[df['outlier_iqr']].head()

# Visualize outliers using boxplot
plt.boxplot(df['transaction_amount'])
plt.title("Transaction Amount – Outlier Visualization")
plt.show()

# Remove outliers
clean_df = df[df['outlier_iqr'] == False]

# Save cleaned dataset
clean_df.to_csv("cleaned_dataset.csv", index=False)

# Download cleaned dataset
files.download("cleaned_dataset.csv")
