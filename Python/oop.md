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

```python
@staticmethod
    def staticmethodFunc():
        print('Hello staticmethodFunc!')
```

Static methods, much like class methods, are methods that are bound to a class rather than its object.

They do not require a class instance creation. So, are not dependent on the state of the object.

The difference between a static method and a class method is:

Static method knows nothing about the class and just deals with the parameters.
Class method works with the class since its parameter is always the class itself.
They can be called both by the class and its object.

```python
Class.staticmethodFunc()
```

_______________________________________________________________

```python
class Developer(Employee):
    raise_amt = 1.10

    def __init__(self, first, last, pay, prog_lang):
        super().__init__(first, last, pay)
        self.prog_lang = prog_lang
```
_______________________________________________________________

Dunder

```python
    def __repr__(self):
        return "Employee('{}', '{}', {})".format(self.first, self.last, self.pay)

    def __str__(self):
        return '{} - {}'.format(self.fullname(), self.email)
 ```
 
 You can use add method (by changing) to sum Employee's salaries.
 
 ```python
    def __add__(self,other):
        return self.pay + other.pay
 ```
 ----> print( emp_1 + emp_2 )
-----> 1100000

_______________________________________________________________

```python
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        print('Getting name')
        return self._name

    @name.setter
    def name(self, value):
        print('Setting name to ' + value)
        self._name = value

    @name.deleter
    def name(self):
        print('Deleting name')
        del self._name

p = Person('Adam')
print('The name is:', p.name)

p.name = 'John'

del p.name
 ```
 
 
