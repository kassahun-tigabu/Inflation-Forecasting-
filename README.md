
##  CPI Forecasting using Recurrent Neural Networks (RNNs)

### 1. Project Overview

This project aims to build and optimize a Recurrent Neural Network (RNN) model to forecast the Consumer Price Index (CPI). CPI is a critical economic indicator that measures inflation and purchasing power. Accurate forecasting of CPI can provide valuable insights for economic policy-making, investment strategies, and business planning.

The project follows a structured approach:
1.  **Data Preprocessing & Sequence Creation**: Preparing the time series data for RNN input.
2.  **Exploratory Data Analysis (EDA)**: Understanding the characteristics of the CPI and inflation data.
3.  **Baseline RNN Model**: Developing a simple RNN model as a starting point.
4.  **Improved Model with LSTM/GRU & Hyperparameter Tuning**: Enhancing model performance using more advanced RNN architectures and optimizing their parameters.
5.  **Model Evaluation & Forecasting**: Thoroughly evaluating the best model and generating future CPI forecasts.

### 2. Data Source

The dataset `cpiai_csv.csv` contains historical monthly CPI Index and Inflation Rate data spanning **1212 months from 1913 to 2014**.

### 3. Methodology

#### 3.1. Data Preprocessing & Sequence Creation

*   **Feature Selection**: Initially, only the 'Index' (CPI) was used as a feature. Later, the 'Inflation' rate was added to create a multi-feature input sequence.
*   **Normalization**: Data was scaled using `MinMaxScaler` to a range of (0, 1) to prepare it for neural network training.
*   **Sliding Window**: Sequences were created using a sliding window approach with a `WINDOW_SIZE` of 12 months, meaning each prediction uses the previous 12 months' data.
*   **Train-Test Split**: The dataset was split into 80% for training and 20% for testing.

#### 3.2. Exploratory Data Analysis (EDA)

Key insights from EDA:
*   **Data Quality**: No missing values after initial cleaning.
*   **Inflation Range**: Monthly inflation varied from -3.2% to 5.9%.
*   **Stationarity**: The 'Inflation Rate' series was found to be stationary (good for time series modeling), while the 'CPI Index' series was non-stationary.
*   **Seasonality**: Weak but present seasonal patterns were observed in the monthly inflation rates.
*   **Volatility**: Periods of high and low inflation volatility were identified through rolling statistics.

#### 3.3. Baseline RNN Model

A simple `SimpleRNN` model was built with 50 units and a dropout of 0.2. It used only the 'CPI Index' as input. The model was compiled with `Adam` optimizer and `MSE` loss.

#### 3.4. Improved Model with LSTM/GRU & Hyperparameter Tuning

To enhance performance, `LSTM` and `GRU` architectures were compared against `SimpleRNN`. The best performing architecture underwent hyperparameter tuning.

*   **Architecture Comparison**: `GRU` significantly outperformed `SimpleRNN` and `LSTM` in terms of R² score and RMSE.
*   **Multi-Feature Input**: The model was trained with both 'CPI Index' and 'Inflation Rate' as input features.
*   **Hyperparameter Tuning**: A grid search was performed on the `GRU` model, experimenting with:
    *   `units`: [32, 64, 128]
    *   `dropout`: [0.1, 0.2, 0.3]
    *   `learning_rate`: [0.001, 0.0005, 0.0001]
    *   `layers`: [1, 2]

### 4. Key Findings and Results

**Best Model Configuration:**
*   **Architecture**: `GRU`
*   **Units**: 64
*   **Dropout**: 0.2
*   **Learning Rate**: 0.001
*   **Layers**: 1
*   **Features**: CPI Index + Inflation Rate

**Performance Metrics (Test Set):**
*   **RMSE**: 1.1837 CPI points
*   **R² Score**: 0.9980
*   **MAE**: 0.8711 CPI points
*   **MAPE**: 0.46%

**Improvement Over Baseline:**
*   The improved `GRU` model with multi-feature input showed a significant improvement:
    *   **RMSE Reduction**: 91.2% (compared to CPI-only model, actual improvement would be more drastic over the SimpleRNN baseline with single feature)
    *   **R² Improvement**: Substantial increase from the SimpleRNN baseline.
*   **Feature Importance**: Adding the 'Inflation Rate' as an input feature led to a remarkable **91.2% RMSE reduction**, highlighting its importance for accurate CPI forecasting.

### 5. Multi-Step Forecasting (Next 12 Months)

The best-tuned `GRU` model was used to forecast the CPI for the next 12 months following the last date in the dataset (2014-01-01).

*   **Starting CPI (Jan 2014)**: 233.92
*   **Ending Forecasted CPI (Jan 2015)**: 235.95
*   **Expected Annual Growth**: 0.87%

The forecasts show a steady, slight increase in CPI over the next year.

### 6. Conclusion

This project successfully demonstrates the application of RNNs, specifically GRUs, for CPI forecasting. By leveraging multi-feature input and hyperparameter tuning, a highly accurate model was developed, significantly outperforming a basic SimpleRNN baseline. The model provides reliable forecasts and valuable insights into the dynamics of the CPI.

### 7. Future Work and Recommendations

1.  **Multi-Step Output**: Explore models that directly predict multiple future steps rather than an iterative single-step prediction.
2.  **Exogenous Variables**: Incorporate additional macroeconomic indicators (e.g., interest rates, GDP, unemployment rates) that might influence CPI.
3.  **Ensemble Methods**: Combine predictions from multiple models (e.g., different RNNs, ARIMA, Prophet) to improve robustness and accuracy.
4.  **Attention Mechanisms**: Implement attention mechanisms in the RNN architecture to allow the model to focus on the most relevant parts of the input sequence.
5.  **Longer Forecast Horizons**: Experiment with forecasting further into the future (e.g., 24 or 36 months) and assess model performance.
6.  **Real-time Deployment**: Prepare the model for deployment in a real-time environment to provide continuous CPI predictions.

### 8. Project Artifacts

The following files and visualizations are saved in the `/content/drive/MyDrive/RNN_Project/` directory:

*   `eda_time_series.png`: Visualizations of CPI and Inflation trends.
*   `eda_decade_analysis.png`: Inflation rate by decade.
*   `eda_seasonality.png`: Monthly seasonal patterns of inflation.
*   `eda_rolling_stats.png`: Rolling mean and standard deviation of inflation.
*   `training_history.png`: Training and validation loss/MAE for the baseline model.
*   `predictions_visualization.png`: Baseline model's actual vs. predicted CPI.
*   `error_analysis.png`: Baseline model's error distributions.
*   `architecture_comparison.png`: Performance comparison of different RNN architectures.
*   `training_curves_comparison.png`: Training curves for different architectures.
*   `best_model_predictions.png`: Best model's actual vs. predicted CPI, residuals, and error distribution.
*   `final_evaluation_plots.png`: Comprehensive evaluation plots for the final model.
*   `forecast_visualization.png`: Visualization of the 12-month CPI forecast.
*   `best_tuned_model.h5`: The saved Keras model with the best performance.
*   `model_metrics.csv`: Metrics for the baseline model.
*   `architecture_comparison.csv`: Comparison results of different architectures.
*   `hyperparameter_tuning_results.csv`: Detailed results of the hyperparameter tuning.
*   `final_evaluation_metrics.csv`: Comprehensive metrics for the final model.
*   `error_analysis_detailed.csv`: Detailed error analysis for the final model.
*   `forecast_next_12_months.csv`: CSV containing the 12-month CPI forecast.
*   `baseline_model_summary.txt`: Summary of the baseline model.
*   `step4_summary.txt`: Summary of the improved model and tuning process.
*   `FINAL_PROJECT_SUMMARY.txt`: Overall project summary.

*   By KASSAHUN 
