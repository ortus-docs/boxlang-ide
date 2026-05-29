---
description: >-
  How BoxLang version management works — .bvmrc, runtime versions, LSP
  versions, debugger versions, MiniServer versions, and update modes.
icon: code-branch
---

# Version Management

The BoxLang extension manages multiple versioned components: the BoxLang runtime, the Language Server Protocol (LSP) module, the debugger, and the MiniServer. Each can be independently selected, updated, and configured.

---

## Components

| Component | Purpose | Default Version |
| --- | --- | --- |
| **BoxLang Runtime** | Executes BoxLang code, powers the debugger and CLI features. | `1.13.0` |
| **LSP** | Provides language intelligence (diagnostics, completions, hover). | `bx-lsp@1.10.0+9` |
| **Debugger** | Enables breakpoints, variable inspection, and step debugging. | `legacy` (built-in) or `bx-debugger` module |
| **MiniServer** | Lightweight web server for local development and testing. | Version-managed |

---

## How Versions Are Stored

Versions are downloaded from AWS S3 and cached locally:

- **Runtime versions:** `{globalStorage}/boxlang_versions/`
- **LSP versions:** `{globalStorage}/lspVersions/`
- **Each version folder** contains the JAR file and a `version.json` metadata file.

---

## .bvmrc — Per-Workspace Version Pinning

Create a `.bvmrc` file in your workspace root to pin a specific BoxLang version for that project. This is the equivalent of `.nvmrc` for Node.js or `.sdkmanrc` for Java.

### Format

A `.bvmrc` file contains a single line with a version string:

```
1.13.0
```

Or use `latest` to always use the most recent version:

```
latest
```

### Valid Formats

| Format | Example | Description |
| --- | --- | --- |
| Full version | `1.13.0` | Pin to a specific release |
| Minor version | `1.13` | Pin to the latest patch of a minor release |
| Major version | `1` | Pin to the latest release of a major version |
| `latest` | `latest` | Always use the newest available version |

### How It Works

1. The extension watches for `.bvmrc` files in all workspace folders.
2. The first valid `.bvmrc` file found sets the BoxLang version for the workspace.
3. The version is automatically downloaded if not already cached.
4. Changes to `.bvmrc` are detected live — no restart needed.
5. The status bar shows the active version.

{% hint style="info" %}
The `.bvmrc` version takes **precedence** over `boxlang.boxlangVersion` in settings.
{% endhint %}

---

## Version Selection Commands

Use these commands to manage versions interactively:

| Command | Description |
| --- | --- |
| **BoxLang: Select BoxLang Version** | Choose from installed runtime versions. Also triggers download of available versions. |
| **BoxLang: Select LSP Version** | Choose the language server version. May require a window reload. |
| **BoxLang: Select Debugger Version** | Choose the debugger module version. |
| **BoxLang: Select MiniServer Version** | Choose the MiniServer version. |
| **BoxLang: Remove BoxLang Version** | Remove an installed runtime version to free disk space. |
| **BoxLang: Remove Debugger Version** | Remove an installed debugger version. |
| **BoxLang: Check for Updates** | Manually check all components for newer versions. |

---

## Update Modes

Each component has its own update mode setting that controls how it checks for and applies new versions:

| Component | Setting | Default |
| --- | --- | --- |
| LSP | `boxlang.lsp.versionUpdateMode` | `auto` |
| Debugger | `boxlang.debugger.versionUpdateMode` | `auto` |
| Runtime | `boxlang.updates.runtime` | `prompt` |
| MiniServer | `boxlang.updates.miniserver` | `prompt` |

### Mode Behavior

| Mode | Behavior |
| --- | --- |
| `auto` | Automatically download and apply the latest version without prompting. |
| `prompt` | Check for updates and show a notification asking whether to download (default for runtime). |
| `manual` | Never check for updates automatically. Use **BoxLang: Check for Updates** to check manually. |

---

## Pre-Release Versions

Pre-release versions (snapshots, betas, alphas) are excluded from update checks by default. Enable them with:

```json
{
  "boxlang.updates.preRelease": true
}
```

When enabled, update checks include all available versions, not just stable releases.

{% hint style="warning" %}
Pre-release versions may contain unstable features or bugs. Use them for testing, not production.
{% endhint %}

---

## Release vs Pre-Release (Extension)

The VS Code extension itself follows VS Code's pre-release convention:

- **Release:** Minor version is **even** (e.g., `1.18.0`, `1.20.0`)
- **Pre-release:** Minor version is **odd** (e.g., `1.19.0`, `1.21.0`)

Switch between release and pre-release on the extension page in the VS Code Marketplace.

---

## Custom JAR Paths

For advanced scenarios, you can bypass version management and point directly to custom JAR files:

| Setting | Purpose |
| --- | --- |
| `boxlang.jarpath` | Custom BoxLang runtime JAR |
| `boxlang.lspjarpath` | Custom LSP JAR |
| `boxlang.miniserverjarpath` | Custom MiniServer JAR |

When a custom JAR path is set, version management is bypassed for that component.

---

## Debugger Modes

The debugger supports two implementation strategies:

### Legacy Mode (Default)

```json
{
  "boxlang.debugger.mode": "legacy"
}
```

Uses the debugger built into the BoxLang runtime JAR. No separate download needed.

### Module Mode

```json
{
  "boxlang.debugger.mode": "module",
  "boxlang.debugger.moduleName": "bx-debugger",
  "boxlang.debugger.moduleVersion": "1.0.0-snapshot"
}
```

Uses a debugger module from ForgeBox, managed independently from the runtime. This allows the debugger to be updated separately.

{% hint style="info" %}
Module mode requires the module to be available on ForgeBox. Configure `boxlang.debugger.moduleName` and `boxlang.debugger.moduleVersion` to specify which module and version to use.
{% endhint %}

---

## Troubleshooting

### Version Not Found

If a version fails to download:
1. Check your internet connection — versions are downloaded from AWS S3.
2. Run **BoxLang: Check for Updates** to refresh the available versions list.
3. Verify the version format in `.bvmrc` is valid (numeric or `latest`).
4. Check the BoxLang output channel (`View` → `Output` → `BoxLang`) for download errors.

### Stuck on Old Version

If the extension is not using the expected version:
1. Check if `.bvmrc` overrides your settings.
2. Check if a custom JAR path is set (`boxlang.jarpath`, etc.).
3. Run **BoxLang: Output Version Info** to see which versions are active.
4. Try **BoxLang: Hard Reset Workspace Home** to reset the workspace environment.

### Disk Space

Versions accumulate over time. Remove unused versions:
- **BoxLang: Remove BoxLang Version** for runtimes
- **BoxLang: Remove Debugger Version** for debugger modules
- Manually: delete folders from `{globalStorage}/boxlang_versions/`

---

## Related Pages

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="debugging.md" %}
{% endcontent-ref %}

{% content-ref url="project-configuration.md" %}
{% endcontent-ref %}
