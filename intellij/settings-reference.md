---
description: >-
  Complete reference for all BoxLang IntelliJ plugin settings — application-level
  and project-level configuration for runtime, LSP, debugger, and more.
icon: sliders
---

# Settings Reference

The BoxLang IntelliJ plugin provides two levels of configuration: **application-level** (global) settings that apply to all projects, and **project-level** overrides for team collaboration.

Access settings via **Settings → Languages & Frameworks → BoxLang**.

---

## Application-Level Settings

Application-level settings are global defaults that apply to all BoxLang projects unless overridden at the project level.

### Runtime Configuration

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| **BoxLang Runtime** | Status panel | Not installed | Shows current runtime status with Download/Change/Delete actions |
| **BoxLang Home** | Path | `~/.boxlang` | Directory for BoxLang configuration, modules, and logs |
| **Java Home** | Path | System default | Path to Java 21+ installation. Leave empty to use system Java |
| **Use .bvmrc** | Checkbox | Enabled | When enabled, reads BoxLang version from `.bvmrc` file in project root |

### LSP Configuration

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| **LSP Module** | Status panel | Not installed | Shows current LSP status with Download/Change/Delete actions |
| **LSP BoxLang Version** | Text | (runtime version) | BoxLang version used by the LSP server. Leave empty to match runtime |
| **LSP BoxLang Home** | Path | (runtime home) | BoxLang home directory for the LSP server. Leave empty to match runtime |
| **LSP Modules** | Text | (empty) | Comma-separated list of BoxLang modules to install in LSP home (e.g., `bx-esapi, bx-pdf`) |
| **LSP JVM Args** | Text | (empty) | Additional JVM arguments for the LSP server process |
| **LSP Module Path** | Path | (auto) | Path to LSP module JAR. Leave empty for automatic management |
| **Max Heap Size** | Spinner | 512 MB | Maximum heap size for LSP server (64-8192 MB, step 64) |

### Debugger Configuration

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| **Debugger Module** | Status panel | Not installed | Shows current debugger status with Download/Change/Delete actions |
| **Debugger Module Path** | Path | (auto) | Path to debugger module JAR. Leave empty for automatic management |

---

## Project-Level Settings

Project-level settings override application-level defaults for the current project. Access via **Settings → Languages & Frameworks → BoxLang → Project Overrides**.

All settings from the application level can be overridden at the project level. This is useful for:

- **Team collaboration** — Share project-specific BoxLang versions
- **Multi-project workspaces** — Different BoxLang versions per project
- **Testing** — Try new BoxLang versions without affecting global settings

---

## Runtime Management Actions

The runtime, LSP, and debugger status panels provide three actions:

| Action | When Available | Description |
| --- | --- | --- |
| **Download** | Not installed | Download and install the latest version from ForgeBox/S3 |
| **Change** | Installed | Select a different version from available versions |
| **Delete** | Installed | Remove the installed version from the cache |

Clicking the **path link** opens the installation directory in your system file browser.

---

## .bvmrc Support

When **Use .bvmrc** is enabled, the plugin reads the BoxLang version from a `.bvmrc` file in the project root:

```
1.13.0
```

Or use `latest` for the most recent version:

```
latest
```

The `.bvmrc` version takes precedence over the configured runtime version.

---

## Storage Locations

The plugin stores downloaded components in the IDE's system directory:

| Component | Location |
| --- | --- |
| **Runtime versions** | `{IDE_SYSTEM}/boxlang/runtimes/{version}/` |
| **LSP modules** | `{IDE_SYSTEM}/boxlang/lsp/{version}/` |
| **Debugger modules** | `{IDE_SYSTEM}/boxlang/debugger/{version}/` |

Each version directory contains the JAR file and a `version.json` metadata file.

---

## Related Pages

- [Installation](installation.md)
- [Runtime Management](runtime-management.md)
- [Run Configurations](run-configurations.md)
- [Debugging](debugging.md)
