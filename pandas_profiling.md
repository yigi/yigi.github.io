# Generate a Detailed Report of your Dataset

```python
import pandas as pd 
import pandas_profiling 

# read the dataset 
data = pd.read_csv('add-your-data-here') 
pandas_profiling.ProfileReport(data)
```
