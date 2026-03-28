# lsd (LSDeluxe) Installation & Configuration Guide

**lsd** — A modern, feature-rich alternative to the traditional `ls` command with syntax highlighting, icons, and Git integration.

---

## 📖 Table of Contents
- [What is lsd?](#what-is-lsd)
- [Installation](#installation)
- [Minimal Working Configuration](#minimal-working-configuration)
- [Configuration Reference](#configuration-reference)
- [Usage Examples](#usage-examples)
- [Alias Setup](#alias-setup)
- [Troubleshooting](#troubleshooting)

---

## 🚀 What is lsd?

**lsd** (pronounced "ls deluxe") is a modern replacement for the classic `ls` command that adds:
- 🎨 **Syntax highlighting** for file types
- 📁 **File icons** (requires Nerd Fonts)
- 🔀 **Git integration** showing file status
- 📊 **Tree view** with `--tree` flag
- 🚀 **Fast performance** written in Rust

---

## 📦 Installation

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install lsd
```

### Verify Installation
```bash
lsd --version
```

---

## ⚙️ Minimal Working Configuration

After multiple attempts with various syntax errors, here is the **minimal working configuration** that works across different lsd versions:

### Step 1: Create the config directory
```bash
mkdir -p ~/.config/lsd
```

### Step 2: Create the configuration file
```bash
nano ~/.config/lsd/config.yaml
```

### Step 3: Add the minimal configuration
Copy and paste exactly this:

```yaml
# lsd - Minimal Working Configuration
# This configuration works without syntax errors

# Icons settings
icons:
  when: auto
  theme: fancy
  separator: " "

# Layout arrangement (grid, tree, or oneline)
layout: grid

# Which files to display
display: visible-only

# Sorting preferences
sorting:
  column: name
  reverse: false
  dir-grouping: first

# Color settings
color:
  when: auto
  theme: default

# Hyperlink support (always, auto, or never)
hyperlink: auto
```

### Step 4: Save and exit
- **For nano:** `Ctrl + O` → `Enter` → `Ctrl + X`
- **For vim:** `Esc` → `:wq` → `Enter`

### Step 5: Test the configuration
```bash
lsd
```

You should see a colorful directory listing with icons (if your terminal supports them).

---

## 📝 Configuration Reference

Here are the correct field values for lsd configuration:

| Field | Purpose | Valid Values |
|-------|---------|--------------|
| **icons.when** | When to show icons | `auto`, `always`, `never` |
| **icons.theme** | Icon theme | `fancy`, `unicode` |
| **layout** | Display arrangement | `grid`, `tree`, `oneline` |
| **display** | Which files to show | `visible-only`, `all`, `almost-all`, `directory-only` |
| **sorting.column** | Sort by | `name`, `size`, `time`, `extension` |
| **sorting.reverse** | Reverse order | `true`, `false` |
| **sorting.dir-grouping** | Directory position | `first`, `last`, `none` |
| **color.when** | When to use colors | `auto`, `always`, `never` |
| **hyperlink** | Terminal hyperlinks | `auto`, `always`, `never` |

---

## 💻 Usage Examples

### Basic Commands
```bash
# Basic listing
lsd

# Long format with details
lsd -l

# Show all files (including hidden)
lsd -a

# Long format with all files
lsd -la

# Tree view
lsd --tree

# Tree view with depth limit
lsd --tree --depth 2
```

### Advanced Commands
```bash
# Show Git status (colors indicate modified/staged files)
lsd --git

# Sort by size (largest first)
lsd --sort size

# Sort by time (newest first)
lsd --sort time

# Reverse sort order
lsd --reverse

# One-line layout
lsd --layout oneline

# Human-readable sizes
lsd -l --size short
```

---

## 🔄 Alias Setup

Replace the default `ls` command with lsd by adding aliases to your shell configuration.

### For Zsh (~/.zshrc)
```bash
# Add these lines to ~/.zshrc
echo '# lsd aliases' >> ~/.zshrc
echo 'alias ls="lsd"' >> ~/.zshrc
echo 'alias l="lsd -l"' >> ~/.zshrc
echo 'alias la="lsd -a"' >> ~/.zshrc
echo 'alias lla="lsd -la"' >> ~/.zshrc
echo 'alias lt="lsd --tree"' >> ~/.zshrc
echo 'alias lta="lsd --tree -a"' >> ~/.zshrc
echo 'alias lg="lsd --git"' >> ~/.zshrc
echo 'alias lgl="lsd --git -l"' >> ~/.zshrc

# Reload configuration
source ~/.zshrc
```

### For Bash (~/.bashrc)
```bash
# Add these lines to ~/.bashrc
echo '# lsd aliases' >> ~/.bashrc
echo 'alias ls="lsd"' >> ~/.bashrc
echo 'alias l="lsd -l"' >> ~/.bashrc
echo 'alias la="lsd -a"' >> ~/.bashrc
echo 'alias lla="lsd -la"' >> ~/.bashrc
echo 'alias lt="lsd --tree"' >> ~/.bashrc
echo 'alias lta="lsd --tree -a"' >> ~/.bashrc
echo 'alias lg="lsd --git"' >> ~/.bashrc
echo 'alias lgl="lsd --git -l"' >> ~/.bashrc

# Reload configuration
source ~/.bashrc
```

---

## 🔍 Troubleshooting

### Common Errors and Solutions

| Error | Solution |
|-------|----------|
| **Command not found: lsd** | Install lsd: `sudo apt install lsd` |
| **No icons showing** | Install a Nerd Font and configure your terminal to use it |
| **Configuration syntax errors** | Use the minimal configuration above with correct field values |
| **`dir-grouping: true` error** | Change to `dir-grouping: first` |
| **`hyperlink: false` error** | Change to `hyperlink: auto` |
| **`display: grid` error** | Use `display: visible-only` (layout controls grid) |
| **Config not being used** | Verify file location: `ls -la ~/.config/lsd/config.yaml` |

### Reset Configuration
If you encounter persistent errors, remove the config and start fresh:
```bash
rm ~/.config/lsd/config.yaml
mkdir -p ~/.config/lsd
# Then recreate using the minimal configuration above
```

### Test Without Config
To test if lsd works without any configuration:
```bash
mv ~/.config/lsd/config.yaml ~/.config/lsd/config.yaml.backup
lsd
```

---

## 🎯 Quick Start Summary

For a complete working setup, run these commands:

```bash
# 1. Install lsd
sudo apt update && sudo apt install lsd

# 2. Create config directory
mkdir -p ~/.config/lsd

# 3. Create minimal config
cat > ~/.config/lsd/config.yaml << 'EOF'
icons:
  when: auto
  theme: fancy
layout: grid
display: visible-only
sorting:
  column: name
  reverse: false
  dir-grouping: first
color:
  when: auto
hyperlink: auto
EOF

# 4. Test it works
lsd

# 5. Add aliases (optional)
echo 'alias ls="lsd"' >> ~/.zshrc
echo 'alias l="lsd -l"' >> ~/.zshrc
source ~/.zshrc
```

---

## 📚 Additional Resources

- [Official GitHub Repository](https://github.com/lsd-rs/lsd)
- [Nerd Fonts for Icons](https://www.nerdfonts.com/)
- [Rust Installation](https://www.rust-lang.org/tools/install)

---

## 📄 Documentation Maintained By

*Community Contribution*

---

*For issues or questions, please open an issue on the [GitHub repository](https://github.com/lsd-rs/lsd/issues).*
```

This documentation provides:
1. **Minimal working configuration** that avoids all syntax errors
2. **Correct field values** based on your version's requirements
3. **Step-by-step setup** with clear commands
4. **Troubleshooting table** for common errors
5. **Quick start summary** for users who want to copy-paste and go
6. **Alias setup** for both Zsh and Bash
7. **Complete reference** of all configuration options

