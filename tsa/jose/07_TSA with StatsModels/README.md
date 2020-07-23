# [Another look at measures of forecast accuracy- Rob J.Hyndman and Anne B.Koehlerb1](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)

## Types of Validation Procedures
<font color="green">__MAPE:__</font> Mean Absolute Percentage Error <br>
<font color="green">__MdAPE:__</font> Median Absolute Percentage Error <br>
<font color="green">__sMAPE:__</font> Symmetric Mean Absolute Percentage Error <br>
<font color="green">__sMdAPE:__</font> Symmetric Median Absolute Percentage Error <br>
<font color="green">__MdRAE:__</font> Median Relative Absolute Error <br>
<font color="green">__GMRAE:__</font> Geometric Mean Relative Absolute Error <br>
<font color="green">__MASE:__</font> Mean Absolute Scaled Error <br>

Let $Y_{t}$ denote the observation at time t and $F_{t}$ denote the forecast of $Y_{t}$. Then define the forecast error $e_{t}$ =$Y_{t}$ - $F_{t}$

## Scale-dependent measures
- <font color="green">Mean Square Error (MSE)</font> = mean($e_{t}^2$) <br>
- <font color="green">Root Mean Square (RMSE)</font> =√MSE <br>
- <font color="green">Mean Absolute Error (MAE)</font> = mean(|$e_{t}$|) <br>
- <font color="green">Median Absolute Error</font> = median(|$e_{t}$|)  <br>

## Measures based on percentage errors
The percentage error is given by: $p_{t}$ = 100*$e_{t}/y_{t}$
- <font color="green">MAPE</font> = mean($p_{t}$)
- <font color="green">MdAPE</font> = median($p_{t}$)
- <font color="green">RMPSE</font> = √(mean($p_{t}^2$))
- <font color="green">RMdPSE</font> = √(median($p_{t}^2$)) 
