<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Airline Passengers Time Series Forecasting Project</title>
  <style>
    body { font-family: Segoe UI, Arial, sans-serif; margin: 36px; background: #f8f8f8; color: #222; }
    h1 { color: #164194; }
    h2 { color: #18325d; border-bottom: 1px solid #e2e2e2; padding-bottom: 2px;}
    h3 { color: #1b425e; }
    img { max-width: 95%; margin: 22px 0 8px 0; border: 1.5px solid #bbb; box-shadow: 2px 3px 14px #eee; }
    span.figcap { display: block; color: #444; font-size: 0.98em; font-style: italic; margin-bottom: 24px; }
    ul { line-height: 1.7em; }
    .highlight { color: #1a7845; font-weight: bold; }
    .metric { background: #e0f5df; color: #17673e; padding: 2px 7px; border-radius: 3px; font-weight: 500;}
    code { background: #ececec; border-radius: 2px; padding: 0 2px;}
  </style>
</head>
<body>
  <h1>Time Series Forecasting with Decomposition: US Airline Passengers Dataset</h1>
  
  <h2>Project Overview</h2>
  <p>
    This project applies classical time series decomposition and forecasting methods to monthly airline passenger data for the United States in the 1950s. The analysis was conducted as part of a business analytics consultancy exercise, following typical data science project methodology. The objective is to analyze passenger trends and seasonality, build an appropriate forecasting model, and evaluate its predictive accuracy for the year 1960.
  </p>
  
  <h2>Dataset Description</h2>
  <ul>
    <li><b>Source:</b> Public monthly airline passengers data (US, 1949–1960), commonly used in time series analysis.</li>
    <li><b>Variables:</b> Month (Jan–Dec), Year (1949–1960), Number of passengers per month.</li>
    <li><b>Sample Size:</b> 144 months (12 years × 12 months).</li>
    <li><b>File Provided:</b> <code>Air-passengersdata.xlsx</code></li>
  </ul>
  <img src="Monthly Airline Passengers in the US (1949–1959).png" alt="Monthly Passengers">
  <span class="figcap"><b>Figure 1.</b> Monthly Airline Passengers in the US (1949–1959): Clear trend and strong seasonality are visible in the time series.</span>

  <h2>Part A – Executive Summary (for Head of Marketing)</h2>
  <h3>Aim & Objectives</h3>
  <ul>
    <li>To forecast monthly airline passenger numbers using historical data and decomposition techniques.</li>
    <li>To identify and quantify underlying trend and seasonality in the dataset.</li>
    <li>To assess the accuracy of the forecasting model and make recommendations for use in operational planning.</li>
  </ul>

  <h3>Summary of Approach</h3>
  <ul>
      <li>Calculation of 12-month moving averages to smooth the trend.</li>
      <li>Centering the moving averages for seasonality estimation.</li>
      <li>Estimation of monthly seasonal indices using ratio-to-moving-average method.</li>
      <li>Deseasonalizing the series and fitting a linear trend to the deseasonalized data.</li>
      <li>Producing monthly forecasts for 1960, then recomposing to actual scale using the seasonal indices.</li>
      <li>Evaluating model performance with MAE and MSE metrics.</li>
  </ul>

  <h3>Key Results & Visualizations</h3>
  <ul>
    <li><b>Clear upward trend</b> in airline passengers over the decade, with consistent seasonal peaks (summer) and troughs (winter).</li>
    <li><b>Seasonality:</b> 12 distinct seasonal patterns (one for each month); July and August are highest.</li>
    <li><b>Multiplicative decomposition</b> provided best fit due to increasing amplitude of seasonal effects over time.</li>
    <li><b>Forecast accuracy for 1960:</b>
      <ul>
        <li>Mean Absolute Error (MAE): <span class="metric">16.65</span> passengers</li>
        <li>Mean Squared Error (MSE): <span class="metric">580.75</span></li>
      </ul>
    </li>
  </ul>
  <img src="Figure 5. Forecasts for 1960 and Model Error Calculation.png" alt="Forecasts Table">
  <span class="figcap"><b>Figure 5.</b> Forecasted passengers for 1960, actuals, and error metrics.</span>

  <h3>Recommendations</h3>
  <ul>
    <li>Adopt multiplicative time series decomposition for passenger forecasting in operational planning.</li>
    <li>Account for month-specific seasonal effects in resource allocation and marketing campaigns.</li>
    <li>Continue monitoring MAE and MSE for future forecasts as part of a model validation process.</li>
  </ul>

  <h2>Part B – Technical Analysis</h2>
  <h3>Data Preparation & Cleaning</h3>
  <ul>
    <li>Data loaded from Excel, checked for missing/erroneous values (none detected).</li>
    <li>Converted date fields to monthly period for analysis.</li>
  </ul>
  
  <h3>Trend & Seasonality Detection</h3>
  <p>
    <b>Does the data have a trend or seasonal component?</b><br>
    Yes, there is a strong upward trend and annual seasonality.<br>
    <img src="Monthly Airline Passengers in the US (1949–1959).png" alt="Time Series Plot">
    <br>
    <i>Trends: Steady increase over years.<br>
    Seasonality: Annual cycles with 12 seasons (months).</i>
  </p>

  <h3>Moving Average Smoothing and Seasonal Index Calculation</h3>
  <p>
    <b>Approach:</b> Used 12-month centered moving averages to estimate the trend and computed monthly ratios to estimate the seasonal effect.
    <br>
    <img src="Sample calculation of 12-Month Moving Average, Centered Moving Average, and Seasonal Ratio for the airline passenger dataset (first 20 months shown)..png" alt="MA and Seasonal Ratio">
    <span class="figcap"><b>Figure 2.</b> Calculation of 12-Month Moving Average, Centered Moving Average, and Seasonal Ratio.</span>
    <img src="Figure 3. Monthly Seasonal Indices.png" alt="Seasonal Indices">
    <span class="figcap"><b>Figure 3.</b> Monthly Seasonal Indices (multiplicative factors for each month).</span>
  </p>
  
  <h3>Model Selection & Trend Fitting</h3>
  <ul>
    <li><b>Model choice:</b> Multiplicative decomposition (variation in seasonal effect increases with trend).</li>
    <li>Deseasonalized values were regressed against time to find linear trend.</li>
  </ul>
  <img src="Figure 4. Trendline Fit to Deseasonalised Data.png" alt="Trendline Fit">
  <span class="figcap"><b>Figure 4.</b> Scatter plot of deseasonalized values and linear trendline (high R²).</span>

  <h3>Forecasting 1960 & Model Evaluation</h3>
  <ol>
    <li>Used trend equation to forecast deseasonalized values for each month in 1960.</li>
    <li>Re-multiplied by seasonal indices to obtain final monthly forecasts.</li>
    <li>Compared forecasts to actuals to compute <b>error metrics:</b></li>
  </ol>
  <img src="Figure 5. Forecasts for 1960 and Model Error Calculation.png" alt="1960 Forecast Table">
  <span class="figcap">Forecasted passengers, actual values, errors, absolute and squared errors, MAE and MSE.</span>
  <img src="MAE_MSE.png" alt="MAE MSE Table" style="max-width:350px;">
  <span class="figcap">Mean Absolute Error (MAE) = <b>16.65</b>; Mean Squared Error (MSE) = <b>580.75</b></span>

  <h3>Interpretation & Discussion</h3>
  <ul>
    <li>The model tracks the actual data very closely, with very low MAE and MSE relative to monthly volumes (~400–600).</li>
    <li>Seasonal peaks and troughs are well predicted, confirming validity of decomposition.</li>
    <li>Multiplicative approach is appropriate as seasonal amplitude grows with trend.</li>
    <li>Assumption: No structural changes in airline market or major outliers in 1960 (these could affect results).</li>
  </ul>
  
  <h3>Limitations & Assumptions</h3>
  <ul>
    <li>Model does not account for external shocks or irregular events.</li>
    <li>Assumes past seasonality and trend persist in forecast period.</li>
    <li>Data quality and completeness are presumed accurate.</li>
  </ul>
  
  <h3>Technical Conclusion</h3>
  <p>
    Classical decomposition using a multiplicative model provided an accurate and interpretable forecast for airline passengers. The model captures both upward trend and increasing seasonal effect, with error metrics suggesting strong predictive validity. This approach is recommended for similar demand forecasting scenarios in business analytics.
  </p>
</body>
</html>
