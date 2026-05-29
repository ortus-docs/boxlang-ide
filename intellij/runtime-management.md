---
description: >-
  How the BoxLang IntelliJ plugin manages runtime versions — automatic downloads,
  version selection, .bvmrc support, and cache management.
icon: download
---

# Runtime Management

The BoxLang IntelliJ plugin automatically manages BoxLang runtime versions, LSP modules, and debugger modules. It downloads components on demand and caches them locally for fast startup.

---

## Automatic Downloads

When you first open a BoxLang project or configure settings, the plugin can automatically download required components:

### Runtime

The BoxLang runtime is the core execution engine. The plugin:

1. Checks if a runtime is configured in settings
2. Downloads the specified version from the Ortus S3 bucket
3. Caches it in the IDE system directory
4. Uses it for all run configurations

### LSP Module

The Language Server Protocol module provides code intelligence. The plugin:

1. Downloads the LSP module from ForgeBox
2. Installs it in the LSP cache directory
3. Starts the LSP server automatically
4. Restarts the server when settings change

### Debugger Module

The debugger module enables debugging support. The plugin:

1. Downloads the debugger module from ForgeBox
2. Installs it in the debugger cache directory
3. Uses it when starting debug sessions

---

## Version Selection

### Selecting a Runtime Version

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Click **Change** next to **BoxLang Runtime**
3. Select a version from the list:
   - **Latest** — Most recent stable release
   - **Specific version** — Choose from available versions
4. Click **OK**
5. The plugin downloads and installs the selected version

### Selecting an LSP Version

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Click **Change** next to **LSP Module**
3. Select a version from the list
4. Click **OK**
5. The LSP server restarts with the new version

### Selecting a Debugger Version

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Click **Change** next to **Debugger Module**
3. Select a version from the list
4. Click **OK**

---

## .bvmrc Support

The plugin supports `.bvmrc` files for project-specific BoxLang versions:

### How It Works

1. Plugin checks for `.bvmrc` in the project root
2. Reads the version string (e.g., `1.13.0` or `latest`)
3. Downloads that version if not already cached
4. Uses it for all run configurations in that project

### .bvmrc Format

Create a `.bvmrc` file in your project root:

```
1.13.0
```

Or use `latest` for the most recent version:

```
latest
```

### Enabling .bvmrc

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Check **Use .bvmrc for BoxLang version**
3. Click **Apply**

### Priority Order

When multiple version sources exist, the plugin uses this priority:

1. **.bvmrc file** (if enabled and present)
2. **Project-level settings** (if configured)
3. **Application-level settings** (global default)

---

## Cache Management

### Cache Locations

The plugin stores downloaded components in the IDE system directory:

| Component | Location |
| --- | --- |
| **Runtime** | `{IDE_SYSTEM}/boxlang/runtimes/{version}/` |
| **LSP** | `{IDE_SYSTEM}/boxlang/lsp/{version}/` |
| **Debugger** | `{IDE_SYSTEM}/boxlang/debugger/{version}/` |

**Finding the IDE System Directory:**

- **macOS:** `~/Library/Caches/JetBrains/IntelliJIdea{VERSION}`
- **Windows:** `%LOCALAPPDATA%\JetBrains\IntelliJIdea{VERSION}`
- **Linux:** `~/.cache/JetBrains/IntelliJIdea{VERSION}`

### Deleting Cached Versions

To free disk space or force a re-download:

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Click **Delete** next to the component
3. Confirm the deletion
4. The plugin will re-download when needed

### Manual Cache Cleanup

You can manually delete cached versions:

```bash
# macOS example
rm -rf ~/Library/Caches/JetBrains/IntelliJIdea2024.2/boxlang/runtimes/1.12.0
```

---

## Version Information

### Viewing Installed Versions

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Check the status panels:
   - **BoxLang Runtime** — Shows installed version and path
   - **LSP Module** — Shows installed version and path
   - **Debugger Module** — Shows installed version and path

### Checking for Updates

The plugin does not automatically check for updates. To update:

1. Click **Change** next to a component
2. Select **Latest** or a newer version
3. The plugin downloads and installs it

---

## Troubleshooting

### Download Failures

**Symptoms:** "Failed to download BoxLang runtime"

**Solutions:**
1. Check internet connection
2. Verify firewall allows HTTPS connections to `ortus-boxlang.s3.amazonaws.com`
3. Try downloading manually and configuring a custom path
4. Check IDE logs: **Help → Show Log in Finder/Explorer**

### Version Not Found

**Symptoms:** "BoxLang version 1.99.0 not found"

**Solutions:**
1. Verify the version exists on [ForgeBox](https://forgebox.io)
2. Use **Latest** instead of a specific version
3. Check for typos in `.bvmrc` file

### LSP Not Starting

**Symptoms:** No code intelligence features

**Solutions:**
1. Verify LSP module is installed in settings
2. Check Java 21+ is configured
3. Increase LSP heap size (e.g., 1024 MB)
4. Restart the IDE

### .bvmrc Not Working

**Symptoms:** Plugin uses wrong version despite `.bvmrc`

**Solutions:**
1. Verify **Use .bvmrc** is enabled in settings
2. Check `.bvmrc` is in the project root (not a subdirectory)
3. Verify `.bvmrc` contains only the version string (no extra whitespace)
4. Restart the IDE to reload the configuration

---

## Best Practices

### Use .bvmrc for Projects

Always use `.bvmrc` for project-specific versions:

```bash
# In your project root
echo "1.13.0" > .bvmrc
```

This ensures all team members use the same BoxLang version.

### Pin LSP to Runtime Version

Leave **LSP BoxLang Version** empty to match the runtime version automatically. This prevents version mismatches.

### Regular Updates

Periodically update to the latest versions:

1. Click **Change** next to each component
2. Select **Latest**
3. Test your project
4. Commit `.bvmrc` with the new version

### Clean Old Versions

Periodically delete old cached versions to free disk space:

1. Open settings
2. Click **Delete** for old versions
3. Or manually clean the cache directory

---

## Related Pages

- [Settings Reference](settings-reference.md)
- [LSP Features](lsp-features.md)
- [Run Configurations](run-configurations.md)
