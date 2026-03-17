# Student Performance Analysis & Prediction

## Project Overview

This project analyzes student performance data and predicts the final scores using a Linear Regression model. The project follows a complete Data Science pipeline — from raw data cleaning to feature engineering, modeling, and evaluation — as learned in the DECODE Data Science Bootcamp 2026 at COMSATS WAH.

The goal is to understand which factors influence student performance and build a predictive model to estimate final scores.

## Dataset

The dataset contains 205 rows and 14 columns.

Columns include: Student_ID, Name, Age, Gender, City, Department, Education_Level, Attendance_%, Study_Hours_Daily, Assignments, Quizzes, Midterm, Internet_Access, and Final_Score (target).

Issues in the dataset:

- Inconsistent casing (Gender, Name, Department)
- Wrong data types (Age in text)
- Missing values (Assignments, Attendance, Midterm, Study_Hours)
- Impossible values (Attendance_% <0 or >100, Final_Score >100)
- Duplicate rows

Note: The dataset is included in the repository as `student_data.xlsx`.

## Steps Followed

### Step 1: Data Loading & Exploration

- Loaded the CSV file using pandas.
- Checked shape, column names, data types, first/last 5 rows, and statistical summary.
- Observed missing values and data inconsistencies.

**Initial observations:**

- Missing values exist in multiple columns.
- Categorical columns have inconsistent casing.
- Some numerical columns have impossible values.

### Step 2: Data Cleaning

- Fixed all inconsistencies:
  - Gender: Standardized to Male/Female.
  - Name: Converted to Title Case.
  - Department: Uppercase, stripped spaces.
  - Age: Converted text to numeric; missing values filled with median.
  - Attendance_% and Final_Score: Impossible values replaced with NaN, then filled with median.
- Filled missing numerical values with median to avoid bias.
- Removed duplicate rows.
- Final dataset has zero missing values.

**Justifications:**

- Median used instead of mean for robustness to outliers.
- Duplicates removed to prevent model overfitting.
- Impossible values replaced with NaN to avoid corrupting predictions.

### Step 3: Exploratory Data Analysis (EDA)

- Plotted distributions, scatter plots, boxplots, and heatmaps using Seaborn.

**Key insights:**

- Higher attendance and study hours generally lead to higher final scores.
- Midterm scores strongly correlate with final scores.
- Some departments perform better on average than others.

### Step 4: Feature Engineering & Pipeline

- Created a new feature: `Total_Academic = Midterm + Assignments*5 + Quizzes*2`.
- Added `Attendance_Category` (Low, Medium, High) based on Attendance_%.
- Dropped Student_ID and Name (no predictive value).
- Encoded categorical columns:
  - One-Hot: Gender, Internet_Access, City, Department
  - Ordinal: Education_Level, Attendance_Category
- Scaled numerical features using StandardScaler.
- Split dataset into train (80%) and test (20%) sets before transformation.
- Built a sklearn Pipeline combining preprocessing and LinearRegression.

### Step 5: Model Training & Evaluation

- Trained the pipeline on training data.
- Predicted final scores on test data.
- Evaluated model:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
  - R² Score
- Visualized actual vs predicted final scores with a scatter plot.

**Observations:**

- Points close to diagonal → good predictions.
- Features with highest weight: Midterm, Total_Academic, and Study_Hours_Daily.
- Model explains ~0.7 of variance in final scores (R² ≈ 0.7).

## Conclusions

- Final scores are primarily influenced by Midterm scores, Assignments, Quizzes, Attendance, and Study Hours.
- Linear Regression provides a good baseline with R² ≈ 0.7, indicating the model captures a significant portion of the pattern in final scores.

**Possible improvements:**

- Try more complex models like Random Forest or XGBoost.
- Feature selection or interaction features.
- Clean dataset further or add more data points.

## Tools Used
- Python  
- Pandas, NumPy  
- Seaborn, Matplotlib  
- Scikit-learn  

## Author
Fizza Batool
FA23-BCS-056
