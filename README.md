# Tesseract OCR Source Builder

A powerful and intelligent bash script that builds [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) from source with full customization and dependency management.

## ✨ Features

- **🔧 Configurable Versions**: Build any Tesseract version (default: 5.5.1)
- **🌍 Multi-Language Support**: Download and install language packs from [tessdata_best](https://github.com/tesseract-ocr/tessdata_best)
- **🖥️ Cross-Platform**: Supports Ubuntu/Debian, RHEL/CentOS/Fedora, and macOS
- **📊 Intelligent Status Checking**: Comprehensive analysis of current installation state
- **⚡ Selective Installation**: Skip any component (dependencies, Leptonica, Tesseract, languages)
- **🛠️ Automatic Dependency Management**: Installs all required system packages
- **🚀 Parallel Compilation**: Uses all available CPU cores for faster builds
- **💡 Smart Recommendations**: Suggests optimal installation commands based on system status

## 🎯 Quick Start

```bash
# Download the script
curl -O https://raw.githubusercontent.com/NikolasTh90/tesseract-installer/main/build_tesseract.sh
chmod +x build_tesseract.sh

# Check current status
./build_tesseract.sh --status

# Full installation with defaults
./build_tesseract.sh

# Custom version and languages
./build_tesseract.sh -v 5.4.1 -l eng,fra,deu,spa
```

## 📋 Requirements

### System Requirements
- **Linux**: Ubuntu 18.04+, Debian 10+, RHEL/CentOS 7+, Fedora 30+
- **macOS**: macOS 10.14+ with Homebrew
- **Memory**: 2GB+ RAM recommended for compilation
- **Disk**: 1GB+ free space

### Permissions
- `sudo` access for system-wide installation (when using default `/usr/local` prefix)
- Internet connection for downloading source code and dependencies

## 🚀 Installation & Usage

### Basic Usage

```bash
# Install with defaults (Tesseract 5.5.1, languages: eng,ara,ell)
./build_tesseract.sh

# Specify version and languages
./build_tesseract.sh --version 5.4.1 --languages eng,fra,deu

# Custom installation prefix
./build_tesseract.sh --prefix /opt/tesseract

# Use specific number of compilation jobs
./build_tesseract.sh --jobs 8
```

### Status Checking

```bash
# Check what's currently installed
./build_tesseract.sh --status

# Get installation recommendations
./build_tesseract.sh --status
# Follow the suggested command from the output
```

### Selective Installation

```bash
# Only install missing languages (Tesseract already installed)
./build_tesseract.sh --skip-tesseract --languages eng,chi_sim,jpn

# Install Tesseract without language files
./build_tesseract.sh --skip-languages

# Skip dependency installation (already installed manually)
./build_tesseract.sh --skip-dependencies

# Quick rebuild (skip deps and Leptonica)
./build_tesseract.sh --skip-dependencies --skip-leptonica
```

## 📖 Command Reference

### Main Options

| Option | Description | Default |
|--------|-------------|---------|
| `-v, --version VERSION` | Tesseract version to build | `5.5.1` |
| `-l, --languages LANGS` | Comma-separated language codes | `eng,ara,ell` |
| `-p, --prefix PREFIX` | Installation directory | `/usr/local` |
| `-j, --jobs JOBS` | Parallel compilation jobs | Auto-detect |

### Skip Options

| Option | Description | Use Case |
|--------|-------------|----------|
| `--skip-dependencies` | Skip system package installation | Dependencies already installed |
| `--skip-leptonica` | Skip Leptonica build | Leptonica already available |
| `--skip-tesseract` | Skip Tesseract build | Only updating languages |
| `--skip-languages` | Skip language downloads | Managing languages separately |

### Utility Options

| Option | Description |
|--------|-------------|
| `--status` | Show installation status and exit |
| `-h, --help` | Display help message |

## 🌍 Supported Languages

The script downloads high-quality language models from [tessdata_best](https://github.com/tesseract-ocr/tessdata_best). Common language codes include:

| Code | Language | Code | Language |
|------|----------|------|----------|
| `eng` | English | `fra` | French |
| `ara` | Arabic | `deu` | German |
| `ell` | Greek | `spa` | Spanish |
| `por` | Portuguese | `rus` | Russian |
| `chi_sim` | Chinese (Simplified) | `chi_tra` | Chinese (Traditional) |
| `jpn` | Japanese | `kor` | Korean |
| `hin` | Hindi | `ita` | Italian |
| `nld` | Dutch | `pol` | Polish |
| `tur` | Turkish | `vie` | Vietnamese |

[View complete list →](https://github.com/tesseract-ocr/tessdata_best)

## 🔍 Status Information

The `--status` command provides comprehensive information about:

- **System Dependencies**: Installed vs missing packages
- **Leptonica**: Installation status and version
- **Tesseract**: Version, location, and compatibility
- **Language Data**: Available vs requested languages
- **Recommendations**: Suggested commands for completion

### Example Status Output

```
=== TESSERACT INSTALLATION STATUS ===
System: Linux x86_64
Install Prefix: /usr/local

=== SYSTEM DEPENDENCIES ===
✓ All required dependencies are installed (20 packages)

=== LEPTONICA STATUS ===
✓ Leptonica is installed (version: 1.82.0)

=== TESSERACT STATUS ===
✓ Tesseract is installed
  Version: 5.5.1
  Location: /usr/local/bin/tesseract

=== LANGUAGE DATA STATUS ===
  Tessdata directory: /usr/local/share/tessdata
✓ Available languages: eng ara ell
✓ All requested languages are available

=== SUMMARY ===
✓ Complete Tesseract installation detected!
  All components are installed and ready to use
```

## 🛠️ Troubleshooting

### Common Issues

**Permission Denied**
```bash
# Run with sudo for system-wide installation
sudo ./build_tesseract.sh

# Or use custom prefix
./build_tesseract.sh --prefix ~/tesseract
```

**Missing Dependencies**
```bash
# Check what's missing
./build_tesseract.sh --status

# Install dependencies manually, then skip them
./build_tesseract.sh --skip-dependencies
```

**Compilation Errors**
```bash
# Use fewer parallel jobs
./build_tesseract.sh --jobs 1

# Check available memory
free -h
```

**Language Files Not Found**
```bash
# Re-download languages only
./build_tesseract.sh --skip-tesseract --languages eng,fra,deu

# Check tessdata directory permissions
ls -la /usr/local/share/tessdata
```

### Platform-Specific Notes

**Ubuntu/Debian**
- Requires `sudo apt-get update` if packages are outdated
- May need `universe` repository enabled

**RHEL/CentOS**
- May require EPEL repository for some packages
- Use `dnf` instead of `yum` on newer versions

**macOS**
- Requires Homebrew package manager
- May need Xcode command line tools: `xcode-select --install`

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

### Development

1. Fork the repository
2. Create a feature branch
3. Test your changes on multiple platforms
4. Submit a pull request

### Testing

Test the script on different scenarios:
```bash
# Test status checking
./build_tesseract.sh --status

# Test with skip flags
./build_tesseract.sh --skip-dependencies --skip-leptonica

# Test with different versions
./build_tesseract.sh -v 5.4.1
```

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) - The amazing OCR engine
- [Leptonica](https://github.com/DanBloomberg/leptonica) - Image processing library
- [tessdata_best](https://github.com/tesseract-ocr/tessdata_best) - High-quality language models

## 📞 Support

If you encounter issues:

1. Check the [troubleshooting section](#-troubleshooting)
2. Run `./build_tesseract.sh --status` to diagnose
3. [Open an issue](https://github.com/YOUR_USERNAME/YOUR_REPO/issues) with:
   - Your operating system and version
   - Complete error output
   - Status command output

---

**⭐ Star this repository if it helped you build Tesseract successfully!**
