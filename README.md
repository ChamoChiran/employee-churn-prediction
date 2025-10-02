# Employee Churn Prediction - HR Analytics Project

## Project Overview

This project provides data-driven insights for the Human Resources department of a large consulting firm to predict employee attrition and develop effective retention strategies. By analyzing employee satisfaction, performance, workload, and other key factors, we built predictive models to identify employees at risk of leaving the company.

## Business Objective

**Primary Goal**: Predict whether an employee will leave the company using available features such as job satisfaction, performance evaluations, workload, tenure, and compensation.

**Business Impact**: Enable HR to proactively identify at-risk employees and implement targeted retention strategies, reducing turnover costs and maintaining organizational knowledge.

## Project Structure

```
├── data/
│   ├── HR_capstone_dataset.csv          # Main dataset
│   └── employee_data_dictionary.txt     # Data dictionary
├── docs/
│   ├── Executive Summary.pptx           # Executive presentation
│   └── PACE_strategy.docx              # Project methodology
├── models/
│   ├── clf_lr.pkl                      # Logistic Regression model
│   ├── clf_rf.pkl                      # Random Forest model
│   └── clf_xgb.pkl                     # XGBoost model (Champion)
├── notebooks/
│   ├── employee_churn_prediction.ipynb         # Base analysis
│   └── employee_churn_prediction-fe.ipynb     # Enhanced analysis with feature engineering
└── README.md
```

## Dataset Description

The dataset contains **14,999 employee records** with the following features:

| Variable | Description |
|----------|-------------|
| `satisfaction_level` | Employee-reported job satisfaction level [0–1] |
| `last_evaluation` | Score of employee's last performance review [0–1] |
| `number_projects` | Number of projects employee contributes to |
| `average_monthly_hours` | Average number of hours employee worked per month |
| `tenure` | How long the employee has been with the company (years) |
| `work_accident` | Whether or not the employee experienced a work accident |
| `churn_status` | Whether or not the employee left the company (target variable) |
| `promotion_last_5years` | Whether the employee was promoted in the last 5 years |
| `department` | Employee's department |
| `salary` | Employee's salary level (low, medium, high) |

## Key Findings

### Employee Churn Patterns

1. **Satisfaction Level**: 
   - Employees with higher satisfaction levels are significantly more likely to stay
   - Churned employees show bimodal distribution with peaks at very low (0.1) and moderate (0.4) satisfaction

2. **Performance Paradox**:
   - Both underperformers AND top performers are more likely to leave
   - High performers with excessive workload show "burnout cluster" behavior

3. **Workload Impact**:
   - Optimal project load is 3-5 projects for retention
   - Employees with 7+ projects show higher churn rates
   - Overwork index reveals employees working significantly above department norms are at risk

4. **Tenure Insights**:
   - Employees with 3-5 years tenure show highest churn risk
   - Long-tenured employees (7+ years) rarely leave
   - Early career employees (1-2 years) show mixed patterns

5. **Promotion & Recognition**:
   - Lack of promotion in last 5 years correlates with higher churn
   - Salary level shows significant relationship with retention

## Methodology

### Data Processing
- **Data Cleaning**: Removed 3,008 duplicate records
- **Feature Engineering**: Created advanced features:
  - `proj_tenure_ratio`: Projects per year of tenure
  - `overwork_index`: Hours relative to department median
  - `rel_performance`: Performance relative to department average
  - `rel_performance_sq`: Squared term to capture non-linear relationships

### Model Development
Implemented and compared three machine learning approaches:

1. **Logistic Regression** - Baseline interpretable model
2. **Random Forest** - Ensemble method for non-linear relationships
3. **XGBoost** - Gradient boosting for optimal performance

### Model Selection
- **Champion Model**: XGBoost
- **Evaluation Metric**: ROC AUC (chosen for imbalanced classification)
- **Validation Strategy**: Train/Validation/Test split with stratification

## Model Performance

The XGBoost model was selected as the champion based on superior ROC AUC performance across validation sets. The model effectively handles:
- Class imbalance in the dataset
- Non-linear relationships between features
- Feature interactions
- Robust performance across different employee segments

## Business Recommendations

### Immediate Actions
1. **Workload Management**: Monitor and redistribute excessive project loads (7+ projects)
2. **High-Performer Retention**: Identify overworked top performers and adjust workloads
3. **Career Development**: Implement structured promotion pathways for 3-5 year employees
4. **Satisfaction Monitoring**: Regular pulse surveys to identify satisfaction drops

### Strategic Initiatives
1. **Predictive Monitoring**: Deploy model to score employee churn risk monthly
2. **Department-Specific Programs**: Tailor retention strategies by department
3. **Performance Management**: Balance high performance expectations with sustainable workloads
4. **Recognition Programs**: Enhanced recognition for high performers to prevent burnout

## Technical Requirements

### Dependencies
```
pandas >= 1.3.0
numpy >= 1.21.0
scikit-learn >= 1.0.0
xgboost >= 1.5.0
matplotlib >= 3.4.0
seaborn >= 0.11.0
scipy >= 1.7.0
```

### Installation
```bash
pip install pandas numpy scikit-learn xgboost matplotlib seaborn scipy
```

## Usage

### Loading the Champion Model
```python
import pickle
import pandas as pd

# Load the trained model
with open('models/clf_xgb.pkl', 'rb') as f:
    model = pickle.load(f)

# Make predictions on new data
predictions = model.predict(X_new)
churn_probabilities = model.predict_proba(X_new)[:, 1]
```

### Feature Engineering Pipeline
```python
def feature_engineering(df):
    # Project-to-tenure ratio
    df['proj_tenure_ratio'] = df['number_projects'] / df['tenure']
    
    # Overwork index
    dept_median_hrs = df.groupby('department')['average_monthly_hours'].transform('median')
    df['overwork_index'] = df['average_monthly_hours'] / dept_median_hrs
    
    # Relative performance
    dept_avg_eval = df.groupby('department')['last_evaluation'].transform('mean')
    df['rel_performance'] = df['last_evaluation'] / dept_avg_eval
    df['rel_performance_sq'] = df['rel_performance'] ** 2
    
    return df
```

## Files Description

- **`employee_churn_prediction-fe.ipynb`**: Complete analysis with advanced feature engineering
- **`employee_churn_prediction.ipynb`**: Basic analysis and initial modeling
- **`clf_xgb.pkl`**: Final XGBoost model (recommended for production)
- **`HR_capstone_dataset.csv`**: Complete employee dataset

## License

This project is part of the Google Advanced Analytics Capstone program and is intended for educational purposes.

---

*This project demonstrates end-to-end data science methodology for HR analytics, from exploratory data analysis to production-ready predictive models.*