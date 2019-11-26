instead of using print use logging.debug

```python
import logging
logging.basicConfig(filename='test.log', level=logging.DEBUG,
                    format='%(asctime)s:%(levelname)s:%(message)s')
logging.debug("...")
```

or use 

-debug
-info
-error
-critical

____________________________________________________________________________
