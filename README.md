# dotfiles

My portable terminal environment for macOS, built around zsh, Starship, and iTerm2.
> dotfiles managed with [chezmoi](https://www.chezmoi.io/). 

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

- `Homebrew` ➞ [Package manager](https://brew.sh/)
- `chezmoi` ➞ [dotfile manager](https://www.chezmoi.io/)
- `zsh` ➞ [Shell](https://zsh.sourceforge.io/)
- `iTerm2` ➞ [Terminal emulator](https://iterm2.com/)
- `Starship` ➞ [Prompt](https://starship.rs/)
- `zsh-autocomplete` ➞ [Tab-completion plugin](https://github.com/marlonrichert/zsh-autocomplete)
- `zsh-autosuggestions` ➞ [Inline command suggestions](https://github.com/zsh-users/zsh-autosuggestions)
- `zsh-syntax-highlighting` ➞ [Colors commands as you type](https://github.com/zsh-users/zsh-syntax-highlighting)
- `autojump` ➞ [Fast directory jumping](https://github.com/wting/autojump)
- `eza` ➞ [Modern `ls` replacement](https://github.com/eza-community/eza)
- `thefuck` ➞ [Command-correction tool](https://github.com/nvbn/thefuck)
- `Hack Nerd Font` ➞ [Font with the icons used by Starship and eza](https://www.nerdfonts.com/)

## Setting up on a new machine

1. Install Homebrew:

       /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

   On Apple Silicon, `brew` is not on your PATH yet in this first window. Run this once (after step 4, .zprofile handles it automatically):

       eval "$(/opt/homebrew/bin/brew shellenv)"

2. Install the command-line tools and zsh plugins:

       brew install chezmoi starship eza thefuck autojump zsh-autocomplete zsh-autosuggestions zsh-syntax-highlighting pipx

   Also add `git-lfs` if you work with Git LFS repos (.gitconfig enables its filter).

3. Install iTerm2 and the font, but don't open iTerm2 yet:

       brew install --cask iterm2 font-hack-nerd-font

4. Initialize and apply this repo. HTTPS works without an SSH key because the repo is public:

       chezmoi init --apply https://github.com/avocadoattack/dotfiles.git

   iTerm2 must not be running during this step, or it overwrites the applied preferences when it quits.

5. Open iTerm2. New windows load Homebrew, the plugins, and Starship.

6. Before committing from this machine, set up your SSH key, switch the remote to SSH, and confirm your git identity:

       cd ~/.local/share/chezmoi
       git remote set-url origin <your SSH remote URL>
       git config user.name
       git config user.email

## Maintaining this setup

Editing a tracked text file (e.g. .zshrc):

    cd ~/.local/share/chezmoi
    chezmoi edit ~/.zshrc
    chezmoi diff
    chezmoi apply
    git status              # confirm the real source filename before staging
    git add <file>
    git commit -m "description"
    git push

Editing a GUI-configured file (e.g. iTerm2 preferences):

    # make the change in the app itself, then:
    cd ~/.local/share/chezmoi
    chezmoi re-add
    chezmoi diff
    git status              # confirm the real source filename before staging
    git add <file>
    git commit -m "description"
    git push

## Notes

- Some files use chezmoi's templating ({{ .chezmoi.homeDir }}) so paths resolve correctly regardless of the machine's username.
- Source filenames often differ from live filenames due to chezmoi's naming convention (e.g., `.zshrc` → `dot_zshrc.tmpl`, and files under `.chezmoiignore`-adjacent private paths get a `private_` prefix). Run `git status` or `chezmoi source-path <live-file>` if `git add` can't find the file you expect.
- SSH keys, GPG keys, shell history, and credential files were never added to this repo — see .chezmoiignore for the full list and reasoning.
