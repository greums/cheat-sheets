# Useful tricks

![](https://images.unsplash.com/photo-1506362802973-bd1717de901c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1437&q=80)
📷 by [Sergi Viladesau](https://unsplash.com/@svi_designs)

## Linting and configuration

### No brainer code formatting

[Black](https://github.com/psf/black) is a Python code formatter. It is PEP 8 compliant and opinionated, thus no configuration is required to run it.

```bash
sudo -H pip install install black
```

Run Black on a Python project directory:
```bash
cd my-awesome-project
black .

All done! ✨ 🍰 ✨
11 files left unchanged.
```

Although Black enforces PEP 8 rules, we can tweak some options via a `~/.config/black`:
```toml
[tool.black]
line-length = 119
```

### Separate development and production requirements

```bash
mkdir requirements
touch requirements/prod.txt
touch requirements/dev.txt
```
```bash
nano requirements/prod.txt

click
guessit
logzero
requests
```
```bash
nano requirements/dev.txt

-r prod.txt
black
pylint
pre-commit
```

Install `dev` dependencies in local environment:
```bash
pip install -r requirements/dev.txt
```

## Lists and dictionaries

### Remove duplicates from a list of dictionaries

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

### Sort list of dictionaries by attribute values

```python
sorted(staff, key=lambda person: person["name"])
```
