```markdown
# Learning Pandas 🐼

A comprehensive collection of pandas examples and techniques for data manipulation and analysis in Python.

## 📚 Table of Contents

- [Basic DataFrame Operations](#basic-dataframe-operations)
- [Loading Data from Files](#loading-data-from-files)
- [Accessing and Selecting Data](#accessing-and-selecting-data)
- [Filtering Data](#filtering-data)
- [Adding and Removing Columns](#adding-and-removing-columns)
- [Merging and Concatenating Data](#merging-and-concatenating-data)
- [Handling Null Values](#handling-null-values)
- [Data Aggregation](#data-aggregation)
- [Advanced Functionality](#advanced-functionality)

## 🚀 Basic DataFrame Operations

### Creating a DataFrame
```python
import pandas as pd

df = pd.DataFrame([[1,2,3],[4,5,6], [7,8,9]], 
                  columns=["A","B","C"], 
                  index=["x","y","z"])
```

### Essential DataFrame Methods
- `df.head(n)` - Display first n rows
- `df.tail(n)` - Display last n rows
- `df.info()` - DataFrame summary information
- `df.describe()` - Statistical summary
- `df.shape` - Dimensions (rows, columns)
- `df.columns.tolist()` - Get column names as list
- `df.index.tolist()` - Get index values as list
- `df.nunique()` - Count unique values per column
- `df['column'].unique()` - Get unique values in a column

## 📂 Loading Data from Files

### Supported File Formats
```python
# CSV Files
coffee_df = pd.read_csv('sample_data/coffee.csv')

# Parquet Files
results_df = pd.read_parquet('results.parquet')

# Excel Files
olympics_df = pd.read_excel('olympics-data.xlsx')
```

## 🎯 Accessing and Selecting Data

### Data Selection Methods
```python
# Random sampling
df.sample(10)

# Label-based selection
df.loc[[0,1,2]]
df.loc[5:8, ['Day', 'Units Sold']]

# Single value access
df.at[0, "Units Sold"]

# Sorting
df.sort_values("Units Sold", ascending=False)
```

## 🔍 Filtering Data

### Boolean Indexing
```python
# Multiple conditions with & (and) | (or)
filtered_df = df[(df['height_cm'] > 215) & (df['born_country'] == 'USA')]

# String operations
df[df['name'].str.contains('Naim Süleymanoğlu')]

# Query method (alternative syntax)
df.query('born_country == "TUR" and born_city == "Sinop"')
```

## ➕ Adding and Removing Columns

### Column Operations
```python
import numpy as np

# Conditional column creation
df['price'] = np.where(df['Coffee Type'] == "Espresso", 3.99, 5.99)

# Mathematical operations
df['revenue'] = df['Units Sold'] * df['price']

# String operations
df['First Name'] = df['name'].str.split(' ').str[0]

# Date operations
df['born_datetime'] = pd.to_datetime(df['born_date'])
df['born_year'] = df['born_datetime'].dt.year

# Apply custom functions
df['height_category'] = df['height_cm'].apply(
    lambda x: 'Tall' if x > 200 else ('Average' if x > 180 else 'Short')
)

# Remove columns
df.drop(columns=["price"])
```

## 🔗 Merging and Concatenating Data

### Combining DataFrames
```python
# Merge on common columns
merged_df = pd.merge(bios_df, nocs, left_on='born_country', right_on='NOC', how='left')

# Concatenate DataFrames vertically
combined_df = pd.concat([usa_df, gbr_df])

# Join on index
result = pd.merge(results_df, bios_df, on='athlete_id', how='left')
```

## 🚫 Handling Null Values

### Missing Data Operations
```python
# Fill with mean
df['Units Sold'].fillna(df['Units Sold'].mean())

# Interpolate missing values
df['Units Sold'].interpolate()

# Drop rows with null values
df.dropna(subset=['Units Sold'])

# Filter out null values
df[df['Units Sold'].notna()]
```

## 📊 Data Aggregation

### Grouping and Summarizing
```python
# Value counts
df['born_city'].value_counts()

# Group by operations
df.groupby(['Coffee Type'])['Units Sold'].sum()
df.groupby(['Coffee Type'])['Units Sold'].mean()

# Multiple aggregations
df.groupby(['Coffee Type', 'Day']).agg({'Units Sold': 'sum', 'price': 'mean'})

# Pivot tables
pivot = df.pivot(columns='Coffee Type', index='Day', values='revenue')

# Date-based grouping
df.groupby([df['year_born'], df['month_born']])['name'].count()
```

## 🔧 Advanced Functionality

### Rolling Windows
```python
# Moving averages
df['3day_avg'] = df['Units Sold'].rolling(3).sum()
```

### Data Cleaning with PyJanitor
```python
import janitor

# Clean column names
df.clean_names()  # Converts to snake_case
```

### Enhanced Data Profiling with Skimpy
```python
from skimpy import skim

# Comprehensive data summary
skim(df)  # Provides detailed statistics and visualizations
```

### Performance Optimization
```python
# Arrow backend for better performance
df_arrow = pd.read_parquet('data.parquet', engine='pyarrow', dtype_backend='pyarrow')
```

## 📋 Sample Datasets Used

This repository includes examples with the following datasets:
- **Coffee Sales Data**: Daily coffee sales by type
- **Olympics Data**: Athlete biographical information and competition results
- **Regional Data**: Country codes and regional mappings

## 🛠️ Required Libraries

```python
pip install pandas numpy pyjanitor skimpy
```

## 💡 Key Learning Points

1. **DataFrame Creation**: Multiple ways to create and initialize DataFrames
2. **Data Loading**: Reading from various file formats (CSV, Parquet, Excel)
3. **Data Selection**: Label-based and position-based indexing
4. **Filtering**: Boolean indexing and query operations
5. **Data Transformation**: Adding, modifying, and removing columns
6. **Data Combination**: Merging and concatenating datasets
7. **Missing Data**: Various strategies for handling null values
8. **Aggregation**: Grouping and summarizing data
9. **Performance**: Using modern pandas features for efficiency

## 🎯 Next Steps

- Explore time series analysis with pandas
- Learn about categorical data handling
- Practice with multi-level indexing
- Dive into pandas plotting capabilities
- Study memory optimization techniques

---

*Happy pandas learning! 🐼📊*
```
