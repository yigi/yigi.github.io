```python
# Global variable
total = 100
 
def test():
    # Local variable
    marks = 19
    print('Marks = ', marks)
    print('Total = ', total)
 
def func1():
    total = 15
 
def func():
    # refer to global variable 'total' inside function
    global total
    if total > 10:
        total = 15
 
def func2():
    global total
    if total > 10:
        total = 15
 
def func3():
    listOfGlobals = globals()
    listOfGlobals['total'] = 11 // globals()['total'] = 11 same
    total = 22
    print('Local Total = ', total)
 
 
def main():
    print('Total = ', total)
    func1()
    print('Total = ', total)
    func()
    print('Total = ', total)
    func2()
    print('Total = ', total)
    func3()
    print('Total = ', total)
 
if __name__ == '__main__':
    main()
```

Total =  100
Total =  100
Total =  15
Total =  15
Local Total =  22
Total =  11
