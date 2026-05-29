---
description: >-
  How to install the BoxLang IntelliJ plugin — from JetBrains Marketplace,
  manual installation from disk, and post-installation configuration.
icon: download
---

# Installation

Install the **BoxLang IDE** plugin to add BoxLang language support to your JetBrains IDE.

---

## Requirements

Before installing, ensure your system meets these requirements:

| Requirement | Minimum Version |
| --- | --- |
| **IntelliJ IDEA** | 2024.2 or later |
| **Java** | 21 or later (for running BoxLang) |
| **Operating System** | Windows, macOS, or Linux |

The plugin works with both **IntelliJ IDEA Community** and **IntelliJ IDEA Ultimate**.

---

## Install from JetBrains Marketplace (Recommended)

### Method 1: From Within the IDE

1. Open IntelliJ IDEA
2. Open **Settings** (Windows/Linux) or **Preferences** (macOS)
   - Keyboard shortcut: **Ctrl+Alt+S** (Windows/Linux) or **Cmd+,** (macOS)
3. Navigate to **Plugins**
4. Click the **Marketplace** tab
5. Search for `BoxLang IDE`
6. Click **Install** next to the plugin
7. Click **Restart IDE** when prompted

### Method 2: From the JetBrains Website

1. Visit the [BoxLang IDE plugin page](https://plugins.jetbrains.com/plugin/30311-boxlang-ide)
2. Click **Install to IDE**
3. Select your IntelliJ IDEA installation
4. Follow the prompts to complete installation
5. Restart the IDE when prompted

---

## Manual Installation from Disk

If you cannot access the Marketplace or need to install a specific version:

### Download the Plugin

1. Visit the [GitHub Releases page](https://github.com/ortus-boxlang/intellij-boxlang/releases)
2. Download the latest `.zip` file (e.g., `intellij-boxlang-1.0.0.zip`)

### Install in IntelliJ

1. Open IntelliJ IDEA
2. Open **Settings** (Windows/Linux) or **Preferences** (macOS)
3. Navigate to **Plugins**
4. Click the **gear icon** ⚙️ in the top-right
5. Select **Install Plugin from Disk...**
6. Browse to and select the downloaded `.zip` file
7. Click **OK**
8. Restart the IDE when prompted

---

## Post-Installation Setup

After installing the plugin, configure your BoxLang environment:

### Step 1: Configure BoxLang Settings

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Configure the following:

**Runtime Configuration:**
- **BoxLang Home** — Directory for BoxLang configuration (default: `~/.boxlang`)
- **Java Home** — Path to Java 21+ installation (leave empty for system default)
- **Use .bvmrc** — Enable to read version from `.bvmrc` files

**LSP Configuration:**
- **Max Heap Size** — Memory for LSP server (default: 512 MB, range: 64-8192 MB)
- **LSP Modules** — Additional BoxLang modules (e.g., `bx-esapi, bx-pdf`)

3. Click **Apply**

### Step 2: Download BoxLang Runtime

The plugin will prompt you to download the BoxLang runtime:

1. Click **Download** next to **BoxLang Runtime**
2. Select a version (recommended: **Latest**)
3. Wait for the download to complete
4. The plugin automatically downloads the LSP and debugger modules

### Step 3: Create Your First BoxLang File

1. Right-click in the Project view
2. Select **New → BoxLang File**
3. Choose **BoxLang Script**
4. Name it `HelloWorld`
5. Add this code:

```javascript
// HelloWorld.bxs
writeOutput("Hello, BoxLang!");
```

6. Click the green play icon ▶️ in the gutter to run it

---

## Verify Installation

### Check Plugin Status

1. Open **Settings → Plugins → Installed**
2. Verify **BoxLang IDE** appears in the list
3. Check that it's enabled (checkbox is checked)

### Check BoxLang Runtime

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Verify the status panels show:
   - **BoxLang Runtime:** Installed (with version number)
   - **LSP Module:** Installed (with version number)
   - **Debugger Module:** Installed (with version number)

### Test Code Intelligence

1. Create a new BoxLang file
2. Type `array` and press **Ctrl+Space**
3. You should see completion suggestions like `arrayAppend()`, `arrayLen()`, etc.

### Test Run Configuration

1. Create a simple script:
   ```javascript
   writeOutput("Test successful!");
   ```
2. Click the green play icon ▶️ in the gutter
3. Select **Run 'filename'**
4. The Run tool window should show "Test successful!"

---

## Troubleshooting Installation

### Plugin Not Appearing in Marketplace

**Symptoms:** Cannot find "BoxLang IDE" in the Marketplace

**Solutions:**
1. Verify your IntelliJ version is 2024.2 or later
2. Check your internet connection
3. Try installing manually from disk (see above)
4. Visit the [plugin page](https://plugins.jetbrains.com/plugin/30311-boxlang-ide) directly

### Installation Fails

**Symptoms:** Error during installation or plugin doesn't load

**Solutions:**
1. Check IDE logs: **Help → Show Log in Finder/Explorer**
2. Verify you have write permissions to the plugins directory
3. Try installing manually from disk
4. Restart the IDE and try again

### Plugin Loads but Features Don't Work

**Symptoms:** Plugin is installed but no code intelligence or run configurations

**Solutions:**
1. Verify BoxLang runtime is downloaded in settings
2. Check Java 21+ is installed and configured
3. Restart the IDE
4. Check IDE logs for errors

### Java Version Issues

**Symptoms:** "Java 21 or later is required"

**Solutions:**
1. Install Java 21 or later:
   ```bash
   # macOS (Homebrew)
   brew install openjdk@21

   # Ubuntu/Debian
   sudo apt install openjdk-21-jdk
   ```
2. Configure Java Home in BoxLang settings
3. Or leave Java Home empty to use system default

---

## Updating the Plugin

### Automatic Updates

IntelliJ automatically checks for plugin updates:

1. Open **Settings → Plugins → Installed**
2. If an update is available, click **Update**
3. Restart the IDE when prompted

### Manual Updates

To manually check for updates:

1. Open **Settings → Plugins → Installed**
2. Click the **gear icon** ⚙️
3. Select **Check for Updates**
4. If an update is available, click **Update**

### Downgrading

To install an older version:

1. Uninstall the current version
2. Download the desired version from [GitHub Releases](https://github.com/ortus-boxlang/intellij-boxlang/releases)
3. Install manually from disk (see above)

---

## Uninstalling the Plugin

1. Open **Settings → Plugins → Installed**
2. Find **BoxLang IDE** in the list
3. Click the **gear icon** ⚙️ next to it
4. Select **Uninstall**
5. Restart the IDE when prompted

### Clean Up Cache (Optional)

To remove all cached BoxLang components:

```bash
# macOS
rm -rf ~/Library/Caches/JetBrains/IntelliJIdea*/boxlang

# Windows
rmdir /s %LOCALAPPDATA%\JetBrains\IntelliJIdea*\boxlang

# Linux
rm -rf ~/.cache/JetBrains/IntelliJIdea*/boxlang
```

---

## Next Steps

After installation:

- [Overview](overview.md) — Learn about all plugin features
- [Settings Reference](settings-reference.md) — Configure the plugin
- [Run Configurations](run-configurations.md) — Run BoxLang scripts
- [Debugging](debugging.md) — Debug BoxLang applications
- [TestBox Integration](testbox-integration.md) — Run and debug tests

---

## Getting Help

If you encounter issues:

- **Documentation:** [boxlang-ide.ortusbooks.com](https://boxlang-ide.ortusbooks.com)
- **GitHub Issues:** [github.com/ortus-boxlang/intellij-boxlang/issues](https://github.com/ortus-boxlang/intellij-boxlang/issues)
- **Community Forum:** [community.ortussolutions.com](https://community.ortussolutions.com)
- **Slack:** [boxteam.ortussolutions.com](https://boxteam.ortussolutions.com)
