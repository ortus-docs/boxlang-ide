---
description: >-
  Complete reference of all BoxLang VS Code extension commands organized by
  category — version management, server management, BoxLang Home, execution,
  and CFML tools.
icon: terminal
---

# Commands Reference

The BoxLang extension provides over 40 commands accessible through the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`), context menus, and tree view actions.

{% hint style="info" %}
Commands marked with 🖱️ are primarily accessed through **context menus** or **tree view buttons** rather than the Command Palette.
{% endhint %}

---

## Version Management

Commands for managing BoxLang runtime, LSP, debugger, and MiniServer versions.

| Command | Description |
| --- | --- |
| **BoxLang: Select BoxLang Version** | Choose from installed BoxLang runtime versions. Affects execution and the LSP. |
| **BoxLang: Remove BoxLang Version** | Remove an installed BoxLang runtime version. |
| **BoxLang: Select LSP Version** | Choose the language server version. May require a window reload. |
| **BoxLang: Select Debugger Version** | Choose the debugger module version. |
| **BoxLang: Remove Debugger Version** | Remove an installed debugger version. |
| **BoxLang: Select MiniServer Version** | Choose the MiniServer version used for web server features. |
| **BoxLang: Check for Updates** | Manually check for updates to all BoxLang components. |
| **BoxLang: Reinstall Component** | Reinstall a BoxLang component (runtime, LSP, debugger, or MiniServer). |

---

## Runtime & Execution

Commands for running BoxLang code.

| Command | Description |
| --- | --- |
| **BoxLang: Run File** | Run the current BoxLang script (`.bxs`, `.cfs`) or class (`.bx`, `.cfc`) if it has a `main` function. |
| **BoxLang: Run REPL** | Open the BoxLang REPL (Read-Eval-Print Loop) in the integrated terminal. |
| **BoxLang: Run Web Server** | Start a MiniServer web server from the current workspace. |
| 🖱️ **BoxLang: Run MiniServer Here** | Right-click a folder in the Explorer and start a MiniServer using that folder as web root. |
| **BoxLang: Download Java 21** | Download and configure a compatible Java 21 JRE for the extension. Does not affect your system Java installation. |

---

## Server Management 🖱️

Commands for creating, configuring, and managing BoxLang MiniServers. These appear in the **BoxLang Servers** tree view and context menus.

| Command | Description |
| --- | --- |
| 🖱️ **Add Server** | Create a new MiniServer configuration. Prompts for name, port, web root, and other settings. |
| 🖱️ **Edit Server Property** | Edit an individual server property (port, web root, JVM args, etc.) by clicking the pencil icon. |
| 🖱️ **Run Server** | Start the configured MiniServer. |
| 🖱️ **Debug Server** | Start the MiniServer and attach the debugger. |
| 🖱️ **Stop Server** | Stop a running MiniServer. |
| 🖱️ **Open Browser** | Open the running MiniServer's root URL in your default browser. |
| 🖱️ **Delete Server** | Remove a MiniServer configuration. |

{% hint style="info" %}
Server management commands also appear as **inline action buttons** in the BoxLang Servers tree view — no Command Palette needed.
{% endhint %}

---

## BoxLang Home Management 🖱️

Commands for managing BoxLang Home directories and their contents. These appear in the **BoxLang Homes** tree view.

| Command | Description |
| --- | --- |
| 🖱️ **Add BoxLang Home** | Register a new BoxLang Home directory. |
| 🖱️ **Remove BoxLang Home** | Remove a BoxLang Home registration (cannot remove the default home). |
| 🖱️ **Open BoxLang Home** | Open the BoxLang Home directory in your file manager. |
| 🖱️ **Open BoxLang Config File** | Open the `boxlang.json` configuration file for editing. |
| 🖱️ **Clear Class Files** | Delete compiled class files from the BoxLang Home to force recompilation. |
| 🖱️ **Install BoxLang Module** | Install a module from ForgeBox into the BoxLang Home. |
| 🖱️ **Remove Module** | Remove an installed module from the BoxLang Home. |
| 🖱️ **Open Module Home Page** | Open the module's ForgeBox or documentation page. |
| 🖱️ **Open Log File** | Open the BoxLang server log file. |
| 🖱️ **Clear Log File** | Clear the contents of the log file. |
| **BoxLang: Hard Reset Workspace Home** | Completely reset the workspace-scoped BoxLang Home to its initial state. |

---

## Configuration & Setup

Commands for generating and managing configuration files.

| Command | Description |
| --- | --- |
| **BoxLang: Create .bxlint.json** | Generate a `.bxlint.json` file at the workspace root with all lint rules and their defaults. |
| **BoxLang: Create .bxformat.json** | Generate a `.bxformat.json` file at the workspace root with formatting settings. |
| **BoxLang: Convert .cfformat.json** | Convert an existing `cfformat.json` (from cfformat) to `.bxformat.json` format. |
| **BoxLang: Migrate VSCode Settings** | Migrate legacy settings format to the current format. |

---

## Language Server

Commands for controlling the BoxLang Language Server.

| Command | Description |
| --- | --- |
| **BoxLang: Restart Language Server** | Perform a full restart of the BoxLang Language Server for the current workspace. |
| **BoxLang: Refresh Global Definitions Cache** | Force-refresh the cache of global CFML definitions. |
| **BoxLang: Refresh Workspace Definitions Cache** | Force-refresh the cache of workspace-level component definitions. |

---

## Debugging

Commands available during debugging sessions.

| Command | Description |
| --- | --- |
| 🖱️ **BoxLang: Dump Variable** | In debug mode, right-click in the editor and select to dump a variable's contents to the dump panel. |
| 🖱️ **Dump Variable** | In the Debug Variables panel, right-click a variable and select to dump its contents. |

---

## Navigation & Editor

Commands for navigating and editing BoxLang/CFML code.

| Command | Description |
| --- | --- |
| **BoxLang: Toggle Line Comment** | Toggle a line comment in BoxLang/CFML files. Default keybinding: `Ctrl+/` (`Cmd+/` on Mac). |
| **BoxLang: Toggle Block Comment** | Toggle a block comment. Default keybinding: `Shift+Alt+A`. |
| **BoxLang: Go to Matching Tag** | Jump between opening and closing CFML tags. |
| **BoxLang: Fold All Functions** | Fold all function bodies in the active editor. |
| **BoxLang: Open Application File** | Open the `Application.cfc` or `Application.cfm` file for the currently active document. |

---

## Documentation Lookup

Commands for accessing documentation directly from the editor.

| Command | Description |
| --- | --- |
| **BoxLang: Open CFDocs Page** | Open the CFDocs reference page for the word under the cursor. |
| **BoxLang: Open Engine Docs** | Open the CFML engine documentation page for the word under the cursor. |

---

## Information & Help

Commands for diagnostics and help resources.

| Command | Description |
| --- | --- |
| **BoxLang: Output Version Info** | Display detailed information about the extension version, configuration, and component versions. **Include this output in bug reports.** |
| **BoxLang: Focus on Help & Feedback View** | Open the Help & Feedback panel with quick links to docs, community, Slack, and issue trackers. |

---

## Feature Audit

| Command | Description |
| --- | --- |
| **BoxLang: Open Feature Audit Tool** | Open the Feature Audit webview to analyze BoxLang feature usage across the workspace. |

---

## Context Menu Commands

These commands appear in right-click context menus and are not available in the Command Palette.

### Explorer Context Menu

| Command | When |
| --- | --- |
| **BoxLang: Run File** | Right-click on `.bx`, `.bxs`, `.cfc`, `.cfs` files |
| **BoxLang: Run MiniServer Here** | Right-click on any folder |
| **BoxLang: Open Feature Audit Tool** | Right-click on any folder |

### Editor Context Menu

| Command | When |
| --- | --- |
| **BoxLang: Run File** | When editing BoxLang or CFML files |
| **BoxLang: Dump Variable** | When in debug mode and editing BoxLang/CFML files |

### Debug Variables Context Menu

| Command | When |
| --- | --- |
| **Dump Variable** | When debugging a BoxLang session, right-click a variable in the Variables panel |

---

## Keybindings

| Keybinding | Command | When |
| --- | --- | --- |
| `Ctrl+/` (`Cmd+/` on Mac) | Toggle Line Comment | In BoxLang or CFML files |
| `Shift+Alt+A` | Toggle Block Comment | In BoxLang or CFML files |

---

## Related Pages

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="debugging.md" %}
{% endcontent-ref %}

{% content-ref url="version-management.md" %}
{% endcontent-ref %}

{% content-ref url="miniserver.md" %}
{% endcontent-ref %}

{% content-ref url="boxlang-home-configuration.md" %}
{% endcontent-ref %}
