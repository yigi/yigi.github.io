
```python
list = [1,2,3,4,5,6,7]

my_list = filter (lambda x: x % 2 == 0 , list) 

or 

my_list = [ n for n in list if n % 2 == 0]
```

______________________________________________________________

```python
output -> 0 a 1 a 2 a 0 b 1 b 2 b

letter = 'ab'
nums = [1,2]

my_list = [ (num,let) for let in letter for num in nums ]
```

______________________________________________________________

```python
list1 = ['a','b','c']
list2 = ['A','B','C']

my_list = { l1:l2  for l1,l2 in zip(list1,list2) if l1 != 'a' }

```
