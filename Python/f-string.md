Every f-string statement consists of two parts, one is character f or F, and the next one is a string which we want to format. The string will be enclosed in single, double, or triple quotes.

```python
# declaring variables
name = "Datacamp"
type_of_company = "Educational"

# enclose your variable within the {} to display it's value in the output
print(f"{name} is an {type_of_company} company.")
```

```python
person = {"name": "John", "age": 19}
print(f"{person['name']} is {person['age']} years old.")
```
