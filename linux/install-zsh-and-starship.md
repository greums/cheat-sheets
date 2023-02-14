# Install Zsh and Starship

Zsh is an extended Bourne shell with many improvements, including some features of Bash, ksh, and tcsh. It can be further improved by [Oh My Zsh](https://ohmyz.sh/), the most popular Zsh framework, adding tons of functions and plugins.

[Starship](https://starship.rs/) is a minimal, blazing-fast, and infinitely customizable prompt for any shell, making Zsh look freaking cool!

![](https://images.unsplash.com/photo-1582513166998-56ed1ea02d13?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1632&q=80)

📷 by [Brian McGowan](https://unsplash.com/@sushioutlaw)

## Install zsh and oh-my-zsh

```bash
sudo apt-get install zsh
chsh -s $(which zsh)
curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh | sh
# install zsh-autosuggestions plugin, to be activated in .zshrc plugins list
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

## Install Nerd Font

An installed and enabled [Nerd Font](https://www.nerdfonts.com/font-downloads) is a prerequisite for Starship to display clean icons in prompt.

```bash
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.2.2/CascadiaCode.zip
unzip CascadiaCode.zip -d ~/.local/share/fonts
fc-cache -fv
```

## Install Starship

```bash
curl -sS https://starship.rs/install.sh | sh
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
starship preset nerd-font-symbols > ~/.config/starship.toml
source .zshrc
```
