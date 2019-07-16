### Drop Multiple Columns
 df.drop(column_names, axis = 1, inplace = True)
### Change dtypes (to save memory)
 df[column_int] = df[cloumn_int].astype('int32')
 df[column_float] = df[cloumn_float].astype('float32')
### Convert categorical variable to numerical
 num_encode = { 'column1' : {'YES' : 1, 'NO' : 0},
                'column2' : {'WIN' : 1, 'LOSE' : 0} }
 df.replace( num_encode, inplace = True)
### Check missing data
  df.isnull().sum().sort_values(ascending = False)
### Remove whitespace 
  df[col] = df[col].str.lstrip()
### Convert timestamp (from string to datetime)
  date_str1 = 'Wednesday, June 6, 2018'
  date_str2 = '6/6/18'
  date_str3 = '06-06-2018'

  date_dt1 = datetime.strptime(date_str1, '%A, %B %d, %Y')
  date_dt2 = datetime.strptime(date_str2, '%m/%d/%y')
  date_dt3 = datetime.strptime(date_str3, '%m-%d-%Y')
