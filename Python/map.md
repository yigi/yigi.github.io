```python
student = { 'name' : 'John', 'course' : ['A','B']}
print( student.get('phone','Not Found')

```
> Not Found

Change the values with update -> student.update...

Delete the value with del -> del student['name'] # it returns the deleted item too

_______________________________________________________________________________

to iterate 

```python
for key,value in student.items():
  print key,value

```
