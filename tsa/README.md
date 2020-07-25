# <font color="gold">__Templates__</font>
Collection of notebooks, code templates and other usefull resources collated during learning (with the seasoning of some really awkward and funny comments and rants)

## <font color="purple"><ins>Conda Environment Creation and Exporting</ins></font>
```
> conda info
> conda update conda
> conda install PACKAGENAME 
> conda update PACKAGENAME 

> conda create --name ENVNAME python=3.6   # Here new environment is named ENVNAME, install Python 3.6
> conda create --clone ENVNAME --name NEWENV # Exact copy of existing environment
> conda env list 
> conda list --name ENVNAME
> conda activate env_name

> conda env export --name ENVNAME > envname.yml
> conda env create --file envname.ym
> conda env create # Create an environment from the file named environment.yml in the current director

> conda remove --name ENVNAME --all # Delete an entire environment
```
## <font color="purple"><ins>Setting a DatetimeIndex Frequency</ins></font>
> Most of the TSA will require you to make sure your index col (most of the time it will be a sequential timestamp) to be in its correct frequency or offset alias<br>
A full list of time series offset aliases can be found in the <a href='http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases'>official doc</a>.

___
# <font color="purple">__<ins>Outlier Detection and Treatment</ins>:__</font>
- Interquartile Range Method
- Automatic Outlier Detection

### <font color="yellow">__Method1: Interquartile Range Method__</font>
- Calculate Q1 ( the first Quarter) <br>
- Calculate Q3 ( the third Quartile) <br>
- Find IQR = (Q3 - Q1) <br>
- Find the lower Range = Q1 -(1.5 * IQR) <br>
- Find the upper Range = Q3 + (1.5 * IQR) <br>

#### <font color="Red">__1.1)Identification and Removal__</font>
```python
Q1 = input_df['sum_gmv'].quantile(0.25)
Q3 = input_df['sum_gmv'].quantile(0.75)
IQR = Q3 - Q1

input_df_treated = input_df[~((input_df < (Q1 - 1.5 * IQR)) |(input_df > (Q3 + 1.5 * IQR))).any(axis=1)]
input_df_treated.head()
```


#### <font color="Red">__1.2)Outlier Identification and Imputation__</font>
<font color="teal">__1.2.1)Identification__</font> <br>
```python
def outlier_detection(datacolumn):
    sorted(datacolumn)
    Q1,Q3 = np.percentile(datacolumn , [25,75])
    IQR = Q3 - Q1
    lower_range = Q1 - (1.5 * IQR)
    upper_range = Q3 + (1.5 * IQR)
    
    return lower_range,upper_range

lowerbound,upperbound = outlier_detection(input_df_raw['sales'])

outliers = input_df_raw[(input_df_raw['sales'] < lowerbound) | (input_df_raw['sales'] > upperbound)]
print(outliers)
```

<font color="teal">__2.2)Imputation__</font> <br>
We have identified the Outliers in the above give indexes  <br>
Since we can remove any data point, as it will create an absentia in the time-series, we will impute the outliers 
Our choice of imputation will be knn-Imputer as it assigns nulls/nan with the closest knn  <br>

```python
# making outliers as NaN so that they can be treated by KNN Imputer
input_df.loc[outliers.index, 'sales']=np.nan
input_df

from sklearn.impute import SimpleImputer

impNumeric = SimpleImputer(missing_values=np.nan, strategy='mean')
impCategorical = SimpleImputer(missing_values=np.nan, strategy='most_frequent')

# Fitting the data to the imputer object 
impNumeric = impNumeric.fit(input_df[['sales']])
  
# Imputing the data      
input_df['sales'] = impNumeric.transform(input_df[['sales']])
input_df

input_df.boxplot(column=['sales']);
```

### <font color="yellow">__Method2:Automatic Outlier Detection__</font>
<font color="teal">__2.1)Isolation Forest__</font> <br>
- iForest for short, is a tree-based anomaly detection algorithm
- Contamination is used to help estimate the number of outliers in the dataset
> This is a value between 0.0 and 0.5 and by default is set to 0.1
```python
# identify outliers in the training dataset
iso = IsolationForest(contamination=0.1)
yhat = iso.fit_predict(X_train)
```


- Once identified, we can remove the outliers from the training dataset
```python
# select all rows that are not outliers
mask = yhat != -1
X_train, y_train = X_train[mask, :], y_train[mask]
```

> __COMPLETE CODE__

```python
# evaluate model performance with outliers removed using isolation forest
from pandas import read_csv
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import IsolationForest
from sklearn.metrics import mean_absolute_error
# load the dataset
url = 'https://raw.githubusercontent.com/jbrownlee/Datasets/master/housing.csv'
df = read_csv(url, header=None)
# retrieve the array
data = df.values
# split into input and output elements
X, y = data[:, :-1], data[:, -1]
# split into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=1)
# summarize the shape of the training dataset
print(X_train.shape, y_train.shape)
# identify outliers in the training dataset
iso = IsolationForest(contamination=0.1)
yhat = iso.fit_predict(X_train)
# select all rows that are not outliers
mask = yhat != -1
X_train, y_train = X_train[mask, :], y_train[mask]
# summarize the shape of the updated training dataset
print(X_train.shape, y_train.shape)
# fit the model
model = LinearRegression()
model.fit(X_train, y_train)
# evaluate the model
yhat = model.predict(X_test)
# evaluate predictions
mae = mean_absolute_error(y_test, yhat)
print('MAE: %.3f' % mae)
```



<font color="teal">__2.2)Minimum Covariance Determinant__</font> <br>
- If the input variables have a Gaussian distribution, then simple statistical methods can be used to detect outliers
- If the dataset has two input variables and both are Gaussian, then the feature space forms a multi-dimensional Gaussian and knowledge of this distribution can be used to identify values far from the distribution.
- This approach can be generalized by defining a hypersphere (ellipsoid) that covers the normal data, and data that falls outside this shape is considered an outlier
- An efficient implementation of this technique for multivariate data is known as the Minimum Covariance Determinant, or MCD for short
```python
...
# identify outliers in the training dataset
ee = EllipticEnvelope(contamination=0.01)
yhat = ee.fit_predict(X_train)
```
<br>

- Once identified, we can remove the outliers from the training dataset
```python
# select all rows that are not outliers
mask = yhat != -1
X_train, y_train = X_train[mask, :], y_train[mask]
```
<br><br>

> __COMPLETE CODE__

```python
# evaluate model performance with outliers removed using elliptical envelope
from pandas import read_csv
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.covariance import EllipticEnvelope
from sklearn.metrics import mean_absolute_error
# load the dataset
url = 'https://raw.githubusercontent.com/jbrownlee/Datasets/master/housing.csv'
df = read_csv(url, header=None)
# retrieve the array
data = df.values
# split into input and output elements
X, y = data[:, :-1], data[:, -1]
# split into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=1)
# summarize the shape of the training dataset
print(X_train.shape, y_train.shape)
# identify outliers in the training dataset
ee = EllipticEnvelope(contamination=0.01)
yhat = ee.fit_predict(X_train)
# select all rows that are not outliers
mask = yhat != -1
X_train, y_train = X_train[mask, :], y_train[mask]
# summarize the shape of the updated training dataset
print(X_train.shape, y_train.shape)
# fit the model
model = LinearRegression()
model.fit(X_train, y_train)
# evaluate the model
yhat = model.predict(X_test)
# evaluate predictions
mae = mean_absolute_error(y_test, yhat)
print('MAE: %.3f' % mae)
```


<font color="teal">__2.3)One-Class SVM__</font> <br>
- When modeling one class, the algorithm captures the density of the majority class and classifies examples on the extremes of the density function as outliers. This modification of SVM is referred to as One-Class SVM
- Although SVM is a classification algorithm and One-Class SVM is also a classification algorithm, it can be used to discover outliers in input data for both regression and classification datasets
- The class provides the “nu” argument that specifies the approximate ratio of outliers in the dataset, which defaults to 0.1
```python
...
# identify outliers in the training dataset
ee = OneClassSVM(nu=0.01)
yhat = ee.fit_predict(X_train)
```
<br><br>

> __COMPLETE CODE__

```python
# evaluate model performance with outliers removed using one class SVM
from pandas import read_csv
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.svm import OneClassSVM
from sklearn.metrics import mean_absolute_error
# load the dataset
url = 'https://raw.githubusercontent.com/jbrownlee/Datasets/master/housing.csv'
df = read_csv(url, header=None)
# retrieve the array
data = df.values
# split into input and output elements
X, y = data[:, :-1], data[:, -1]
# split into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=1)
# summarize the shape of the training dataset
print(X_train.shape, y_train.shape)
# identify outliers in the training dataset
ee = OneClassSVM(nu=0.01)
yhat = ee.fit_predict(X_train)
# select all rows that are not outliers
mask = yhat != -1
X_train, y_train = X_train[mask, :], y_train[mask]
# summarize the shape of the updated training dataset
print(X_train.shape, y_train.shape)
# fit the model
model = LinearRegression()
model.fit(X_train, y_train)
# evaluate the model
yhat = model.predict(X_test)
# evaluate predictions
mae = mean_absolute_error(y_test, yhat)
print('MAE: %.3f' % mae)
```

___
