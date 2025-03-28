# README: Understanding Stationarity and Transformations in Time Series

## Why is Stationarity Important in Time Series?

**Stationarity** is crucial in time series analysis because many statistical models (like ARIMA, SARIMA) assume that the time series has a constant mean, variance, and autocorrelation over time. This helps in creating reliable, interpretable, and accurate models.

### Types of Stationarity

- **Strict Stationarity**: The entire distribution does not change over time (rare in practice).
- **Weak (Covariance) Stationarity**: Mean, variance, and autocovariance are constant over time (common and usually sufficient).

### Importance of Stationarity:

1. **Predictability**: Easier to forecast when statistical properties are constant.
2. **Model Accuracy**: Models assuming stationarity perform better.
3. **Validity of Statistical Tests**: Tests like ADF, KPSS, and Granger causality rely on stationarity.
4. **Interpretability**: Stationary series are easier to analyze and interpret.

---

## How to Make a Series Stationary

### 1. Differencing: Stabilizing the Mean / Trend

**Goal**: Remove trends or seasonality (changing mean over time).

**What is Differencing?**
Subtract the previous value from the current one:

```
Y'_t = Y_t - Y_{t-1}
```

**Types:**

- First-order differencing: Removes linear trends
- Second-order differencing: Removes quadratic trends
- Seasonal differencing: `Y_t - Y_{t-m}` to handle seasonal components

**Example:**
Original: `[100, 105, 110, 115]`  → Trend = +5
First Difference: `[5, 5, 5]` → Constant mean → Stationary

### 2. Log Transformation: Stabilizing the Variance

**Goal**: Handle changing variance (heteroskedasticity), often due to exponential growth.

**What is Log Transformation?**
Apply the log function to each point:

```
Y'_t = log(Y_t)
```

**Example:**
Original: `[10, 100, 1000, 10000]`
Log Transformed: `[1, 2, 3, 4]` → Reduced variance

### 3. Log + Differencing: Handle Multiplicative Trends

You can combine both to handle more complex patterns:

```
Y''_t = log(Y_t) - log(Y_{t-1}) = log(Y_t / Y_{t-1})
```

This is also known as **log returns** and is commonly used in finance.

---

##

