# Time series

This document describes statistical methods that can used for time series smoothing and forecasting, with associated formulas and practical usage with Excel.

## Notations

Here is a list of the notations used throughout this document

 - $Y_t$: the data value at time $t$ 
 - $F_t$: the forecasted value at time $t$ 
 - $G_t$: the smoothed value at time $t$ 
 - $S_t$: the seasonal coefficient at time $t$
 - $R_t$: the residual at time $t$
 - $T_t$: the trend at time $t$


## Moving average

Simple and efficient way to smooth the data, equivalent to the convolution of the signal by a window. Weighted moving average allows to control the weight of observation, shaping different types of window.

### Smoothing

When using the moving average method to **smooth** the data (i.e. to soften sudden changes), then a central moving average is computed.
Example to compute a CMA3:

$\displaystyle G_t = \frac{Y_{t-1} + Y_{t} + Y_{t+1}}{3} $

When the number of coefficient is even, then the formula reads (for CMA4):

$\displaystyle G_t = \frac{\frac{1}{2}Y_{t-2} + Y_{t-1} + Y_{t} + Y_{t+1} + \frac{1}{2}Y_{t+2}}{3} $

### Forecast

When using the moving average method to **forecast** (i.e. predict future values), then a moving average is computed on past values only!
Example to compute a MA3:

$\displaystyle F_t = \frac{Y_{t-3} + Y_{t-2} + Y_{t-1}}{3} $

Weights can be applied:

$\displaystyle F_t = \frac{w_3 Y_{t-3} + w_2 Y_{t-2} + w_1 Y_{t-1}}{w_1 + w_2 + w_3} $

More generally for weighted MA $N$ :

$\displaystyle F_t = \frac{1}{\sum_{i=1}^{N} w_i} ~~\sum_{i=1}^{N} w_{i} Y_{t-i}  $


## Simple exponential smoothing

Recursive way to smooth the data, with exponentially decreasing weights, controlled by one parameter: $\alpha$

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

The idea is to apply exponential smoothing twice (we use the result of the first smoothing to estimate the trend). In the course we use Brown's linear exponential smoothing. Double exponential smoothing is only used to do forecast.

The recursive formula reads:

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
