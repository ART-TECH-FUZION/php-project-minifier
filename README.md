# PHP Project Minifier

A powerful and easy-to-use CLI tool that compresses and minifies your PHP projects. Built with a Vite-inspired design, it handles multiple file types and creates optimized production-ready builds.

---

## Table of Contents

- [What is PHP Project Minifier?](#what-is-php-project-minifier)
- [Key Features](#key-features)
- [Installation Guide](#installation-guide)
  - [Method 1: Download via Git](#method-1-download-via-git-recommended)
  - [Method 2: Download as ZIP](#method-2-download-as-zip)
  - [Method 3: Install via Composer](#method-3-install-via-composer)
- [Quick Start](#quick-start)
- [Understanding Output Folder Priority](#understanding-output-folder-priority)
- [Basic Usage Examples](#basic-usage-examples)
- [Command Options](#command-options)
- [Supported File Types](#supported-file-types)
- [compress.json Configuration](#compressjson-configuration)
- [Real-World Example](#real-world-example)
- [Watch Mode for Development](#watch-mode-for-development)
- [Dry Run Mode](#dry-run-mode)
- [Minimum Output Mode](#minimum-output-mode)
- [Requirements](#requirements)
- [Troubleshooting](#troubleshooting)
- [How Minification Works](#how-minification-works)
- [Best Practices](#best-practices)
- [Performance Stats Example](#performance-stats-example)
- [Security Note](#security-note)
- [Version Information](#version-information)
- [Contributing \& Contact](#contributing--contact)

---

## What is PHP Project Minifier?

PHP Project Minifier is a command-line tool that makes your project files smaller by removing unnecessary whitespace, comments, and formatting. This results in:

- **Faster page loads** - Smaller files download quicker
- **Reduced bandwidth** - Less data transfer between server and users
- **Better performance** - Optimized code runs more efficiently
- **Professional builds** - Clean, production-ready output

---

## Key Features

| Feature | Description |
|---------|-------------|
| **Multiple File Support** | Minifies PHP, HTML, CSS, JS, JSON, JSX, and XML files |
| **Smart Minification** | Preserves strings, comments in code, and special content like SQL in PHP strings |
| **Gitignore Support** | Automatically respects your .gitignore rules |
| **Watch Mode** | Auto-compresses files when they change during development |
| **Config File** | Custom settings via `compress.json` |
| **Detailed Stats** | Shows file count, size savings, and compression percentage |
| **Index Files** | Auto-creates `index.php` in every folder for security |
| **Dry Run** | Preview what would happen without making changes |
| **Mixed Code Handling** | Properly handles PHP files with inline HTML, CSS, and JavaScript |

---

## Installation Guide

### Method 1: Download via Git (Recommended)

**Step 1: Open Terminal**

**Step 2: Clone the Repository**
```bash
git clone https://github.com/ART-TECH-FUZION/php-project-minifier.git
```

**Step 3: Navigate to the Project**
```bash
cd php-project-minifier
```

**Step 4: Make Scripts Executable (Linux/macOS)**
```bash
chmod +x bin/compress
chmod +x bin/build
```

**Step 5: Verify Installation**
```bash
php bin/compress --version
```

---

### Method 2: Download as ZIP

**Step 1: Download ZIP**
- Go to: https://github.com/ART-TECH-FUZION/php-project-minifier.git
- Click the green **"Code"** button
- Select **"Download ZIP"**

**Step 2: Extract the ZIP**
```bash
unzip php-project-minifier-main.zip
cd php-project-minifier-main
```

**Step 3: Make Scripts Executable**
```bash
chmod +x bin/compress
chmod +x bin/build
```

---

### Method 3: Install via Composer

```bash
# Download via Composer (global installation)
composer global require compress/php-compress
```

---

## Quick Start

### Option 1: Direct Usage (No Installation)

```bash
# Navigate to the minifier directory
cd /users/name/desktop/lib/php-project-minifier

# Compress your project
php bin/compress /path/to/your/project
```

### Option 2: Using the Alias Command

```bash
# Go to your project directory
cd /path/to/your/project

# Run the build command (make sure PATH includes the bin folder)
build
```

### Option 3: Global Installation via Composer

```bash
# Install globally
composer global require compress/php-compress

# Now use from anywhere
cd /path/to/your/project
compress
```

---

## Understanding Output Folder Priority

The tool decides where to save compressed files in this order:

1. **Command Line Argument** - If you specify a second argument, that's the output folder
2. **compress.json** - If your project has a `compress.json` file with `"output"` setting
3. **Default** - If neither is set, it creates a `dist` folder in your project

Example:
```bash
# Output goes to /my-project/dist (default)
php bin/compress /my-project

# Output goes to /my-custom-folder
php bin/compress /my-project /my-custom-folder
```

---

## Basic Usage Examples

### Example 1: Compress Current Directory

```bash
cd /path/to/your/project
php bin/compress
```

### Example 2: Compress a Specific Folder

```bash
php bin/compress /users/user-name/my-website
```

### Example 3: Specify Custom Output Folder

```bash
php bin/compress /users/user-name/my-website /users/user-name/my-website/minified-output
```

### Example 4: Use compress.json Config

Create a `compress.json` file in your project root:

```json
{
  "source": "./",
  "output": "./dist"
}
```

Then simply run:
```bash
cd /path/to/your/project
build
```

---

## Command Options

| Command | Description |
|---------|-------------|
| `php bin/compress` | Compress current directory |
| `php bin/compress <folder>` | Compress specific folder |
| `php bin/compress <src> <output>` | Compress with custom output |
| `build` | Alias for compress on current directory |
| `--init` | Create a default compress.json file |
| `--watch <folder>` | Watch for changes and auto-compress |
| `--min` | Show minimal output (only stats) |
| `--dry-run` | Preview without making changes |
| `--no-index` | Don't create index.php files |
| `--help` or `-h` | Show help message |
| `--version` or `-v` | Show version number |

---

## Supported File Types

| Extension | What It Does |
|-----------|---------------|
| `.php` | Minifies PHP code, handles inline HTML/CSS/JS |
| `.html` / `.htm` | Minifies HTML with inline CSS/JS |
| `.css` | Compresses CSS, preserves strings |
| `.js` | Minifies JavaScript, handles template literals |
| `.json` | Compresses JSON (no data loss) |
| `.jsx` | Minifies React JSX files |
| `.xml` | Compresses XML, protects CDATA sections |

---

## Complete compress.json Configuration

Create this file in your project root to customize behavior:

```json
{
  "source": "./",
  "output": "./dist",
  "exclude": [
    ".git",
    "node_modules",
    "vendor"
  ],
  "extensions": ["php", "html", "htm", "css", "js", "json", "jsx", "xml"],
  "createIndex": true,
  "indexContent": "<?php\n// Silence is golden.\n"
}
```

### Configuration Options Explained

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `source` | string | `"./"` | Which folder to compress |
| `output` | string | `"./dist"` | Where to save compressed files |
| `exclude` | array | `[".git"]` | Folders to skip |
| `extensions` | array | All supported | File types to process |
| `createIndex` | boolean | `true` | Create index.php in each folder |
| `indexContent` | string | `<?php\n// Silence is golden.\n` | Content for index files |

---

## Real-World Example

### Before Compression

**Project Structure:**
```
my-website/
├── index.php
├── about.html
├── contact.php
├── css/
│   └── style.css
├── js/
│   └── main.js
└── data/
    └── config.json
```

### After Running Compression

```bash
cd my-website
build
```

**Output Structure:**
```
my-website/
├── index.php           (minified)
├── about.html          (minified)
├── contact.php         (minified)
├── css/
│   ├── style.css       (minified)
│   └── index.php       (auto-created)
├── js/
│   ├── main.js         (minified)
│   └── index.php       (auto-created)
├── data/
│   ├── config.json     (minified)
│   └── index.php       (auto-created)
└── dist/               (compressed copy)
    ├── index.php
    ├── about.html
    ├── contact.php
    ├── css/
    │   ├── style.css
    │   └── index.php
    ├── js/
    │   ├── main.js
    │   └── index.php
    └── data/
        ├── config.json
        └── index.php
```

---

## Watch Mode for Development

Automatically compress files when they change:

```bash
php bin/compress --watch /path/to/project
```

The tool will monitor your project and re-compress whenever you save a file. Press `Ctrl+C` to stop watching.

---

## Dry Run Mode

Preview what would happen without actually creating files:

```bash
php bin/compress --dry-run /path/to/project
```

This shows you what files would be processed and how much space would be saved.

---

## Minimum Output Mode

For CI/CD pipelines or scripts:

```bash
php bin/compress --min /path/to/project
```

Output example:
```
Files: 15/20 | Size: 2.5 MB → 1.8 MB | Saved: 28%
```

---

## Requirements

- **PHP Version**: 7.4 or higher
- **Operating System**: Works on Windows, macOS, and Linux
- **Terminal Access**: Command line interface required

---

## Troubleshooting

### Problem: "Permission denied" error

**Solution:** Make the scripts executable
```bash
chmod +x bin/compress
chmod +x bin/build
```

### Problem: "build" command not found

**Solution:** Add the bin folder to your PATH
```bash
export PATH="/users/user-namedDesktop/lib/php-project-minifier/bin:$PATH"
```

### Problem: "Source directory does not exist"

**Solution:** Use the full absolute path
```bash
php bin/compress /users/user-name/my-project
```

### Problem: Want to change output folder

**Solution:** Either update compress.json or specify in command
```bash
# Via config file
# Add to compress.json: "output": "./build"

# Via command
php bin/compress /my-project /my-output-folder
```

---

## How Minification Works

### For PHP Files
- Removes PHP comments (`//` and `/* */`)
- Removes HTML comments (`<!-- -->`)
- Collapses whitespace
- Preserves strings, SQL queries, and HTML inside PHP
- Smart handling of `<?php ?>` tags

### For HTML Files
- Removes comments
- Collapses whitespace between tags
- Preserves content inside `<pre>`, `<textarea>`, `<script>`, `<style>`

### For CSS Files
- Removes comments
- Collapses whitespace
- Preserves content inside strings
- Removes unnecessary spaces around punctuation

### For JavaScript Files
- Removes single-line and multi-line comments
- Collapses whitespace where safe
- Preserves strings, template literals, and regex
- Handles ES6+ syntax properly

### For JSON Files
- Removes all whitespace
- No data loss - just formatting removal

---

## Best Practices

1. **Always test after compression** - Run your application to ensure everything still works
2. **Use .gitignore** - The tool respects your .gitignore rules automatically
3. **Use watch mode during development** - Keep your compressed files updated automatically
4. **Use dry run first** - Preview results before actually compressing
5. **Keep source files** - The tool creates a copy; your original files remain unchanged
6. **Use version control** - Add the output folder (like `dist/`) to your .gitignore

---

## Performance Stats Example

When you run compression, you'll see a detailed report:

```
╔════════════════════════════════════════════╗
║              COMPRESSION RESULTS            ║
╠════════════════════════════════════════════╣
║  Total Files:                    25         ║
║  Compressed:                    20          ║
║  Skipped:                        5          ║
║  Ignored:                        3          ║
╠════════════════════════════════════════════╣
║  Original Size:              2.5 MB        ║
║  Compressed Size:           1.8 MB         ║
║  Saved:                     716.5 KB        ║
║  Reduction:                    28%          ║
╠════════════════════════════════════════════╣
║  Time:                         145ms        ║
╚════════════════════════════════════════════╝
```

---

## Security Note

The auto-created `index.php` files contain a comment `// Silence is golden.` - this is a common PHP security practice to prevent directory listing when there's no proper index file.

---

## Version Information

- **Current Version**: 1.0.0
- **Release Date**: 2026
- **License**: MIT License

---

## Contributing & Contact

### Want to Contribute?

We welcome contributions from the community! If you have ideas to improve this tool or want to add new features:

1. **Fork the repository** - Create your own copy of the project
2. **Make your changes** - Implement your improvements or fixes
3. **Submit your pull request** - Send your changes for review
4. **Our team will review** - We'll check your code and if everything looks good, we'll merge and push it to the main project

### Have Questions or Need Support?

If you have any questions, encounter issues, or need help with this tool, feel free to reach out to the developer directly.

**Contact through:** [arttechfuzion.com](https://arttechfuzion.com)

Visit the website and connect with the developer for:
- Technical support
- Feature requests
- Bug reports
- General inquiries
- Custom implementation help

---
