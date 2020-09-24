***pip install plotly***
***# Plotly is a pre-requisite before installing cufflinks***

***pip install cufflinks***

```python
import pandas as pd
#importing plotly and cufflinks in offline mode
import cufflinks as cf

import plotly.offline
cf.go_offline()
cf.set_config_file(offline=False, world_readable=True)

df.iplot()
```
