# Installation Guide

This document provides detailed installation instructions for Excel TUI on various platforms.

## Table of Contents

- [Requirements](#requirements)
- [Quick Install](#quick-install)
- [Platform-Specific Instructions](#platform-specific-instructions)
- [Building from Source](#building-from-source)
- [Verifying Installation](#verifying-installation)
- [Troubleshooting](#troubleshooting)

## Requirements

- Go 1.21 or higher (for building from source)
- Terminal with 256-color support
- For Linux: `xclip` or `xsel` for clipboard support

## Quick Install

### Using go install

```bash
go install github.com/CodeOne45/vexcel-tui@latest
```

### Download Pre-built Binaries

1. Visit the [releases page](https://github.com/dth99/vexcel.git/releases)
2. Download the appropriate binary for your platform
3. Extract and move to your PATH

## Platform-Specific Instructions

### macOS

#### Using Homebrew (Recommended)

```bash
# Coming soon
brew install vexcel
```

#### Manual Installation

```bash
# Download latest release
curl -L https://github.com/dth99/vexcel.git/releases/latest/download/vexceldarwin-arm64.tar.gz -o vexcel-tui.tar.gz

# Extract
tar xzf vexcel.tar.gz

# Make executable
chmod +x vexceldarwin-arm64

# Move to PATH
sudo mv vexceldarwin-arm64 /usr/local/bin/vexcel

# Verify
vexcel --version
```

**Note**: On macOS, you may need to allow the app in System Preferences → Security & Privacy

### Linux

#### Using Package Manager

```bash
# Debian/Ubuntu (Coming soon)
sudo apt install vexcel

# Arch Linux (Coming soon)
yay -S vexcel

# Fedora (Coming soon)
sudo dnf install vexcel
```

#### Manual Installation

```bash
# Download latest release
wget https://github.com/dth99/vexcelcel.git/releases/latest/download/vexcellinux-amd64.tar.gz

# Extract
tar xzf vexcellinux-amd64.tar.gz

# Make executable
chmod +x vexcellinux-amd64

# Move to PATH
sudo mv vexcellinux-amd64 /usr/local/bin/vexcel

# Install clipboard utilities
sudo apt-get install xclip  # Ubuntu/Debian
# or
sudo pacman -S xclip        # Arch
# or
sudo dnf install xclip      # Fedora

# Verify
vexcel --version
```

### Windows

#### Using Chocolatey (Coming soon)

```powershell
choco install vexcel
```

#### Using Scoop (Coming soon)

```powershell
scoop install vexcel
```

#### Manual Installation

1. Download `vexcelwindows-amd64.zip` from [releases](https://github.com/dth99/vexcelcel.git/releases/latest)
2. Extract the ZIP file
3. Add the directory to your PATH:
   - Right-click "This PC" → Properties
   - Advanced system settings → Environment Variables
   - Edit PATH and add the directory
4. Open a new terminal and verify: `vexcel --version`

**Recommended Terminal**: Windows Terminal for best experience

## Building from Source

### Prerequisites

```bash
# Install Go (if not already installed)
# Visit: https://golang.org/doc/install

# Verify Go installation
go version
```

### Build Steps

```bash
# Clone the repository
git clone https://github.com/dth99/vexcelcel.git
cd vexcelcel

# Install dependencies
go mod download

# Build
go build -o vecel .

# Or use Make
make build

# Install globally
make install
```

### Development Build

```bash
# Build with race detector
go build -race -o vexcel .

# Run tests
make test

# Run with coverage
make test-coverage
```

## Verifying Installation

After installation, verify it works:

```bash
# Check version
vexcel --version

# Run with sample data
vexcel sample_data.csv

# Test with a theme
vexcel sample_data.csv --theme nord
```

## Troubleshooting

### "command not found"

**Problem**: Shell can't find the `vex` command

**Solution**:

```bash
# Check if binary is in PATH
which vexcel

# If not found, add to PATH
export PATH="$PATH:/path/to/vexcel"

# Make permanent (add to ~/.bashrc or ~/.zshrc)
echo 'export PATH="$PATH:/path/to/vexcel"' >> ~/.bashrc
```

### Clipboard Not Working (Linux)

**Problem**: Copy operations don't work

**Solution**:

```bash
# Install clipboard utilities
sudo apt-get install xclip xsel  # Ubuntu/Debian
sudo pacman -S xclip xsel        # Arch
sudo dnf install xclip xsel      # Fedora
```

### Colors Not Displaying Correctly

**Problem**: Terminal shows wrong colors or no colors

**Solution**:

```bash
# Check TERM variable
echo $TERM

# Should be xterm-256color or similar
# Set it if needed
export TERM=xterm-256color

# Make permanent
echo 'export TERM=xterm-256color' >> ~/.bashrc
```

### "Permission Denied" on macOS

**Problem**: macOS blocks execution of downloaded binary

**Solution**:

```bash
# Remove quarantine attribute
xattr -d com.apple.quarantine /path/to/vexcel

# Or allow in System Preferences
# System Preferences → Security & Privacy → General
```

### Go Build Fails

**Problem**: Build errors or dependency issues

**Solution**:

```bash
# Clean and retry
go clean -cache -modcache
go mod download
go mod verify
go build .
```

### Large Files Load Slowly

**Problem**: Excel files with 50k+ rows are slow

**Solution**:

- This is expected for very large files
- The app uses lazy loading for optimal performance
- Consider filtering/splitting the data beforehand
- Use CSV format when possible (faster than Excel)

## Uninstalling

### If installed via go install

```bash
rm $(which vexcel)
```

### If installed manually

```bash
# Remove binary
sudo rm /usr/local/bin/vexcel

# Remove config (if any)
rm -rf ~/.config/vexcel
```

### If installed via package manager

```bash
# macOS
brew uninstall vexcel

# Linux
sudo apt remove vexcel     # Debian/Ubuntu
yay -R vexcel              # Arch
sudo dnf remove vexcel     # Fedora

# Windows
choco uninstall vexcel     # Chocolatey
scoop uninstall vexcel     # Scoop
```

## Next Steps

After successful installation:

1. Read the [README](README.md) for feature overview
2. Check [CONTRIBUTING](CONTRIBUTING.md) if you want to contribute
3. Report issues on [GitHub](https://github.com/dth99/vexcel/issues)

## Support

If you encounter issues not covered here:

- Check [existing issues](https://github.com/dth99/vexcel/issues)
- Create a new issue with:
  - Your OS and version
  - Go version (if building from source)
  - Terminal emulator
  - Error messages
  - Steps to reproduce

Happy viewing! 📊✨
