# dotfiles

Personal dotfiles managed with [chezmoi](https://www.chezmoi.io/). My portable terminal environment for macOS, built around zsh, Starship, and iTerm2.

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

- `Homebrew` — package manager (https://brew.sh/)
- `chezmoi` — dotfile manager (https://www.chezmoi.io/)
- `zsh` — shell
- `iTerm2` — terminal (https://iterm2.com/)
- `Starship` — prompt (https://starship.rs/)
- `zsh-autocomplete` — tab-completion plugin
- `zsh-autosuggestions` — inline command suggestions
- `zsh-syntax-highlighting` — colors commands as you type
- `autojump` — fast directory jumping
- `eza` — modern `ls` replacement
- `thefuck` — command-correction tool

## Setting up on a new machine

1. Install Homebrew:

       /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Install chezmoi and initialize from this repo:

       brew install chezmoi
       chezmoi init --apply git@github.com:avocadoattack/dotfiles.git

3. Install the tools listed above via Homebrew and their respective zsh plugins.

4. Restart your terminal — chezmoi apply will have already placed all config files in the right spots.

## Maintaining this setup

Editing a tracked text file (e.g. .zshrc):

    cd ~/.local/share/chezmoi
    chezmoi edit ~/.zshrc
    chezmoi diff
    chezmoi apply
    git add <file>
    git commit -m "description"
    git push

Editing a GUI-configured file (e.g. iTerm2 preferences):

    # make the change in the app itself, then:
    cd ~/.local/share/chezmoi
    chezmoi re-add
    chezmoi diff
    git add <file>
    git commit -m "description"
    git push

## Notes

- Some files use chezmoi's templating ({{ .chezmoi.homeDir }}) so paths resolve correctly regardless of the machine's username.
- SSH keys, GPG keys, shell history, and credential files were never added to this repo — see .chezmoiignore for the full list and reasoning.
