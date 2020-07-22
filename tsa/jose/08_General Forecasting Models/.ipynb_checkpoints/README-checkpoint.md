___
# General Forecasting Models
> *TSA [Evaluation Metrics](https://github.com/juspreet51/templates/blob/master/TSA_Jose/08_General%20Forecasting%20Models/TSA_Evaluation_Metrics.ipynb)* and [Detailed Explanation](https://medium.com/@joydeepubuntu/common-metrics-for-time-series-analysis-f3ca4b29fe42) <br>
> *ARMA [Family](https://github.com/juspreet51/templates/tree/master/TSA_Jose/08_General%20Forecasting%20Models) Models* <br>
____

# Componenets of TSA
> **Trend:**<br>
> **Seasonality:** <br>
> **Cyclicity:** <br>
> <br>
___

# GRANGER CASUALITY TEST
The GRANGER CASUALITY TEST is a hypothesis test to determine if one TSD is helpful in forecasting the other TSD.

***Cor-relation ≠ Causation***

> <ins>*Correlation*</ins> is a statistical measure (expressed as a number) that describes the size and direction of a relationship between two or more variables. A correlation between variables, however, does not automatically mean that the change in one variable is the cause of the change in the values of the other variable.
>
> <ins>*Causation*</ins> indicates that one event is the result of the occurrence of the other event; i.e. there is a causal relationship between the two events. This is also referred to as cause and effect.
___
# Stationarity
TS having similar statistical measurements(***Mean,Std Dvtn, Variance, Auto-Covariance***) are called as Sationary TS. <br>
And Non-Stationary for not following so.

TSA requires data to be stationary, i.e. any model being applierd to TS, must be have data to be Stationary, as *most of the model assume the data to be stationary*.
Conditions to declare a TS as Stationary TS:-
- Constant Mean <br>
- Constant Variance <br>
- Auto-Covariance must not be dependent on time  <br>

## How to confirm the stationarity of the data?
ADF Test: Having a null-hypothesis that our TS is non-stationary and generating Test Statistics and Critical Values. And if the Test Statistics < Critical value, H<sub>0</sub> can be rejected
___

# ARIMA
## AR and MA model integrated by I
> p= # auto-lags <br>
> d= order of differencing and <br>
> q= order of moving avg

These (p,d,q) values can be achieved by using [Pyramid Auto-Arima](https://github.com/juspreet51/templates/blob/master/TSA_Jose/08_General%20Forecasting%20Models/64_ARIMA.ipynb) library

___
# 10 Common Steps in ARMA family models
```
1) Load dataset

2) Visualize feature to focus upon

3) Call seasonal_decompose on the dataframe's feature and understand TS componnets

4) Use Pyramid Auto-Arima on the dataframe's to know the values of p,d,q (make seasonal=True if felt so in ETS decomposition)

5) Training and Fitting, Model type and orders as per the Auto-Arima's suggestions

6) Print total number of observation and then decide on Train-Test split
trained_model = SARIMAX(train['feature_name'],order=(p,d,q),seasonal_order=(P,D,Q,m))
fit_results = trained_model.fit()
fit_results.summary()

7) Make predections using:
predictions = fit_results.predict(start=start_predections, end=end_predections, dynamic=False, typ="levels or linear").rename("Name of the model")

8) Plot Test and predected values

9) Call metrics like RMSE and R Sq on the predicted values
from sklearn.metrics import r2_score
from statsmodels.tools.eval_measures import rmse

10) Make Unseen Future Forecasts
fcst_model = SARIMAX(df['feature_name'],order=(p,d,q),seasonal_order=(P,D,Q,m))
fcst_fit = fcst_model.fit()
fcst_results = fcst_fit.predict(len(df),len(df)+11,typ='levels').rename('SARIMA(p,d,q)(P,D,Q,m) Forecast')
df['feature_name'].plot()
fcst_results.plot()
```
___
# VAR: 
Usually, the value of y<sub>t</sub> depends upon the predictor varibales, but its vice versa is not so common <br>
However, ___in ceratain cases, e.g. Changes in personal disposable income w.r.t. personal consumption expenditure, predictor and y<sub>t</sub> can affect each other, in such cases, we use Vector Auto_regressive modeling___
> \[𝑦𝑡=𝑐+𝜙1𝑦𝑡−1+𝜙2𝑦𝑡−2+⋯+𝜙𝑝𝑦𝑡−𝑝+𝜀𝑡\]

2-Dimenssional VAR(1) model:
> \[𝑦1,𝑡=𝑐1+𝜙11,1𝑦1,𝑡−1+𝜙12,1𝑦2,𝑡−1+𝜀1,𝑡\] <br>
> \[𝑦2,𝑡=𝑐2+𝜙21,1𝑦1,𝑡−1+𝜙22,1𝑦2,𝑡−1+𝜀2,𝑡\] <br>

