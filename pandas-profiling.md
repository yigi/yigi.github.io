**pip install pandas-profiling**

```python
df.profile_report()
```

Extract to HTML

```python
profile = df.profile_report(title='Pandas Profiling Report')
profile.to_file(outputfile="Titanic data profiling.html")
```
