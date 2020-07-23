# [Another look at measures of forecast accuracy- Rob J.Hyndman and Anne B.Koehlerb1](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)

## <font color="yellow">Types of Validation Procedures</font>
<font color="green">__MAPE:__</font> Mean Absolute Percentage Error <br>
<font color="green">__MdAPE:__</font> Median Absolute Percentage Error <br>
<font color="green">__sMAPE:__</font> Symmetric Mean Absolute Percentage Error <br>
<font color="green">__sMdAPE:__</font> Symmetric Median Absolute Percentage Error <br>
<font color="green">__MdRAE:__</font> Median Relative Absolute Error <br>
<font color="green">__GMRAE:__</font> Geometric Mean Relative Absolute Error <br>
<font color="green">__MASE:__</font> Mean Absolute Scaled Error <br>

<font color="yellow">Let Y<sub>t</sub> denote the observation at time t and F<sub>t</sub> denote the forecast of Y<sub>t</sub>. Then define the forecast error e<sub>t</sub> =Y<sub>t</sub> - F<sub>t</sub></font>

## Scale-dependent measures
- <font color="green">__Mean Square Error (MSE)__</font> = mean(e<sub>t</sub><sup>2</sup>) <br>
- <font color="green">__Root Mean Square (RMSE)__</font> =√MSE <br>
- <font color="green">__Mean Absolute Error (MAE)__</font> = mean(|e<sub>t</sub>|) <br>
- <font color="green">__Median Absolute Error__</font> = median(|e<sub>t</sub>|)  <br>

## Measures based on percentage errors
The percentage error is given by: $p_{t}$ = 100*$e_{t}/y_{t}$
- <font color="green">__MAPE__</font> = mean(p<sub>t</sub>)
- <font color="green">__MdAPE__</font> = median(p<sub>t</sub>)
- <font color="green">__RMPSE__</font> = √(mean(p<sub>t</sub><sup>2</sup>))
- <font color="green">__RMdPSE__</font> = √(median(p<sub>t</sub><sup>2</sup>)) 

## Measures based on relative errors
- <font color="green">__Mean Relative Absolute Error (MRAE)__</font> = mean(|r<sub>t</sub>|)
- <font color="green">__Median Relative Absolute Error (MdRAE)__</font> = median(|r<sub>t</sub>|)
- <font color="green">__Geometric Mean Relative Absolute Error (GMRAE)__</font> = gmean(|r<sub>t</sub>|)

## Scaled errors
### <font color="orange">Scaled error</font> is define as:  q<sub>t</sub> = $\frac {e_{t}}{ \frac{1}{n-1} \sum_{i=2}^n |Y_{i}-Y_{i-1}| } $
- <font color="green">__Mean Absolute Scaled Error (MASE)__</font> = mean(|qt |)
- <font color="green">__Mean Scaled Error (MSE)__</font> = mean(qt)
- <font color="green">__MdASE__</font> = median(|qt |)
- <font color="green">__RMSSE__</font> = √MSE
 
for more detail, refer to the [paper](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)