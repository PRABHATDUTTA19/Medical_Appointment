# Data Cleaning and Preprocessing: No-Show Medical Appointments

## Project Overview

This repository contains the code and documentation for the data cleaning and preprocessing of the "No-Show Medical Appointments" dataset. The goal of this project is to transform raw, messy data into a clean, structured, and reliable format suitable for further exploratory data analysis (EDA), statistical modeling, or machine learning tasks aimed at understanding and predicting patient no-shows.

The original dataset provides information about over 100,000 medical appointments in Brazil, including patient characteristics, appointment details, and whether the patient showed up for their appointment.

## Dataset

* **Filename:** `KaggleV2-May-2016.csv`


## Data Cleaning and Preprocessing Steps

The following steps were performed to clean and preprocess the dataset. Detailed execution and code for each step can be found in the `No_Show_Appointments_Cleaning.ipynb` Jupyter Notebook.

### 1. Initial Data Inspection

* Loaded the dataset into a Pandas DataFrame.
* Performed initial checks using `df.head()`, `df.info()`, and `df.isnull().sum()` to understand structure, data types, and identify explicit missing values.
* **Observation:** The dataset initially had no explicit `NaN` values.

# Data Cleaning and Inspection for No-Show Medical Appointments Dataset

```python
# 2. Load the Dataset
# The first step is to load the raw CSV file into a Pandas DataFrame.

# Load the dataset from the uploaded CSV file
df = pd.read_csv('KaggleV2-May-2016.csv')

# Display the first 5 rows to get an initial glance at the data structure
print("--- Original DataFrame Head ---")
print(df.head())

# 3. Initial Data Inspection

# 3.1. DataFrame Information (.info())
# This provides a concise summary of the DataFrame
print("\n--- Original DataFrame Info ---")
df.info()

# 3.2. Missing Values Check (.isnull().sum())
# Count number of missing values for each column
print("\n--- Initial Missing Values Count ---")
print(df.isnull().sum())

# 4. Column Renaming and Standardization
# Rename columns to lowercase and snake_case, fix typos

df.columns = df.columns.str.lower().str.replace('[^a-z0-9_]', '', regex=True)
df.rename(columns={
    'patientid': 'patient_id',
    'appointmentid': 'appointment_id',
    'scheduledday': 'scheduled_day',
    'appointmentday': 'appointment_day',
    'hipertension': 'hypertension',
    'handcap': 'handicap',
    'sms_received': 'sms_received',
    'no_show': 'no_show'
}, inplace=True)

print("\n--- DataFrame Head after Renaming Columns ---")
print(df.head())
print("\n--- New Column Names ---")
print(df.columns.tolist())

# 5. Handling Duplicate Rows

initial_rows = df.shape[0]
df.drop_duplicates(inplace=True)
rows_after_dropping_duplicates = df.shape[0]

print(f"\n--- Duplicate Rows Check ---")
print(f"Initial number of rows: {initial_rows}")
print(f"Number of rows after dropping duplicates: {rows_after_dropping_duplicates}")

if initial_rows - rows_after_dropping_duplicates > 0:
    print(f"Removed {initial_rows - rows_after_dropping_duplicates} duplicate rows.")
else:
    print("No duplicate rows found.")

# 6. Standardize Categorical Text Values

print("\n--- Unique 'gender' values before standardization ---")
print(df['gender'].unique())

df['gender'] = df['gender'].str.upper().replace({'F': 'Female', 'M': 'Male'})

print("\n--- Unique 'gender' values after standardization ---")
print(df['gender'].unique())

# 7. Date Format Conversion

df['scheduled_day'] = pd.to_datetime(df['scheduled_day'])
df['appointment_day'] = pd.to_datetime(df['appointment_day'])

df['scheduled_day'] = df['scheduled_day'].dt.date
df['appointment_day'] = df['appointment_day'].dt.date

print("\n--- DataFrame Head after Date Conversion ---")
print(df[['scheduled_day', 'appointment_day']].head())

# 8. Data Type Correction and Anomalies Handling

# 8.1. Handling Invalid 'Age' Values

print("\n--- 'age' Column Descriptive Statistics ---")
print(df['age'].describe())

invalid_age_count = df[df['age'] < 0].shape[0]
print(f"\nNumber of invalid ages (less than 0): {invalid_age_count}")

if invalid_age_count > 0:
    df.loc[df['age'] < 0, 'age'] = np.nan
    median_age = df['age'].median()
    df['age'].fillna(median_age, inplace=True)
    df['age'] = df['age'].astype(int)
    print(f"Invalid ages imputed with median: {median_age:.0f} and column converted to integer.")
else:
    df['age'] = df['age'].astype(int)
    print("No invalid ages found. 'age' column ensured to be integer type.")

# 8.2. Final Data Type Review

print("\n--- Final DataFrame Info after all cleaning steps ---")
df.info()

# 9. Save Cleaned Data

df.to_csv('KaggleV2-May-2016_cleaned.csv', index=False)
print("\nCleaned data saved to 'KaggleV2-May-2016_cleaned.csv'")
```

