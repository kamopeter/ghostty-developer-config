# Ghostty Developer Config for macOS

A ready-to-run setup script for turning a fresh Ghostty installation into a polished, practical development terminal on macOS.

It configures Ghostty, Zsh, Starship, Git, shell history, fuzzy search, directory navigation, modern CLI tools, Laravel shortcuts, Node.js shortcuts, and a cleaner Git workflow.

The goal is to provide a fast, visually clear, Warp-like terminal experience without AI features, accounts, cloud dependency, or unnecessary background services.

## What it does

The script:

- installs Homebrew if it is not already available
- installs useful terminal and development tools
- installs a Nerd Font for terminal icons
- creates a Ghostty configuration
- creates a Starship prompt configuration
- updates your `.zshrc`
- preserves your existing `.zshrc` content
- avoids duplicating its own configuration on repeated runs
- configures Git Delta for readable diffs
- imports existing shell history into Atuin
- creates timestamped backups before modifying configuration files
- validates the generated Zsh and Starship configuration

## Preview

The resulting prompt displays useful information such as:

- operating system
- username
- current directory
- Git branch
- Git working tree status
- Node.js version
- PHP version
- Python, Rust, or Go version when relevant
- Docker context
- current time
- command duration
- command exit status

Example:

```text
󰀵 user  ~/Herd/project   main !2 +1 ?3   v20   v8.4   12:30  ❯
```

Git indicators include:

- `!2` — two modified files
- `+1` — one staged file
- `?3` — three untracked files
- `⇡1` — one commit ahead
- `⇣1` — one commit behind
- `✘1` — one deleted file

## Installed tools

### Ghostty

Ghostty is the terminal emulator this setup is designed for.

The script creates a Ghostty configuration with:

- Catppuccin Mocha theme
- translucent macOS background
- native blur effect
- JetBrains Mono Nerd Font
- balanced window padding
- large scrollback history
- shell integration
- command completion notifications
- improved split visibility
- cursor and mouse behaviour adjustments

### Starship

Starship provides the shell prompt.

It displays contextual information about the current project, including:

- Git branch and status
- Node.js version
- PHP version
- Python environment
- Docker context
- command duration
- command errors

### Atuin

Atuin provides a searchable shell history.

Use:

```text
Ctrl + R
```

Unlike the default shell history, Atuin can search commands using additional context such as:

- the command itself
- the directory where it was executed
- command duration
- exit status

The script uses Atuin locally. Account creation and cloud sync are not required.

### zoxide

zoxide is a smarter replacement for repeatedly typing long `cd` paths.

Example:

```bash
z project-name
```

It learns which directories you use frequently and jumps to the most likely match.

### fzf

fzf provides fuzzy search for files, directories, and command history.

Useful shortcuts include:

- `Ctrl + R` — command history
- `Ctrl + T` — file search
- `Alt + C` — directory search

### eza

eza is a modern replacement for `ls`.

Configured aliases:

```bash
ls
ll
la
tree
```

It adds:

- icons
- Git status
- better formatting
- readable directory trees

### bat

bat is a modern replacement for `cat`.

It provides:

- syntax highlighting
- line numbers
- Git-aware output
- paging for long files

### Lazygit

Lazygit provides a terminal interface for Git.

Launch it with:

```bash
lg
```

It supports:

- staging files
- reviewing diffs
- commits
- branches
- rebasing
- stashing
- cherry-picking
- conflict handling

### Git Delta

Delta improves Git diff output.

It adds:

- syntax highlighting
- line numbers
- side-by-side diffs
- better merge conflict output
- navigation between changes

It is configured automatically as the global Git pager.

### fd

`fd` is a fast and user-friendly alternative to `find`.

Example:

```bash
fd Controller
```

The setup also adds:

```bash
f
```

as a short alias.

### ripgrep

`ripgrep` searches file contents recursively and is significantly faster than traditional `grep` for project searches.

Example:

```bash
rg "ProductVariant"
```

The setup also adds:

```bash
r
```

as a short alias.

### zsh-autosuggestions

Displays suggestions based on previously used commands while typing.

You can usually accept the suggestion using the right arrow key.

### zsh-syntax-highlighting

Highlights valid and invalid commands directly while typing.

This makes command mistakes easier to notice before execution.

### JetBrains Mono Nerd Font

The script installs JetBrains Mono Nerd Font so icons and Powerline separators render correctly.

## Installation

Clone the repository:

```bash
git clone https://github.com/kamopeter/ghostty-developer-config.git
cd ghostty-developer-config
```

Make the script executable:

```bash
chmod +x ghostty-dev-setup.sh
```

Run it:

```bash
./ghostty-dev-setup.sh
```

After installation, fully quit and reopen Ghostty.

Alternatively, reload the shell with:

```bash
exec zsh
```

## One-line installation

```bash
git clone https://github.com/kamopeter/ghostty-developer-config.git \
  && cd ghostty-developer-config \
  && chmod +x ghostty-dev-setup.sh \
  && ./ghostty-dev-setup.sh
```

Review scripts before executing them, especially when downloading them from a public repository.

## Configuration files

The script manages the following files.

### Ghostty

```text
~/Library/Application Support/com.mitchellh.ghostty/config.ghostty
```

### Starship

```text
~/.config/starship.toml
```

### Zsh

```text
~/.zshrc
```

## Backups

Existing configuration files are backed up before being modified.

Backups are stored in:

```text
~/.config/ghostty-dev-setup/backups/
```

Each run creates a timestamped backup directory.

Example:

```text
~/.config/ghostty-dev-setup/backups/20260622-120000/
```

## Safe to run multiple times

The script is designed to be repeatable.

Its managed Zsh configuration is stored between markers:

```text
# >>> GHOSTTY DEV SETUP >>>
# <<< GHOSTTY DEV SETUP <<<
```

When the script is run again, the existing managed block is replaced instead of duplicated.

Existing custom content outside this block is preserved.

Ghostty and Starship configuration files are regenerated, while previous versions are backed up first.

## Included aliases

### General

```bash
ls
ll
la
tree
cat
c
shrc
ezsh
eghost
estarship
```

Descriptions:

```text
shrc       reload ~/.zshrc
ezsh       open ~/.zshrc
eghost     open the Ghostty config
estarship  open the Starship config
```

### Git

```bash
g
gs
gst
ga
gaa
gc
gp
gl
gd
gdc
gb
gco
glog
amend
lg
```

Examples:

```bash
gst
lg
glog
```

### Laravel

```bash
art
pa
pam
pamf
pamfs
pat
par
pac
pint
sail
```

Examples:

```bash
art route:list
pam
pamfs
pat
```

### Composer

```bash
ci
cu
cda
```

### Node.js

```bash
ni
nr
nrd
nrb
nrt
```

Examples:

```bash
nrd
nrb
nr lint
```

### Search

```bash
f
r
```

Examples:

```bash
f Controller.php
r "checkout_completed_at"
```

## Additional shell features

### Create and enter a directory

The setup adds an `mkcd` function:

```bash
mkcd new-project
```

This is equivalent to:

```bash
mkdir -p new-project
cd new-project
```

### Improved shell history

The script configures a larger shared Zsh history with duplicate reduction.

### Automatic directory changes

Zsh `AUTO_CD` is enabled, so entering a directory path without explicitly typing `cd` may change into that directory.

### Command correction

Zsh command correction is enabled for mistyped commands.

## Angular CLI completion issue

Some Angular CLI and Node.js combinations may cause this error during shell startup:

```text
Error [ERR_REQUIRE_ESM]
```

The script automatically disables this line if found:

```bash
source <(ng completion script)
```

This only disables Angular CLI tab completion. It does not remove Angular CLI or affect Angular projects.

## Requirements

- macOS
- Ghostty installed
- internet connection
- administrator access may be required for Homebrew installation

The script supports both Apple Silicon and Intel Homebrew paths.

## Customization

### Change Ghostty theme

Edit the Ghostty configuration:

```bash
eghost
```

Then change:

```ini
theme = Catppuccin Mocha
```

List available Ghostty themes with:

```bash
/Applications/Ghostty.app/Contents/MacOS/ghostty +list-themes
```

### Change font size

Edit:

```ini
font-size = 14
```

### Change background transparency

Edit:

```ini
background-opacity = 0.94
```

Lower values are more transparent.

### Disable side-by-side Git diffs

```bash
git config --global delta.side-by-side false
```

Enable them again with:

```bash
git config --global delta.side-by-side true
```

## Uninstallation

The script does not currently include an automatic uninstaller.

To remove the managed Zsh section, delete everything between:

```text
# >>> GHOSTTY DEV SETUP >>>
# <<< GHOSTTY DEV SETUP <<<
```

Then restore your previous configuration from:

```text
~/.config/ghostty-dev-setup/backups/
```

Homebrew packages can be removed individually with:

```bash
brew uninstall PACKAGE_NAME
```

## Design goals

This setup is intentionally opinionated.

It prioritizes:

- fast navigation
- readable Git information
- useful project context
- local-first tools
- minimal visual clutter
- no required AI features
- no required account or cloud service

It is mainly intended for developers working with:

- Laravel
- PHP
- Node.js
- Git
- Docker
- Composer
- npm

Most of the setup is also useful for other command-line development workflows.

## Repository

https://github.com/kamopeter/ghostty-developer-config

## License

MIT is a practical license for this project. Add a `LICENSE` file to the repository if you want others to freely use, modify, and redistribute the setup.
