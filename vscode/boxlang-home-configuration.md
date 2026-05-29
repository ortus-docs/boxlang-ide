---
description: >-
  The BoxLang Homes panel — manage BoxLang Home directories, modules, logs,
  and class files from the VS Code sidebar.
icon: house-chimney-heart
---

# BoxLang Home Configuration

The **BoxLang Homes** panel provides a central interface for managing BoxLang Home directories directly within VS Code. It appears in the BoxLang sidebar alongside the Servers and Help panels.

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="260"><figcaption></figcaption></figure>

---

## What is BoxLang Home?

**BoxLang Home** (`~/.boxlang` by default) is the directory where BoxLang stores:

- **Configuration** — `boxlang.json` runtime settings
- **Modules** — Installed BoxLang modules from ForgeBox
- **Class files** — Compiled BoxLang classes (cache)
- **Logs** — Runtime and application log files
- **Custom tags** — User-defined custom tag libraries

---

## Panel Structure

The BoxLang Homes tree view displays:

```
🏠 Default Home (~/.boxlang)
├── 📄 boxlang.json (Config File)
├── 📁 modules/
│   └── 📦 bx-compat-cfml (Module)
├── 📁 logs/
│   └── 📄 boxlang.log
└── 📁 classes/
```

Each registered BoxLang Home appears as a top-level item with nested folders and files.

---

## Actions

### Top-Level Home Actions

Hover over a BoxLang Home to reveal action buttons:

| Action | Description |
| --- | --- |
| **Clear Class Files** 🗑️ | Delete all compiled `.class` files. Useful after upgrading BoxLang or when experiencing class caching issues. |
| **Open BoxLang Home** 📂 | Open the BoxLang Home directory in your system file manager. |
| **Delete Home** 🗑️ | Remove a registered BoxLang Home. **Cannot delete the default home.** |
| **Open Config File** ✏️ | Open `boxlang.json` for editing. |

### Log Actions

Hover over a log file in the tree:

| Action | Description |
| --- | --- |
| **Open Log** 📄 | Open the log file in the editor. Useful for inspecting runtime errors and warnings. |
| **Clear Log** 🗑️ | Clear the log file contents. Useful for focusing on recent activity. |

### Module Actions

The **modules** directory and individual modules have their own actions.

**On the modules directory:**

| Action | Description |
| --- | --- |
| **Install Module** ➕ | Install a BoxLang module from ForgeBox. Prompts for the module slug (e.g., `bx-compat-cfml`). |

**On an installed module:**

| Action | Description |
| --- | --- |
| **Remove Module** 🗑️ | Uninstall the module from this BoxLang Home. |
| **Open Module Home Page** 🌐 | Open the module's ForgeBox page or documentation in your browser. |

---

## Installing Modules

Modules extend BoxLang with additional functionality — compatibility layers, premium features, framework integrations, and more.

### From the Panel

1. In the BoxLang Homes panel, expand a BoxLang Home.
2. Hover over the **modules** folder and click ➕ **Install Module**.
3. Enter the module slug when prompted (e.g., `bx-compat-cfml`).
4. The module is downloaded from ForgeBox and installed.

### Common Modules

| Module | Slug | Purpose |
| --- | --- | --- |
| CFML Compatibility | `bx-compat-cfml` | Compatibility layer for CFML code |
| PDF | `bx-pdf` | PDF generation and manipulation |
| Redis | `bx-redis` | Redis cache and session provider |
| CSV | `bx-csv` | CSV file processing |
| Spreadsheet | `bx-spreadsheet` | Excel/Spreadsheet operations |

{% hint style="info" %}
Modules installed in the **default** BoxLang Home are available to all projects. To install project-specific modules, use a workspace-scoped BoxLang Home or `boxlang.json` `modulesDirectory`.
{% endhint %}

---

## Managing Multiple Homes

You can register multiple BoxLang Home directories:

1. Click the ➕ button in the BoxLang Homes tree view title bar.
2. Select or enter the path to a BoxLang Home directory.
3. The new home appears in the tree view with its own modules, logs, and config.

**Use cases for multiple homes:**

- **Project isolation** — Separate homes for different projects
- **Version testing** — Test against different BoxLang configurations
- **Team environments** — Shared home directory with pre-installed modules

---

## Related Pages

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="project-configuration.md" %}
{% endcontent-ref %}

{% content-ref url="miniserver.md" %}
{% endcontent-ref %}
