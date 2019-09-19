## Pandas Tips

Reshape your data using array.reshape(1, -1) if it contains a single sample
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
