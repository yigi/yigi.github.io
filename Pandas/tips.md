# Pandas Tips

### Reshape 
your data using array.reshape(1, -1) if it contains a single sample
Exact 1 row. However, column is **unknown**

```python
z.reshape(3, -1)
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])
```
```python
z.reshape(-1, 2)
array([[ 1,  2],
       [ 3,  4],
       [ 5,  6],
       [ 7,  8],
       [ 9, 10],
       [11, 12]])
```

____________________________________________________________________________________

### Build a DataFrame from multiple files (row-wise)
Let's say that your dataset is spread across multiple files, but you want to read the dataset into a single DataFrame.

For example, I have a small dataset of stock data in which each CSV file only includes a single day. Here's the first day:

```python
pd.read_csv('data/stocks1.csv')

       Date	       Close	Volume	       Symbol
0	2016-10-03	31.50	14070500	CSCO
1	2016-10-03	112.52	21701800	AAPL
2	2016-10-03	57.42	19189500	MSFT


       Date	       Close	Volume	       Symbol
0	2016-10-04	113.00	29736800	AAPL
1	2016-10-04	57.24	20085900	MSFT
2	2016-10-04	31.35	18460400	CSCO
```

```python
from glob import glob
```

You can pass a pattern to glob(), including wildcard characters, and it will return a list of all files that match that pattern.

In this case, glob is looking in the "data" subdirectory for all CSV files that start with the word "stocks":

```python
stock_files = sorted(glob('data/stocks*.csv'))
stock_files
['data/stocks1.csv', 'data/stocks2.csv', 'data/stocks3.csv']
```

glob returns filenames in an arbitrary order, which is why we sorted the list using Python's built-in sorted() function.

We can then use a generator expression to read each of the files using read_csv() and pass the results to the concat() function, which will concatenate the rows into a single DataFrame:

```python
pd.concat((pd.read_csv(file) for file in stock_files))
```

**Unfortunately**, there are now duplicate values in the index. To avoid that, we can tell the concat() function to ignore the index and instead use the default integer index:

```python
pd.concat((pd.read_csv(file) for file in stock_files), ignore_index=True)
```

____________________________________________________________________________________

### Concatenate DataFrames

```python
df_row = pd.concat([df1, df2])

df_row
       id	Feature1	Feature2
0	1	A	       B
1	2	C	       D
2	3	E	       F
3	4	G	       H
4	5	I	       J
0	1	K	       L
1	2	M	       N
2	6	O	       P
3	7	Q	       R
4	8	S	       T
```

You can notice that the two DataFrames df1 and df2 are now concatenated into a single DataFrame df_row along the row. However, the row labels seem to be wrong! If you want the row labels to adjust automatically according to the join, you will have to set the argument ignore_index as True while calling the concat() function:

```python
df_row_reindex = pd.concat([df1, df2], ignore_index=True)
```

pandas also provides you with an option to label the DataFrames, after the concatenation, with a key so that you may know which data came from which DataFrame

```python
frames = [df1,df2]
df_keys = pd.concat(frames, keys=['x', 'y'])

df_keys
                            id	Feature1	Feature2
x             0	       1	A	       B
              1	       2	C	       D
              2	       3	E	       F
              3	       4	G	       H
              4	       5	I	       J
y             0	       1	K	       L
              1	       2	M	       N
              2	       6	O	       P
              3	       7	Q	       R
              4	       8	S	       T
```

___________________________________________________________________________________

### Merge DataFrames

It might happen that the column on which you want to merge the DataFrames have different names (unlike in this case). For such merges, you will have to specify the arguments left_on as the left DataFrame name and right_on as the right DataFrame name, like :

```python
df_merge_difkey = pd.merge(df_row, df3, left_on='id', right_on='id')

df_merge_difkey
       id	Feature1	Feature2	Feature3
0	1	A	       B	       12
1	1	K	       L	       12
2	2	C	       D	       13
3	2	M	       N	       13
4	3	E	       F	       14
5	4	G	       H	       15
6	5	I	       J	       16
7	7	Q	       R	       17
8	8	S	       T	       15
```

```python
You can also append rows to a DataFrame by passing a Series or dict to append() function which returns a new DataFrame:

add_row = pd.Series(['10', 'X1', 'X2', 'X3'],
                    index=['id','Feature1', 'Feature2', 'Feature3'])

df_add_row = df_merge_col.append(add_row, ignore_index=True)

df_add_row
```

___________________________________________________________________________________


### Full Outer Join
The FULL OUTER JOIN combines the results of both the left and the right outer joins. The joined DataFrame will contain all records from both the DataFrames and fill in NaNs for missing matches on either side. You can perform a full outer join by specifying the how argument as outer in the merge() function:

```python
df_outer = pd.merge(df1, df2, on='id', how='outer')

df_outer
```

```python
       id	Feature1_x	Feature2_x	Feature1_y	Feature2_y
0	1	A	       B	       K	       L
1	2	C	       D	       M	       N
2	3	E	       F	       NaN	       NaN
3	4	G	       H	       NaN	       NaN
4	5	I	       J	       NaN	       NaN
5	6	NaN	       NaN	       O	       P
6	7	NaN	       NaN	       Q	       R
7	8	NaN	       NaN	       S	       T
```

df_suffix = pd.merge(df1, df2, left_on='id',right_on='id',how='outer',suffixes=('_left','_right'))

df_suffix

id	Feature1_left	   Feature2_left     Feature1_right	Feature2_right

https://image.slidesharecdn.com/sqlouterjoins-131118145750-phpapp01/95/sql-outer-joins-for-fun-and-profit-8-638.jpg?cb=1384786728


### Inner Join
produces only the set of records that match in both DataFrame A and DataFrame B. You have to pass inner in the how argument of merge() function to do inner join:

```python
df_inner = pd.merge(df1, df2, on='id', how='inner')

df_inner
       id	Feature1_x	Feature2_x	Feature1_y	Feature2_y
0	1	A	       B	       K	       L
1	2	C	       D	       M	       N
```

### Testing Data With Time Series

```python

num_rows = 365 * 24
pd.util.testing.makeTimeDataFrame(num_rows, freq='H')
...
...
...
num_cols = 2
cols = [ 'sales','customer' ]
df = pd.DataFrame( np.random.randint (1,20,size = (num_rows,num_cols)), columns = cols)
df.index = pd.util.testing.makeDateIndex(num_rows, freq = 'H')
```
