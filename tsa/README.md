# Templates
Collection of notebooks, code templates and other usefull resources collated during learning (with the seasoning of some really awkward and funny comments and rants)

## Conda Environment Creation and Exporting
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
### Setting a DatetimeIndex Frequency
> Most of the TSA will require you to make sure your index col (most of the time it will be a sequential timestamp) to be in its correct frequency or offset alias<br>
A full list of time series offset aliases can be found in the <a href='http://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases'>official doc</a>.
