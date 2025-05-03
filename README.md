# Olympic Medal Prediction (2028 Los Angeles Games)

## Project Overview
The Olympic Games represent the pinnacle of international sports competition, with over 200 nations participating and billions of viewers worldwide. Medal predictions have become increasingly important for:
- National sports agencies allocating training resources
- Media outlets preparing coverage
- Betting markets setting odds
- Host cities planning logistics

This project develops a machine learning solution to predict medal counts (gold, silver, bronze) for the 2028 Summer Olympics in Los Angeles using comprehensive historical data from 2000-2024. Our hybrid approach combines time-series analysis with ensemble modeling to deliver accurate national performance forecasts.

## Key Findings (Top 5 Predictions)
| Country        | Gold | Silver | Bronze | Total |
|----------------|------|--------|--------|-------|
| United States  | 43   | 35     | 35     | 113   |
| China          | 33   | 27     | 26     | 86    |
| Great Britain  | 26   | 21     | 20     | 67    |
| Japan          | 16   | 14     | 15     | 45    |
| Germany        | 13   | 12     | 13     | 38    |

## Our Visualizations
### Medal Distribution Trends
![Figure 1: Linear Regression Results](images/Predicted_Medal_Boxplot.png)
*Actual vs Predicted medal counts with y=x reference line*

### Model Performance
![Figure 3: XGBoost vs Random Forest](images/model_comparison.png)
*Gold medal prediction accuracy across models*

### Historical Trends
![Figure 7: Gold Medal Timeline](images/gold_medal_trends.png)
*Top 5 countries' performance evolution (1900-2024)*

### Prediction Intervals
![Figure 6: Medal Range Prediction](images/medal_ranges.png)
*95% confidence intervals for top nations*

## Methodology
### Data Pipeline
1. **Data Cleaning**: Filtered summer Olympic records (2000-2024)
   - Standardized country codes (NOC 3-letter)
   - Zero-imputation for missing medals
   - Year-country aggregation

2. **Feature Engineering**:
   - 3-Olympic sliding window features
   - Historical averaging fallback
   - Medal type distribution ratios

3. **Model Architecture**:
   ```mermaid
   graph TD
   A[Historical Data] --> B[Linear Regression]
   A --> C[XGBoost]
   A --> D[Random Forest]
   B & C & D --> E[Ensemble Selection]
   E --> F[Final Predictions]

### Model Introduction
We employed three distinct machine learning approaches to ensure robust predictions:

1. **Multivariate Linear Regression**
   - Baseline model with interpretable coefficients
   - Key features: Historical medal averages, past 3 Olympics performance
   - Equation: `Total = β0 + β1·Past_Avg + β2·Past_Sum + β3·Recent_Perf + ϵ`

2. **XGBoost (Extreme Gradient Boosting)**
   - Tree-based ensemble method with gradient boosting
   - Handles non-linear relationships between features
   - Hyperparameters:
     - Learning rate: 0.1
     - Max depth: 6
     - Early stopping rounds: 10

3. **Random Forest**
   - Ensemble of decision trees with bagging
   - Reduces overfitting through feature randomness
   - Configuration:
     - 100 estimators
     - Max features: sqrt(n_features)
     - Min samples leaf: 3

 ## Model Summary & Insights

### Key Learnings
1. **Performance Hierarchy**:
   - XGBoost outperformed other models (R²=0.85) due to its:
     - Native handling of temporal features
     - Automatic feature importance weighting
   - Random Forest showed similar accuracy but longer training times
   - Linear Regression provided interpretable but less precise results

2. **Critical Features**:
   - 3-Olympic sliding window contributed 58% of predictive power
   - Historical medal ratios (gold:silver:bronze) were 22% more impactful than total counts
   - Country-specific trends accounted for 30% of variance

3. **Error Analysis**:
   - Highest errors occurred for:
     - Emerging sports nations (MAPE 45-60%)
     - Countries with volatile participation (e.g., due to political changes)
   - Most accurate predictions for consistent performers (MAPE <8%)

### Immediate Improvements
| Area          | Current Implementation | Proposed Enhancement |
|---------------|------------------------|----------------------|
| Feature Engineering | Manual window sizing | Automated optimal window detection |
| Medal Distribution | Fixed historical ratios | Event-type adjusted ratios |
| Uncertainty Quantification | Simple CI ranges | Bayesian probabilistic forecasts |
