# <font color="gold">__TSA By Jose__</font>



# [Another look at measures of forecast accuracy](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)- Rob J.Hyndman and Anne B.Koehlerb1

<details><summary><font color="gold"><h3><b>
    Types of Validation Procedures:
</b></h3></font></summary>


## <font color="yellow"></font>
<font color="green">__MAPE:__</font> Mean Absolute Percentage Error <br>
<font color="green">__MdAPE:__</font> Median Absolute Percentage Error <br>
<font color="green">__sMAPE:__</font> Symmetric Mean Absolute Percentage Error <br>
<font color="green">__sMdAPE:__</font> Symmetric Median Absolute Percentage Error <br>
<font color="green">__MdRAE:__</font> Median Relative Absolute Error <br>
<font color="green">__GMRAE:__</font> Geometric Mean Relative Absolute Error <br>
<font color="green">__MASE:__</font> Mean Absolute Scaled Error <br>

<font color="yellow">__Others:__</font><br>

- y<sub>i</sub> : **Real value** of the test data
- ŷ<sub>i</sub> : **Predicted value** from our forecast

> here, e<sub>t</sub> = y<sub>i</sub> - ŷ<sub>i</sub> is the ***residual component***

<br> <br> 
<b> Mean Squared Error </b>: <img src="https://latex.codecogs.com/gif.latex?\inline&space;\frac{1}{n}&space;\sum_{i=1}^n&space;(y_{i}&space;-&space;\hat{y}_{i})^2" title="\frac{1}{n} \sum_{i=1}^n (y_{i} - \hat{y}_{i})^2" />

<b> Root Mean Squared Error </b>: <img src="https://latex.codecogs.com/gif.latex?\inline&space;\sqrt{\frac{1}{n}&space;\sum_{i=1}^n&space;(y_{i}&space;-&space;\hat&space;y_{i})^2}" title="\sqrt{\frac{1}{n} \sum_{i=1}^n (y_{i} - \hat y_{i})^2}" />

<b>Mean Absolute Error</b>: <img src="https://latex.codecogs.com/gif.latex?\inline&space;\frac{1}{n}&space;\sum_{i=1}^n&space;|&space;y_{i}&space;-&space;\hat{y}_{i}&space;|" title="\frac{1}{n} \sum_{i=1}^n | y_{i} - \hat{y}_{i} |" />

<b> Mean Absolute Percentage Error </b>: 
<img src="https://latex.codecogs.com/gif.latex?\inline&space;\frac{1}{n}&space;\sum_{i=1}^n&space;\left\lvert{\frac{y_{i}-\hat&space;y}{y_{i}}}\right\rvert" title="\frac{1}{n} \sum_{i=1}^n \left\lvert{\frac{y_{i}-\hat y}{y_{i}}}\right\rvert" /> or <img src="https://latex.codecogs.com/gif.latex?\inline&space;\frac{1}{n}&space;\sum_{i=1}^n&space;\left\lvert{\frac{Act_{i}-&space;F_{i}}{Act_{i}}}\right\rvert" title="\frac{1}{n} \sum_{i=1}^n \left\lvert{\frac{Act_{i}- F_{i}}{Act_{i}}}\right\rvert" />

<b>sMAPE</b>:  <br>
<img src="./imgs/sMAPE_formula_00.png" title="\frac{100\%}{n} \sum_{t=1}^n \frac{|F_{t}-A_{t}|}{(|A_{t}|+|F_{t}|)/2}" />

<br> _Reason for divison by 2 in sMAPE is justified by [Spyros Makridakis]("https://sci-hub.tw/10.1016/0169-2070(93)90079-3")_
MAPE as an accuracy measure can be influenced by some problems:	
- Equal errors above the actual value result in a greater APE (Absolute Percentage Error) than those below the actual value. For instance, when the actual value is 150 and the forecast is 100 (an error of 50) the APE(|(Act-Fcst/Act)|) is: 33%
- However, when the actual is 100 and the forecast 150 the APE is 50%
- This problem can be easily corrected by dividing the error (Act - Fcst) by the average of both Act and Fcst i.e.  (Act + Fcst)/2
- The above formula will provide the APE of 40% in both cases

<b><img src="https://latex.codecogs.com/gif.latex?\inline&space;R^2" title="R^2" /> Squared</b>: Is a measure of how close each datapoint fits the regression line.<br>
So it tells us, how well the regression line predicts the actual value

___python libs import___:
```
from sklearn.metrics import mean_absolute_error, median_absolute_error, mean_squared_error,r2_score
```


    
___  
__Detailed explanation and Formulas in [Notebook](https://github.com/juspreet51/templates/blob/master/tsa/jose/TSA_Evaluation_Metrics.ipynb) and [Blog](https://medium.com/@joydeepubuntu/common-metrics-for-time-series-analysis-f3ca4b29fe42)__
___

<font color="yellow">Let Y<sub>t</sub> denote the observation at time t and F<sub>t</sub> denote the forecast of Y<sub>t</sub>. Then define the forecast error e<sub>t</sub> =Y<sub>t</sub> - F<sub>t</sub></font>

## <font color="purple"><ins>Scale-dependent measures</ins></font>
- <font color="green">__Mean Square Error (MSE)__</font> = mean(e<sub>t</sub><sup>2</sup>) <br>
- <font color="green">__Root Mean Square (RMSE)__</font> =√MSE <br>
- <font color="green">__Mean Absolute Error (MAE)__</font> = mean(|e<sub>t</sub>|) <br>
- <font color="green">__Median Absolute Error__</font> = median(|e<sub>t</sub>|)  <br>

## <font color="purple"><ins>Measures based on percentage errors</ins></font>
The percentage error is given by: <img src="https://latex.codecogs.com/gif.latex?\inline&space;p_{t}&space;=&space;100*e_{t}/y_{t}" title="p_{t} = 100*e_{t}/y_{t}" />
- <font color="green">__MAPE__</font> = mean(p<sub>t</sub>)
- <font color="green">__MdAPE__</font> = median(p<sub>t</sub>)
- <font color="green">__RMPSE__</font> = √(mean(p<sub>t</sub><sup>2</sup>))
- <font color="green">__RMdPSE__</font> = √(median(p<sub>t</sub><sup>2</sup>)) 

## <font color="purple"><ins>Measures based on relative errors</ins></font>
- <font color="green">__Mean Relative Absolute Error (MRAE)__</font> = mean(|r<sub>t</sub>|)
- <font color="green">__Median Relative Absolute Error (MdRAE)__</font> = median(|r<sub>t</sub>|)
- <font color="green">__Geometric Mean Relative Absolute Error (GMRAE)__</font> = gmean(|r<sub>t</sub>|)

## <font color="purple"><ins>Scaled errors</ins></font>
### <font color="orange">Scaled error</font> is define as:  q_{t} = <img src="https://latex.codecogs.com/gif.latex?\inline&space;\frac&space;{e_{t}}{&space;\frac{1}{n-1}&space;\sum_{i=2}^n&space;|Y_{i}-Y_{i-1}|&space;}" title="\frac {e_{t}}{ \frac{1}{n-1} \sum_{i=2}^n |Y_{i}-Y_{i-1}| }" />
- <font color="green">__Mean Absolute Scaled Error (MASE)__</font> = mean(|qt |)
- <font color="green">__Mean Scaled Error (MSE)__</font> = mean(qt)
- <font color="green">__MdASE__</font> = median(|qt |)
- <font color="green">__RMSSE__</font> = √MSE

</details>
 
\*___For more detail, refer to the [paper](https://www.sciencedirect.com/science/article/abs/pii/S0169207006000239)___

___

<details><summary><font color="gold"><h3><b>
    Metrics Libraries For Model Validation:
</b></h3></font></summary>

    
```python
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_error
from statsmodels.tools.eval_measures import rmse

test_dataset_mean =  round(test_dataset.sales.mean(),2); print(f'Test\'s Mean:{test_dataset_mean}')

error_mae = round(mean_absolute_error(test_dataset, predictions),2)
print(f'MAE Error: {error_mae}')

error_mse = mean_squared_error(test_dataset, predictions)
error_rmse = round(np.sqrt(error_mse),2)
print(f'RMSE Error: {error_rmse}')

r2_score_val = round(r2_score(test_dataset, predictions),2)
print(f'R Sq value: {r2_score_val}')

def mean_absolute_percentage_error(y_true, y_pred):
    y_true, y_pred = np.array(y_true), np.array(y_pred)
    return np.mean(np.abs((y_true - y_pred) / y_true)) * 100

mape_val = mean_absolute_percentage_error(test_dataset, predictions)
print(f'Mape Value: {mape_val}')
```
<br> <br>
    
    
</details>

___

<details><summary><font color="gold"><h3><b>
    TensorBoard:
</b></h3></font></summary>

```python
>>> import tensorflow as tf
>>> import datetime

>>> NAME = "lstm_name"

>>> log_dir = "logs_fit_" + datetime.datetime.now().strftime("%Y_%m_%d_%H_%M_%S")
>>> tensorboard_callback = tf.keras.callbacks.TensorBoard(log_dir=log_dir, histogram_freq=1)

    logs_fit_2020_07_29_19_35_35
# open tensorboard: %tensorboard --logdir logs/fit
```

</details>