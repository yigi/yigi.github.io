```python
try:
  f = open ('missing.txt')
  if f.name == 'missing.txt'
    raise Exception
  var = bad_var
except FileNotFoundError as e:
  print(e)
except Exception as e:
  print(e)
else:
  f.close()
finally:
  print('Thank you')
```
