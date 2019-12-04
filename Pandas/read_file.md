```python

5 useful "read_csv" parameters that are often overlooked:

➡️ names: specify column names
➡️ usecols: which columns to keep
➡️ dtype: specify data types
➡️ nrows: # of rows to read
➡️ na_values: strings to recognize as NaN#Python 
➡️ header = row number of header (start counting at 0)
➡️ skiprows = list of row numbers to skip
```
___________________________________________________________________________

```python

Two easy ways to reduce DataFrame memory usage:
1. Only read in columns you need
2. Use 'category' data type with categorical data.

Example:
df = http://pd.read _csv('file.csv', usecols=['A', 'C', 'D'], dtype={'D':'category'})

```

___________________________________________________________________________


```python
Build dataframe from multiple files

from glob import glob

files = sorted(glob('file*.csv'))
pd.concat((pd.read_csv(file) for file in files),ignore_index = True)
...
...
...
pd.concat((pd.read_csv(file).assign(filename = file) for file in files),ignore_index = True)
```

