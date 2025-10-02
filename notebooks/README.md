# Notebooks Directory

This directory contains two Jupyter notebooks for the employee churn prediction analysis:

## Notebook Descriptions

### 1. `employee_churn_prediction.ipynb`
**Basic Analysis without Feature Engineering**

- Contains the fundamental exploratory data analysis (EDA)
- Uses original dataset features only
- Implements baseline machine learning models
- Provides initial insights into employee churn patterns
- Good starting point for understanding the data and basic modeling approach

### 2. `employee_churn_prediction-fe.ipynb`
**Enhanced Analysis with Feature Engineering**

- Includes comprehensive feature engineering techniques
- Creates advanced derived features:
  - `proj_tenure_ratio`: Projects per year of tenure
  - `overwork_index`: Hours relative to department median
  - `rel_performance`: Performance relative to department average
  - `rel_performance_sq`: Squared performance term for non-linear relationships
- Implements multiple machine learning models (Logistic Regression, Random Forest, XGBoost)
- Contains detailed model comparison and evaluation
- **Recommended notebook** for complete analysis and production-ready models

## Usage Recommendations

- **Start with**: `employee_churn_prediction.ipynb` to understand the basic approach
- **Use for production**: `employee_churn_prediction-fe.ipynb` for best model performance
- **Feature engineering notebook** contains the champion XGBoost model used in the final recommendations

## Key Differences

| Aspect | Basic Notebook | Feature Engineering Notebook |
|--------|---------------|------------------------------|
| **Features** | Original dataset only | Original + 4 engineered features |
| **Models** | Baseline models | Multiple optimized models |
| **Performance** | Good baseline | Superior predictive performance |
| **Complexity** | Simple, educational | Production-ready |
| **Recommendations** | Initial insights | Comprehensive business strategy |

## Getting Started

1. **Prerequisites**: Ensure you have the required dependencies installed (see main README.md)
2. **Data**: Both notebooks expect the dataset to be in `../data/HR_capstone_dataset.csv`
3. **Models**: Trained models are saved to `../models/` directory
4. **Run Order**: Either notebook can be run independently, but the feature engineering version is recommended for complete analysis

---

*Both notebooks follow the PACE (Plan-Analyze-Construct-Execute) methodology for systematic data science project development.*