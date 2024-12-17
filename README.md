# Day-7-week-2-assignment-
Assignment for week 2 day 7
Task 1: Load and Explore the Dataset
Choose a dataset in CSV format (for example, you can use datasets like the Iris dataset, a sales dataset, or any dataset of your choice).
Load the dataset using pandas.
Display the first few rows of the dataset using .head() to inspect the data.
Explore the structure of the dataset by checking the data types and any missing values.
Clean the dataset by either filling or dropping any missing values.
Task 2: Basic Data Analysis
Compute the basic statistics of the numerical columns (e.g., mean, median, standard deviation) using .describe().
Perform groupings on a categorical column (for example, species, region, or department) and compute the mean of a numerical column for each group.
Identify any patterns or interesting findings from your analysis.
Task 3: Data Visualization
Create at least four different types of visualizations:
Line chart showing trends over time (for example, a time-series of sales data).
Bar chart showing the comparison of a numerical value across categories (e.g., average petal length per species).
Histogram of a numerical column to understand its distribution.
Scatter plot to visualize the relationship between two numerical columns (e.g., sepal length vs. petal length).
Customize your plots with titles, labels for axes, and legends where necessary.


# Import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Enable inline plotting for Jupyter Notebook
# %matplotlib inline  

# ------------------------------- TASK 1: LOAD AND EXPLORE THE DATASET ------------------------------- #

# 1. Load the dataset
try:
    # Use a dataset of your choice or the Iris dataset
    dataset_path = 'your_dataset.csv'  # Replace with the path to your CSV file
    df = pd.read_csv(dataset_path)
    print("Dataset loaded successfully!\n")
except FileNotFoundError as e:
    print(f"Error: {e}")
    exit()

# 2. Display the first few rows of the dataset
print("First 5 rows of the dataset:")
print(df.head())

# 3. Explore the structure of the dataset
print("\nDataset Information:")
print(df.info())

print("\nSummary of Missing Values:")
print(df.isnull().sum())

# 4. Clean the dataset by handling missing values
# Drop rows with missing values or fill them with a specific value
df_cleaned = df.dropna()
print("\nMissing values removed. Cleaned dataset summary:")
print(df_cleaned.info())

# ------------------------------- TASK 2: BASIC DATA ANALYSIS ------------------------------- #

# 1. Compute basic statistics of the numerical columns
print("\nStatistical Summary of Numerical Columns:")
print(df_cleaned.describe())

# 2. Perform groupings on a categorical column and compute the mean
# Replace 'categorical_column' and 'numerical_column' with your column names
categorical_column = 'species'  # Example for Iris dataset
numerical_column = 'sepal_length'

if categorical_column in df_cleaned.columns and numerical_column in df_cleaned.columns:
    grouped_data = df_cleaned.groupby(categorical_column)[numerical_column].mean()
    print(f"\nMean of {numerical_column} grouped by {categorical_column}:")
    print(grouped_data)
else:
    print("\nSpecified columns for grouping not found in the dataset.")

# ------------------------------- TASK 3: DATA VISUALIZATION ------------------------------- #

# Set the seaborn style for better visuals
sns.set(style="whitegrid")

# 1. Line chart: Trend over time (if a time-series column is available)
# Replace 'date_column' and 'value_column' as needed
if 'date' in df_cleaned.columns:
    df_cleaned['date'] = pd.to_datetime(df_cleaned['date'])  # Convert to datetime
    df_cleaned.set_index('date', inplace=True)
    plt.figure(figsize=(10, 6))
    df_cleaned['value_column'].plot(linewidth=2)
    plt.title("Line Chart of Value Over Time")
    plt.xlabel("Date")
    plt.ylabel("Value")
    plt.show()
else:
    print("\nNo date column found for line chart.")

# 2. Bar chart: Comparison of numerical value across categories
plt.figure(figsize=(8, 6))
sns.barplot(x=categorical_column, y=numerical_column, data=df_cleaned)
plt.title(f"Bar Chart of {numerical_column} by {categorical_column}")
plt.xlabel(categorical_column)
plt.ylabel(numerical_column)
plt.show()

# 3. Histogram: Distribution of a numerical column
plt.figure(figsize=(8, 6))
sns.histplot(df_cleaned[numerical_column], bins=20, kde=True, color='skyblue')
plt.title(f"Histogram of {numerical_column}")
plt.xlabel(numerical_column)
plt.ylabel("Frequency")
plt.show()

# 4. Scatter plot: Relationship between two numerical columns
numerical_column1 = 'sepal_length'  # Example column
numerical_column2 = 'sepal_width'   # Example column

if numerical_column1 in df_cleaned.columns and numerical_column2 in df_cleaned.columns:
    plt.figure(figsize=(8, 6))
    sns.scatterplot(x=numerical_column1, y=numerical_column2, data=df_cleaned, hue=categorical_column, palette="deep")
    plt.title(f"Scatter Plot: {numerical_column1} vs {numerical_column2}")
    plt.xlabel(numerical_column1)
    plt.ylabel(numerical_column2)
    plt.legend(title=categorical_column)
    plt.show()
else:
    print("\nNumerical columns for scatter plot not found.")

# ------------------------------- FINDINGS AND OBSERVATIONS ------------------------------- #
print("\nFindings and Observations:")
print("- The statistical summary provides insight into the distribution of numerical columns.")
print(f"- The bar chart shows the comparison of {numerical_column} across {categorical_column}.")
print(f"- The scatter plot reveals the relationship between {numerical_column1} and {numerical_column2}.")
print("- Mention specific patterns or trends based on your dataset analysis.")
