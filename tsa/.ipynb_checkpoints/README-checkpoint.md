# `rgba(255, 165, 0, 1)` Templates</font>
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
- Standard Deviation Method
- Interquartile Range Method
- Automatic Outlier Detection

### <font color="yellow">__Method1: Identification and removal of outliers__</font>
```python
Q1 = input_df['sum_gmv'].quantile(0.25)
Q3 = input_df['sum_gmv'].quantile(0.75)
IQR = Q3 - Q1

input_df_treated = input_df[~((input_df < (Q1 - 1.5 * IQR)) |(input_df > (Q3 + 1.5 * IQR))).any(axis=1)]
input_df_treated.head()
```


### <font color="yellow">__Method2: Identification of the indices of outliers and thier imputation__</font>
<font color="teal">___2.1)Outlier Detection___</font> <br>
- Calculate Q1 ( the first Quarter) <br>
- Calculate Q3 ( the third Quartile) <br>
- Find IQR = (Q3 - Q1) <br>
- Find the lower Range = Q1 -(1.5 * IQR) <br>
- Find the upper Range = Q3 + (1.5 * IQR) <br>

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

<font color="teal">___2.2)Outlier Treatment___</font> <br>
We have identified the Outliers in the above give indexes  <br>
Since we can remove any data point, as it will create an absentia in the time-series, we will impute the outliers 
Our choice of imputation will be knn-Imputer as it assigns nulls/nan with the closest knn  <br>

```python
# making outliers as NaN so that they can be treated by KNN Imputer
input_df = input_df_raw.copy()
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
___
