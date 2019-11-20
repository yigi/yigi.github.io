```python
class Employee:
    
    raise_amt = 1.04
    
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

emp_1 = Employee('A', 'B', 50000)
emp_2 = Employee('C', 'D', 60000)
```

_______________________________________________________________

Employee.set_raise_amt(1.05) -> will set the all values to 1.05 including emp_2 due to @classmethod tag

```python
    @classmethod
    def set_raise_amt(cls, amount):
        cls.raise_amt = amount
```
_______________________________________________________________

emp_str_1 = 'John-Doe-70000'
emp_str_2 = 'Steve-Smith-30000'

to remove "-" when constructor called use classmethod tag instead of Employee

```python
    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay)     # was Employee(first, last, pay) ----> cls and Employee is the same thing
```

```python
new_emp_1 = Employee.from_string(emp_str_1)
```

_______________________________________________________________
