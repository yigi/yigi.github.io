## *args - *kwargs

```python
def adder(*args):
    result = 0
    for arg in args:
        result+=arg
    return result
```
What *args does is that it takes all your passed arguments and provides a variable length argument list to the function which you can use as you want.
Now you can use the same function as follows:

```python
adder(1,2)
adder(1,2,3)
adder(1,2,5,7,8,9,100)
```
and so on.

Can I use *args? Guess not since name and age order is essential. We don’t want to write “28 is Michael years old”.
Come **kwargs in the picture.
```python
def myprint(**kwargs):
    for k,v in kwargs.items():
        print(f'{k} is {v} years old')
```
You can call this function using:
```python
myprint(Sansa=20,Tyrion=40,Arya=17)
```


## decorators
Decorators are functions that wrap another function thus modifying its behavior.
