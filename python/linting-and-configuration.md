# Linting and configuration

![](https://images.unsplash.com/photo-1471086569966-db3eebc25a59?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80)
📷 by [Sarah Dorweiler](https://unsplash.com/@sarahdorweiler)

## No brainer code formatting

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

Although Black enforces PEP 8 rules, we can tweak some options via `~/.config/black` file:
```toml
[tool.black]
line-length = 119
```

## Separate development and production requirements

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
