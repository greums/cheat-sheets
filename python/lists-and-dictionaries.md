# Lists and dictionaries

![](https://images.unsplash.com/photo-1550399105-c4db5fb85c18?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1171&q=80)
📷 by [Ed Robertson](https://unsplash.com/@eddrobertson)

## Merge dictionaries
```python
d1 = {"a": 1, "b": 2}
d2 = {"c": 3, "d": 4}
{**d1, **d2}
```
```python
{"a": 1, "b": 2, "c": 3, "d": 4}
```

Since Python 3.9.0, an [union operator](https://peps.python.org/pep-0584/) has been introduced:
```python
d1 | d2
```

## Remove duplicates from a list of dictionaries
```python
staff = [
    {"id": "00121", "name": "Jim"},
    {"id": "25065", "name": "Dwight"},
    {"id": "78541", "name": "Kevin"},
    {"id": "00145", "name": "Pam"},
    {"id": "05466", "name": "Toby"},
    {"id": "85546", "name": "Angela"},
    {"id": "78455", "name": "Erin"},
    {"id": "00145", "name": "Pam"},
]

list({person["id"]: person for person in staff}.values())
```
## Sort dictionary by keys
```python
d = {2:3, 1:89, 4:5, 3:0}
print({k:v for k,v in sorted(d.items())})
```
```python
{1: 89, 2: 3, 3: 0, 4: 5}
```

## Sort list of dictionaries by attribute values
```python
sorted(staff, key=lambda person: person["name"])
```

## Split list into chunks
```python
my_list = list(range(1, 10))
chunks_size = 3
print(
    [my_list[i:i + chunks_size]
    for i in range(0, len(my_list), chunks_size)]
)
```
```python
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```
