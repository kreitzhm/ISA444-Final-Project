# ISA444 Final Project - Hotel Occupancy Forecasting Analysis

## Business Question
**Do forecasting models systematically under or over-forecast hotel occupancy?**

## Dataset Overview
- **17 hotels** across different locations and types (hotel_28 & hotel_77 removed due to irregularities)
- **518 days** of training data (January 1, 2022 - June 2, 2023)
- **28-day** forecast horizon (June 3-30, 2023)
- **Target variable:** Daily occupancy rate (0-1 scale)

## Models Compared
1. Naive
2. Seasonal Naive
3. AutoETS
4. AutoARIMA
5. LightGBM
6. AutoNBEATS
7. AutoNHITS
8. Chronos (Foundation Model)

## Key Findings
### Best Overall Model: LightGBM
- Won 24 out of 68 competitions (most wins)
- Best performance across all metrics (MAE, RMSE, MAPE, Bias)
- Nearly neutral bias (0.0019)

**Other competitive models:**
- AutoARIMA: 17 wins - strong balanced performance
- AutoETS: 11 wins
- SeasonalNaive: 9 wins

### Systematic Bias Analysis
**Models that OVER-forecast (predict too high):**
| Model | Average Bias | Interpretation |
|-------|--------------|----------------|
| Chronos | +0.0372 | Moderate over-forecasting |
| Naive | +0.0225 | Slight over-forecasting |
| LightGBM | +0.0019 | Nearly neutral |

**Models that UNDER-forecast (predict too low):**
| Model | Average Bias | Interpretation |
|-------|--------------|----------------|
| SeasonalNaive | -0.0175 | Slight under-forecasting (most neutral) |
| AutoARIMA | -0.0215 | Slight under-forecasting |
| AutoETS | -0.0302 | Moderate under-forecasting |
| AutoNBEATS | -0.0408 | Moderate under-forecasting |
| AutoNHITS | -6270.11 | **Failed - extreme values**  |

### Model Insights
- LightGBM wins because it captures complex patterns using lag features and can handle the 518 days of data well
- Statistical models (AutoETS, AutoARIMA) tend to under-forecast, being more conservative
- Neural networks struggled due to limited training data (518 days is marginal for deep learning)
- Chronos over-forecasts slightly, possibly because foundation models are trained on different data distributions

## Conclusion 
### Answer to Business Problem
**Forecasting models systematically under-forecast hotel occupancy.**
- 5 out of 8 models show negative bias (under-forecasting)
- Only 3 models over-forecast (Chronos, Naive, LightGBM)

### Recommendations
1. **Use LightGBM for production forecasting**
   - Highest accuracy
   - Nearly unbiased predictions
   - Reliable across different hotel types

2. **Consider SeasonalNaive as a simple baseline**
   - Minimal bias
   - Easy to implement and explain
   - Good for quick estimates

3. **Be aware of systematic bias**
   - Most statistical models under-forecast by 2-4%
   - Adjust business decisions accordingly
   - Consider adding a bias correction factor

4. **Avoid neural networks with limited data**
   - Need 2+ years of data for reliable performance
   - Current dataset (518 days) insufficient
