# Time series memo

This document describes statistical methods that can used for time series analysis, with associated formulas and practical usage with Excel.

## Notations

Here is a list of the notations used thoughout this document

 - $Y_t$: the data value at time $t$ 
 - $S_t$: the seasonal coeficient at time $t$
 - ...


## Moving average

Simple and efficient way to smooth the data, equivalent to the convolution of the signal by a window. 

### Smoothing

When using the moving average method to *smooth* the data (i.e. to soften sudden changes), then a central moving average is computed.
Example to compute a MA3:


### Forecast

When using the moving average method to *forecast* (i.e. predict future values), then a moving average is computed on past values only!
Example to compute a MA3:

## Simple exponential smoothing

Recuressive way to smooth the data, with exponentially decreasing weights.

### Smoothing

### Forecast
