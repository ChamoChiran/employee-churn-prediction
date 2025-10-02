# Data Directory

This directory contains the dataset and documentation for the employee churn prediction project.

## Files Overview

### `HR_capstone_dataset.csv`
**Main Dataset** - Contains 14,999 employee records with 10 features for predicting employee turnover.

### `employee_data_dictionary.txt`
**Data Dictionary** - Detailed description of all variables, data types, and value ranges.

## Dataset Description

**Size**: 14,999 employee records  
**Features**: 10 variables (8 numerical, 2 categorical)  
**Target Variable**: `left` (whether employee left the company)  
**Data Quality**: Contains 3,008 duplicate records (handled in analysis)

## Variable Details

| Column Name | Data Type | Description | Range/Values |
|-------------|-----------|-------------|--------------|
| `satisfaction_level` | int64 | Employee's self-reported satisfaction level | [0-1] |
| `last_evaluation` | int64 | Score of employee's last performance review | [0-1] |
| `number_project` | int64 | Number of projects employee contributes to | Integer |
| `average_monthly_hours` | int64 | Average hours worked per month | Integer |
| `time_spend_company` | int64 | Years with the company (tenure) | Integer |
| `work_accident` | int64 | Whether employee experienced work accident | 0/1 (Binary) |
| `left` | int64 | **Target**: Whether employee left company | 0/1 (Binary) |
| `promotion_last_5years` | int64 | Promoted in last 5 years | 0/1 (Binary) |
| `department` | str | Employee's department | Categorical |
| `salary` | str | Employee's salary level | low/medium/high |

## Key Dataset Characteristics

### Target Variable Distribution
- **Stayed (0)**: ~76% of employees
- **Left (1)**: ~24% of employees
- **Class Imbalance**: Moderate imbalance requiring appropriate modeling techniques

### Feature Types
- **Continuous**: satisfaction_level, last_evaluation
- **Discrete Numerical**: number_project, average_monthly_hours, time_spend_company
- **Binary**: work_accident, left, promotion_last_5years
- **Categorical**: department, salary

### Data Quality Notes
- **Missing Values**: None detected
- **Duplicates**: 3,008 duplicate records identified and removed during preprocessing
- **Outliers**: Present in tenure variable, handled appropriately based on model sensitivity

## Business Context

This dataset represents employee information from a large consulting firm, capturing key factors that influence employee retention:

- **Performance Metrics**: Satisfaction and evaluation scores
- **Workload Indicators**: Project count and monthly hours
- **Career Progression**: Tenure and promotion history
- **Workplace Factors**: Department, salary level, work accidents

## Usage in Analysis

The dataset supports multiple analytical approaches:

1. **Exploratory Data Analysis**: Understanding churn patterns across different employee segments
2. **Statistical Testing**: Hypothesis testing for significant differences between churned and retained employees
3. **Feature Engineering**: Creating derived variables like project-to-tenure ratio and overwork indices
4. **Predictive Modeling**: Binary classification to predict employee churn probability

## Data Loading

```python
import pandas as pd

# Load the main dataset
df = pd.read_csv('HR_capstone_dataset.csv')

# Basic info
print(f"Dataset shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
```

## Data Preprocessing Notes

Before analysis, the following preprocessing steps are recommended:

1. **Duplicate Removal**: Remove 3,008 duplicate records
2. **Column Renaming**: Standardize to snake_case format
3. **Feature Engineering**: Create derived variables for enhanced predictions
4. **Encoding**: Apply appropriate encoding for categorical variables
5. **Scaling**: Consider scaling for distance-based algorithms

## Data Ethics & Privacy

- Employee data has been anonymized
- No personally identifiable information (PII) included
- Used for educational and analytical purposes only
- Follows ethical guidelines for HR analytics

---

*This dataset enables comprehensive analysis of employee churn patterns and supports data-driven HR decision making.*