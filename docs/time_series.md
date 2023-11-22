# Time series memo

This document describes statistical methods that can used for time series analysis, with associated formulas and practical usage with Excel.

## Notations

Here is a list of the notations used thoughout this document

 - $Y_t$: the data value at time $t$ 
 - $F_t$: the forecasted value at time $t$ 
 - $G_t$: the smoothed value at time $t$ 
 - $S_t$: the seasonal coeficient at time $t$
 - ...


## Moving average

Simple and efficient way to smooth the data, equivalent to the convolution of the signal by a window. Weighted moving average allows to control the weight of observation, shaping different types of window.


### Smoothing

When using the moving average method to **smooth** the data (i.e. to soften sudden changes), then a central moving average is computed.
Example to compute a CMA3:

$G_t = Y_{t-1} + Y_{t} + Y_{t+1} $

When the number of coefficient is even, then the formula reads (for CMA4):

$G_t = \frac{1}{2}Y_{t-2} + Y_{t-1} + Y_{t} + Y_{t+1} + \frac{1}{2}Y_{t+2} $

### Forecast

When using the moving average method to **forecast** (i.e. predict future values), then a moving average is computed on past values only!
Example to compute a MA3:

$F_t = Y_{t-3} + Y_{t-2} + Y_{t-1} $

Weights can be applied:

$F_t = w_3 Y_{t-3} + w_2 Y_{t-2} + w_1 Y_{t-1} $

More generally for weighted MA $N$ :

$\displaystyle F_t = \sum_{i=1}^{i=N} w_{i} Y_{t-i}  $


## Simple exponential smoothing

Recuressive way to smooth the data, with exponentially decreasing weights, controlled by one parameter: $\alpha$

> **Simple exponential smoothing is good for data with no trend and no seasonality!**

### Smoothing

When smoothing data, the recursive formula reads:

$G_t = \alpha Y_t + (1-\alpha)G_{t-1}$

with initialization:
$G_0 = Y_0$

### Forecast

When forecasting data, the recursive formula reads:

$F_t = \alpha Y_{t-1} + (1-\alpha)F_{t-1}$

with initialization:
$G_0 = Y_0$

## Double exponential smoothing

The idea is to apply exponential smoothing twice (we use the result of the first smoothing to estimate the trend). In the course we use Brown's linear exponential smoothing. Double exponential smoothing is only used to do forcast.

The recurssive formula reads:

$s'_t = \alpha Y_t + (1-\alpha)s'_{t-1}$

$s''_t = \alpha s'_t + (1-\alpha)s''_{t-1}$

$a_t = 2s'_t - s''_t$

$b_t = \frac{\alpha}{\alpha - 1} (s'_t - s''_t)$

$\displaystyle F_{t+m} = a_t + m b_t$

> **Double exponential smoothing is good for data with trend and no seasonality!**

### Alternative 

Another way to apply exponential smoothing is Holt's linear, which uses 2 parameters ($\alpha$ and $\beta$).

$s_0 = Y_0$

$b_0 = Y_1 - Y_0$

$s_t =  \alpha Y_t + (1-\alpha)(s_{t-1} + b_{t-1})$

$b_t =  \beta (s_t - s_{t-1}) + (1-\beta)b_{t-1}$

$\displaystyle F_{t+m} = s_t + m b_t$ 

## Time series decomposition

To make better forecast, it is usually required to separate the time serie into different parts:

  - The **trend** $T_t$: model the low frequency variation, can be fit to a linear evolution
  - The **seasonality component** $S_t$: model periodic variations. First step is to identify the period, and second step is to estimate $S_t$
  - The **residuals** $R_t$: the random variation, that should have zero mean

There are **two** classical models (we will only focus on them for this course):

 - the **additive** model, where $Y_t = T_t + S_t + R_t$
 - the **multiplicative** model, where $Y_t = T_t \times S_t \times R_t$
 
 But more generally, each component can be either additive or multiplicative.

 ### Step by step methodology

 1. **VIZ**: Plot the time serie, it is very important to take a look at the evolution of what you are studying. Clearly identify sampling frequency (daily, weekly, monthly, quarterly, yearly?).
 1. **TREND**: Identify if there is a trend, and wheter trend is additive or multiplicative (is trend linear?)
 1. **SEASONALITY**: Identify if there is seasonality, and wheter seasonality is additive or multiplicative (is the applitude of period fluctuation increasing with time?) and it's period.
 1. **MODEL**: Build a model (additive or multiplicative for trend/seasonality) for your data and write the associated equation

 From here, methodologies are different for additive or multiplicative models

 #### Additive model

 1. **ESTIMATE TREND**: Estimate the trend $\hat{T_t}$ using central moving average or exponential smoothing. 
 1. **DETREND DATA**= Compute the detrended time serie $D_t = Y_t - \hat{T_t}$ 
 1. **ESTIMATE SEASONAL COMPONENT**: Use $D_t$ to estimate seasonal component. You should average the values of the coeficient for each similar period (for instance, average all january component for yearly seasonality and monthly data). This gives $\hat{S_t}$ which is **periodic**.
 1. **ESTIMATE REMINDER**: Estimate the residuals $R_t = Y_r - \hat{T_t} - \hat{S_t})$
 1. **EVALUATE YOUR MODEL**: Before starting to forecast, plot $Y$, $S$, $T$ and $R$ and make sure your decomposition is sound.
 1. **FORECAST MODEL**: To perform a forecast, we usually use $Y_t = A_t + S_t$, regrouping trend and residuals into $A_t = T_t + R_t$. 
 
    - The seasonal component will remain periodic with the same values. 
    - A linear regression is performed on $A_t$ so $a$ and $b$ are estimated and we have $\hat{A_t} = at + b + R_t$.
    - Since $\hat{R_t}$ has no trend and no seasonality, a simple exponential smoothing can be used to forecast its values $\hat{R_r}$. Values in the future will simply be equal to the last forecast.
 1. **FORECAST**: Now to compute the forecast, just apply $F_t = \hat{A_t} + \hat{S_t}$, which is equivalent to: $\displaystyle F_t = at + b + \hat{R_r} + \hat{S_t}$

When using Excel to build such a model, you should have the folowing columns:
  - $t$ (1 to $N$)
  - $Y$: Data points
  - $\hat{T_t}$: Central moving average with $k$ points (k being the seasonal period)
  - $D$: Detrended time series $Y/\hat{T_t}$
  - $S$: Seasonal component
  - $A$: Seasonally adjusted component $Y - S$
  - $T$: $at + b$ using $a$ and $b$ from the linear regression of $A$ vs $t$
  - $R$: Residuals $Y-S-T$
  - $\hat{R}$: Forecast of $R$ using exponential smoothing with $\alpha$ being either fixed or solved to minimize the standard error.
  - $F$: Forecast of $Y$
  - $SE$: Standard error


 #### Multiplicative model

 1. **ESTIMATE TREND**: Estimate the trend $\hat{T_t}$ using central moving average or exponential smoothing. 
 1. **DETREND DATA**= Compute the detrended time serie $D_t = Y_t / \hat{T_t}$ 
 1. **ESTIMATE SEASONAL COMPONENT**: Use $D_t$ to estimate seasonal component. You should average the values of the coeficient for each similar period (for instance, average all january component for yearly seasonality and monthly data). This gives $\hat{S_t}$ which is **periodic**.
 1. **ESTIMATE REMINDER**: Estimate the residuals $\displaystyle R_t = \frac{Y_r}{\hat{T_t}\hat{S_t}}$
  1. **EVALUATE YOUR MODEL**: Before starting to forecast, plot $Y$, $S$, $T$ and $R$ and make sure your decomposition is sound.
 1. **FORECAST MODEL**: To perform a forecast, we usually use $Y_t = A_t \times S_t$, regrouping trend and residuals into $A_t = T_t \times R_t$. The seasonal component will remain periodic with the same value, and any model for $A_t$ can be used.
 1. **FORECAST**: Now to forecast apply, just apply $F_t = \hat{A_t} + \hat{S_t}$

When using Excel to build such a model, you should have the folowing columns:
  - $t$ (1 to $N$)
  - $Y$: Data points
  - $\hat{T_t}$: Central moving average with $k$ points (k being the seasonal period)
  - $D$: Detrended time series $Y/\hat{T_t}$
  - $S$: Seasonal component
  - $A$: Seasonally adjusted component $Y / S$
  - $T$: $at + b$ using $a$ and $b$ from the linear regression of $A$ vs $t$
  - $R$: Residuals $Y/(S\times T)$
  - $\hat{R}$: Forecast of $R$ using exponential smoothing with $\alpha$ being either fixed or solved to minimize the standard error.
  - $F$: Forecast of $Y$
  - $SE$: Standard error


 #### Example

 Here is an example of a 
 
 ![decomposition](decomposition.png)
