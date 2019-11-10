Add a list to a list

```python
list1 = [a,b,c]

list2 = [d, e]

list1.extend(list2)
```

list1.append -> appends complete list as a value [a,b,c,[d,e]]

_____________________________________________________________________________________________________

Python uses Timsort

```python
list1 = [a,b,c]

list1.sort(reverse = True) #default False
```

sorted(list1) not actually sorts the list. It returns a sorted list.
_____________________________________________________________________________________________________

```python
for index, character in enumarate(list1):
  print(index,character)
```

0 a 

1 b 

2 c
_____________________________________________________________________________________________________

Sets throw away duplicates and order is not important.

Use {} instead of [] or ()

```python
set1 = {a,b,c}

set2 = {c, d}

print(set1.intersection(set2))
print(set1.difference(set2))
print(set1.union(set2))
```

{'c'}

{'a','b'}

{'a','b','c','d'}

_____________________________________________________________________________________________________
