# lsd (LSDeluxe) Installation Guide for Linux

**lsd** — A modern, feature-rich alternative to the traditional `ls` command with syntax highlighting, icons, and Git integration.

---

## 📖 Table of Contents
- [What is lsd?](#what-is-lsd)
- [Features](#features)
- [Installation Methods](#installation-methods)
  - [Method 1: Package Manager (Ubuntu/Debian)](#method-1-package-manager-ubuntudebian)
  - [Method 2: Cargo (Rust Package Manager)](#method-2-cargo-rust-package-manager)
  - [Method 3: Download Pre-built Binary](#method-3-download-pre-built-binary)
  - [Method 4: Build from Source](#method-4-build-from-source)
- [Post-Installation Setup](#post-installation-setup)
- [Configuration](#configuration)
- [Usage Examples](#usage-examples)
- [Alias Setup](#alias-setup)
- [Troubleshooting](#troubleshooting)

---

## 🚀 What is lsd?

**lsd** (pronounced "ls deluxe") is a modern replacement for the classic `ls` command. It combines the familiarity of `ls` with modern enhancements that make directory listings more readable and informative.

### ✨ Features

- 🎨 **Syntax Highlighting:** File types, permissions, and ownership displayed in colors
- 📁 **Icons:** File icons for better visual identification (requires Nerd Fonts)
- 🔀 **Git Integration:** Shows Git status for files and directories
- 📊 **Tree View:** Built-in tree visualization with `--tree` flag
- 🔍 **Contextual Colors:** Different colors for directories, symlinks, executables, etc.
- 🚀 **Fast:** Written in Rust for performance

---

## 📦 Installation Methods

### Method 1: Package Manager (Ubuntu/Debian)

lsd is available in Ubuntu's universe repository (Ubuntu 20.04+).

**Step 1: Enable Universe Repository (if not already enabled)**
```bash
sudo add-apt-repository universe
sudo apt update
```

**Step 2: Install lsd**
```bash
sudo apt install lsd
```

**Step 3: Verify Installation**
```bash
lsd --version
```

---

### Method 2: Cargo (Rust Package Manager)

Use this method if you have Rust installed or want the latest version.

**Step 1: Install Rust (if not already installed)**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

**Step 2: Install lsd via Cargo**
```bash
cargo install lsd
```

**Step 3: Add Cargo bin to PATH (if not already)**
Add to `~/.bashrc` or `~/.zshrc`:
```bash
export PATH="$HOME/.cargo/bin:$PATH"
```

---

### Method 3: Download Pre-built Binary

For users who prefer a direct download.

**Step 1: Download Latest Release**
```bash
# Get the latest version number
VERSION=$(curl -s https://api.github.com/repos/lsd-rs/lsd/releases/latest | grep -oP '"tag_name": "\K(.*?)(?=")')

# Download for x86_64 Linux
wget https://github.com/lsd-rs/lsd/releases/download/${VERSION}/lsd-${VERSION}-x86_64-unknown-linux-gnu.tar.gz
```

**Step 2: Extract and Install**
```bash
tar -xzf lsd-*.tar.gz
sudo mv lsd /usr/local/bin/
```

**Step 3: Clean Up**
```bash
rm lsd-*.tar.gz
```

---

### Method 4: Build from Source

For developers or those who want the absolute latest version.

**Prerequisites:**
```bash
sudo apt install cargo git
```

**Step 1: Clone the Repository**
```bash
git clone https://github.com/lsd-rs/lsd.git
cd lsd
```

**Step 2: Build and Install**
```bash
cargo build --release
sudo cp target/release/lsd /usr/local/bin/
```

**Step 3: Verify Installation**
```bash
lsd --version
```

---

## 🔧 Post-Installation Setup

### Install a Nerd Font (for Icons)

To see file icons, you need a Nerd Font installed and configured in your terminal.

**Popular Nerd Fonts:**
- [FiraCode Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip)
- [JetBrains Mono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/JetBrainsMono.zip)
- [Cascadia Code Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/CascadiaCode.zip)

**Installation:**
```bash
# Create fonts directory if it doesn't exist
mkdir -p ~/.local/share/fonts

# Download and extract font (example with FiraCode)
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/FiraCode.zip
unzip FiraCode.zip -d ~/.local/share/fonts/FiraCode

# Refresh font cache
fc-cache -fv
```

Then configure your terminal emulator to use the installed Nerd Font.

---

## ⚙️ Configuration

### Create Configuration File

lsd uses a YAML configuration file located at:
- `~/.config/lsd/config.yaml` — User configuration
- `~/.config/lsd/config.yml` — Alternative extension

**Generate Default Configuration:**
```bash
lsd --config-default > ~/.config/lsd/config.yaml
```

### Example Configuration

```yaml
# ~/.config/lsd/config.yaml

# Color themes
theme: default

# Icons
icons:
  when: always
  theme: fancy
  separator: " "

# Layout
layout: grid
size: default

# Sorting
sort:
  type: name
  reverse: false
  dir-grouping: true

# Git integration
git:
  show: true
  status: true
  ignore: false

# Tree view
tree:
  depth: 3
  show-only-directories: false

# Date format
date: "+%Y-%m-%d %H:%M:%S"

# Colors
color:
  when: always
  theme: default
```

---

## 📝 Usage Examples

### Basic Commands

| Command | Description |
|---------|-------------|
| `lsd` | List current directory with colors and icons |
| `lsd -l` | Long format with detailed information |
| `lsd -a` | Show all files (including hidden) |
| `lsd -la` | Combined: long format with hidden files |
| `lsd --tree` | Display as tree structure |
| `lsd --tree --depth 2` | Tree view with limited depth |
| `lsd -R` | Recursive listing |
| `lsd -h` | Human-readable sizes |
| `lsd -t` | Sort by time (newest first) |
| `lsd -S` | Sort by size (largest first) |

### Advanced Examples

```bash
# List with Git status
lsd --git

# Tree view with icons and Git status
lsd --tree --git --icons always

# List with custom date format
lsd -l --date "+%b %d %H:%M"

# Show permissions in octal format
lsd -l --blocks permission,size,date,name
```

---

## 🔄 Alias Setup

Replace the default `ls` command with lsd by adding aliases to your shell configuration.

### Bash (~/.bashrc)
```bash
# lsd aliases
alias ls='lsd'
alias l='lsd -l'
alias la='lsd -a'
alias lla='lsd -la'
alias lt='lsd --tree'
alias lta='lsd --tree -a'
alias lg='lsd --git'
alias lgl='lsd --git -l'
```

### Zsh (~/.zshrc)
```bash
# lsd aliases
alias ls='lsd'
alias l='lsd -l'
alias la='lsd -a'
alias lla='lsd -la'
alias lt='lsd --tree'
alias lta='lsd --tree -a'
alias lg='lsd --git'
alias lgl='lsd --git -l'
```

### Apply Changes
```bash
source ~/.bashrc  # or source ~/.zshrc
```

---

## 🔍 Troubleshooting

| Issue | Solution |
|-------|----------|
| **Command not found: lsd** | Verify installation: `which lsd`<br>Check if `/usr/local/bin` is in PATH: `echo $PATH`<br>Reinstall using one of the methods above |
| **Icons not displaying** | Install a Nerd Font<br>Configure terminal to use the font<br>Verify config: `lsd --config-default \| grep -A2 icons` |
| **Colors not showing** | Ensure `color: when: always` in config<br>Check if terminal supports 256 colors: `echo $TERM`<br>Try `lsd --color always` |
| **Git status not showing** | Ensure `git: show: true` in config<br>Run in a Git repository<br>Try `lsd --git` explicitly |
| **Permission denied errors** | Run with appropriate permissions<br>Check file ownership: `ls -la`<br>Use `sudo` if needed for system directories |
| **Slow performance on large directories** | Disable Git integration in config<br>Reduce tree depth: `--tree --depth 1`<br>Use specific sorting: `--sort name` |
| **Cannot find config file** | Create directory: `mkdir -p ~/.config/lsd`<br>Generate default config: `lsd --config-default > ~/.config/lsd/config.yaml` |
| **Unexpected sorting order** | Check `sort.type` in config<br>Use command-line flags to override: `--sort time` |

---

## 🎯 Quick Reference

### Common Flags

| Flag | Alternative | Description |
|------|-------------|-------------|
| `-l` | `--long` | Detailed list format |
| `-a` | `--all` | Show hidden files |
| `-t` | `--timesort` | Sort by modification time |
| `-S` | `--sizesort` | Sort by file size |
| `-r` | `--reverse` | Reverse sort order |
| `-R` | `--recursive` | List subdirectories recursively |
| `--tree` | — | Display as tree |
| `--git` | — | Show Git status |
| `--icons` | — | Control icon display (always/auto/never) |

---

## 📚 Additional Resources

- [Official GitHub Repository](https://github.com/lsd-rs/lsd)
- [Documentation](https://github.com/lsd-rs/lsd#documentation)
- [Nerd Fonts](https://www.nerdfonts.com/)
- [Rust Installation](https://www.rust-lang.org/tools/install)

---

## 📄 Documentation Maintained By

*Community Contribution*

---

*For issues or feature requests, please open an issue on the [GitHub repository](https://github.com/lsd-rs/lsd/issues).*
```

This README provides:
- Multiple installation methods for different user preferences
- Clear visual hierarchy with emojis for quick scanning
- A detailed troubleshooting table
- Configuration examples with YAML
- Usage examples and common commands
- Alias setup for seamless integration
- A quick reference table for flags
- Links to additional resources
