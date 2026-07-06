# dotfiles

Personal dotfiles managed with chezmoi (https://www.chezmoi.io/) — a portable terminal environment for macOS, built around zsh, Starship, and iTerm2.

## What's in here

| File | Purpose |
|---|---|
| .zshrc | Main zsh config — plugins, aliases, tool integrations |
| .zprofile | Login shell config — PATH setup |
| .gitconfig | Git identity and credential settings |
| ~/.config/starship.toml | Starship prompt appearance and modules |
| ~/.config/zsh/starship.zsh | OS/distro icon detection for the prompt |
| ~/.config/thefuck/settings.py + rules/ | Custom thefuck command-correction rules |
| iTerm2 preferences | Terminal app settings, profiles, and appearance |

## Tools this setup depends on

- Shell: zsh
- Terminal: iTerm2 (https://iterm2.com/)
- Prompt: Starship (https://starship.rs/)
- Package manager: Homebrew (https://brew.sh/)
- Dotfile manager: chezmoi (https://www.chezmoi.io/)

Plugins/tools referenced in .zshrc: zsh-autocomplete, zsh-autosuggestions, zsh-syntax-highlighting, autojump, eza, thefuck.

## Setting up on a new machine

1. Install Homebrew:

   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Install chezmoi and initialize from this repo:

   brew install chezmoi
   chezmoi init --apply git@github.com-avocadoattack:avocadoattack/dotfiles.git

3. Install the tools referenced above via Homebrew (starship, eza, autojump, thefuck, etc.) and their respective zsh plugins.

4. Restart your terminal — chezmoi apply will have already placed all config files in the right spots.

## Notes

- Some files use chezmoi's templating ({{ .chezmoi.homeDir }}) so paths resolve correctly regardless of the machine's username.
- This repo is intentionally private. It's a personal environment snapshot, not a general-purpose starter kit.
- SSH keys, shell history, and credential files are deliberately excluded.
