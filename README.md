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

### 2. Column Renaming and Standardization

* Column headers were converted to lowercase and formatted to snake_case (e.g., `PatientId` to `patient_id`, `ScheduledDay` to `scheduled_day`).
* Common typos in column names like `Hipertension` and `Handcap` were corrected to `hypertension` and `handicap` respectively, for clarity and consistency.

### 3. Handling Duplicate Rows

* A check for exact duplicate rows was performed.
* **Observation:** No duplicate rows were found in the dataset.

### 4. Standardizing Categorical Text Values

* The `Gender` column (renamed to `gender`) was standardized. 'F' and 'M' entries were converted to 'Female' and 'Male' respectively to ensure uniformity.

### 5. Date Format Conversion

* The `ScheduledDay` and `AppointmentDay` columns (renamed to `scheduled_day` and `appointment_day`) were converted from string/object types to `datetime` objects.
* The time component was removed, ensuring that both columns represent only the date (`YYYY-MM-DD`).

### 6. Data Type Correction and Anomalies Handling

* The `Age` column (renamed to `age`) was inspected for inconsistencies.
* An invalid `age` entry of `-1` was identified. This entry was imputed (replaced) with the median age of the dataset (37) to maintain data integrity without skewing statistics.
* The `age` column was then explicitly cast to an integer type.
* All other columns' data types were verified to be appropriate for their content.

## How to Run the Cleaning Process

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YourGitHubUsername/your-repo-name.git](https://github.com/YourGitHubUsername/your-repo-name.git)
    cd your-repo-name
    ```
2.  **Install Dependencies:** Ensure you have Python installed. It's recommended to use a virtual environment or Anaconda.
    ```bash
    pip install pandas numpy matplotlib seaborn
    ```
3.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook No_Show_Appointments_Cleaning.ipynb
    ```
    Execute all cells in the notebook to perform the data cleaning and preprocessing. This will generate the `KaggleV2-May-2016_cleaned.csv` file.

## Cleaned Data

The cleaned dataset is available as `KaggleV2-May-2016_cleaned.csv` in this repository, ready for further analysis.

## Future Work

* **Exploratory Data Analysis (EDA):** In-depth visualization and statistical analysis of the cleaned data to uncover patterns and insights.
* **Feature Engineering:** Creation of new features (e.g., `days_between_scheduling_and_appointment`, `appointment_day_of_week`) that could be useful for modeling.
* **Predictive Modeling:** Building machine learning models to predict `no_show` based on patient and appointment characteristics.

## Contact

For any questions or suggestions, please feel free to reach out.

* **Prabhat Dutta**
* [Your LinkedIn Profile (Optional)]
* [Your Email Address (Optional)]
