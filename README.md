# README: Understanding Stationarity and Transformations in Time Series

Stationarity in a time series refers to the property where a series's statistical characteristics—such as mean, variance, and autocovariance—remain constant over time. In simpler terms, a stationary time series exhibits consistent behavior throughout its length, without any visible trends, shifts in average level, or changing variability.

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

## Stationarity Tests: ADF, KPSS, and PP

### 1. ADF Test (Augmented Dickey-Fuller)

**Purpose**: Tests for a unit root (i.e., non-stationarity).

**Hypotheses**:
- H₀: Series is **non-stationary**
- H₁: Series is **stationary**

**Interpretation**:
- p-value < 0.05 → Reject H₀ → Series is **stationary**
- p-value > 0.05 → Fail to reject H₀ → Series is **non-stationary**

**Notes**:
- Assumes AR structure
- Includes options for constant and trend terms
- Common go-to test

### 2. KPSS Test (Kwiatkowski–Phillips–Schmidt–Shin)

**Purpose**: Tests for **stationarity**.

**Hypotheses**:
- H₀: Series is **stationary**
- H₁: Series is **non-stationary**

**Interpretation**:
- p-value < 0.05 → Reject H₀ → Series is **non-stationary**
- p-value > 0.05 → Fail to reject H₀ → Series is **stationary**

**Notes**:
- Often used alongside ADF for a more reliable conclusion
- Good for checking trend stationarity

### 3. PP Test (Phillips-Perron)

**Purpose**: Similar to ADF, but more robust to heteroskedasticity and autocorrelation.

**Hypotheses**:
- H₀: Series is **non-stationary**
- H₁: Series is **stationary**

**Interpretation**:
- p-value < 0.05 → Reject H₀ → Series is **stationary**
- p-value > 0.05 → Fail to reject H₀ → Series is **non-stationary**

**Notes**:
- No lag terms needed (unlike ADF)
- Good for noisy, real-world data

