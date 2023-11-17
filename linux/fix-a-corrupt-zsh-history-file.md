# Fix a corrupt zsh history file

## Symptom

When starting `zsh`, an error occurs:

```bash
zsh: corrupt history file /home/go/.zsh_history
```

## How to fix it

```bash
cd ~
mv .zsh_history .zsh_history_bad
strings .zsh_history_bad > .zsh_history
fc -R .zsh_history
rm ~/.zsh_history_bad
```
