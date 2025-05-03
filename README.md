# Olympic Medal Prediction (2028 Los Angeles Games)

## Project Overview
This project predicts medal counts (gold, silver, bronze) for countries participating in the 2028 Summer Olympics in Los Angeles using historical Olympic data from 2000-2024. The solution combines time-series analysis with machine learning to forecast national performance.

## Key Findings (Top 5 Predictions)
| Country        | Gold | Silver | Bronze | Total |
|----------------|------|--------|--------|-------|
| United States  | 43   | 35     | 35     | 113   |
| China          | 33   | 27     | 26     | 86    |
| Great Britain  | 26   | 21     | 20     | 67    |
| Japan          | 16   | 14     | 15     | 45    |
| Germany        | 13   | 12     | 13     | 38    |

![Medal Distribution](https://via.placeholder.com/600x400?text=3D+Medal+Bar+Chart)

## Methodology
### Data Pipeline
1. **Data Cleaning**: Filtered summer Olympic records (2000-2024)
   - Standardized country codes
   - Filled missing medals with zeros
   - Aggregated by year-country

2. **Feature Engineering**:
   - Sliding window of past 3 Olympic performances
   - Historical averages for countries with <4 participations
   - Medal type ratios based on historical distribution

3. **Model Architecture**:
   ```mermaid
   graph TD
   A[Historical Data] --> B[Linear Regression]
   A --> C[XGBoost]
   A --> D[Random Forest]
   B & C & D --> E[Ensemble Selection]
   E --> F[Final Predictions]
