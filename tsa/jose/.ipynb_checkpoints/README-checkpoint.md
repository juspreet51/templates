# [Another look at measures of forecast accuracy- Rob J.Hyndman and Anne B.Koehlerb1](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)

## <font color="yellow">Types of Validation Procedures</font>
<font color="green">__MAPE:__</font> Mean Absolute Percentage Error <br>
<font color="green">__MdAPE:__</font> Median Absolute Percentage Error <br>
<font color="green">__sMAPE:__</font> Symmetric Mean Absolute Percentage Error <br>
<font color="green">__sMdAPE:__</font> Symmetric Median Absolute Percentage Error <br>
<font color="green">__MdRAE:__</font> Median Relative Absolute Error <br>
<font color="green">__GMRAE:__</font> Geometric Mean Relative Absolute Error <br>
<font color="green">__MASE:__</font> Mean Absolute Scaled Error <br>

<font color="yellow">Let $Y_{t}$ denote the observation at time t and $F_{t}$ denote the forecast of $Y_{t}$. Then define the forecast error $e_{t}$ =$Y_{t}$ - $F_{t}$</font>

## Scale-dependent measures
- <font color="green">__Mean Square Error (MSE)__</font> = mean($e_{t}^2$) <br>
- <font color="green">__Root Mean Square (RMSE)__</font> =√MSE <br>
- <font color="green">__Mean Absolute Error (MAE)__</font> = mean(|$e_{t}$|) <br>
- <font color="green">__Median Absolute Error__</font> = median(|$e_{t}$|)  <br>

## Measures based on percentage errors
The percentage error is given by: $p_{t}$ = 100*$e_{t}/y_{t}$
- <font color="green">__MAPE__</font> = mean($p_{t}$)
- <font color="green">__MdAPE__</font> = median($p_{t}$)
- <font color="green">__RMPSE__</font> = √(mean($p_{t}^2$))
- <font color="green">__RMdPSE__</font> = √(median($p_{t}^2$)) 

## Measures based on relative errors
- <font color="green">__Mean Relative Absolute Error (MRAE)__</font> = mean(|$r_{t}$|)
- <font color="green">__Median Relative Absolute Error (MdRAE)__</font> = median(|rt |)
- <font color="green">__Geometric Mean Relative Absolute Error (GMRAE)__</font> = gmean(|rt |)
