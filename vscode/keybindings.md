---
description: >-
  All BoxLang VS Code extension keybindings and context menu actions —
  keyboard shortcuts, right-click menus, and tree view actions.
icon: keyboard
---

# Keybindings & Context Menus

The BoxLang extension provides keyboard shortcuts and context menu actions for common editing and navigation tasks.

---

## Keyboard Shortcuts

| Keybinding | Mac | Command | When |
| --- | --- | --- | --- |
| `Ctrl+/` | `Cmd+/` | **Toggle Line Comment** | In BoxLang or CFML files |
| `Shift+Alt+A` | `Shift+Alt+A` | **Toggle Block Comment** | In BoxLang or CFML files |

{% hint style="info" %}
These keybindings can be customized in VS Code's **Keyboard Shortcuts** editor (`Ctrl+K Ctrl+S` / `Cmd+K Cmd+S`). Search for `boxlang` to see all extension keybindings.
{% endhint %}

---

## Context Menus

### Explorer (Right-Click a File or Folder)

| Menu Item | When Available | Description |
| --- | --- | --- |
| **BoxLang: Run File** | Right-click on `.bx`, `.bxs`, `.cfc`, `.cfs` files | Run the selected BoxLang file. |
| **BoxLang: Run MiniServer Here** | Right-click on any folder | Start a MiniServer using the selected folder as the web root. |
| **BoxLang: Open Feature Audit Tool** | Right-click on any folder | Open the Feature Audit tool for the selected folder. |

### Editor (Right-Click in Code)

| Menu Item | When Available | Description |
| --- | --- | --- |
| **BoxLang: Run File** | In BoxLang or CFML files | Run the current file. |
| **BoxLang: Dump Variable** | In debug mode, BoxLang/CFML files | Dump the selected variable to the dump panel. |

### Debug Variables Panel (Right-Click a Variable)

| Menu Item | When Available | Description |
| --- | --- | --- |
| **Dump Variable** | During a BoxLang debug session | Open a rich HTML visualization of the variable's contents. |

---

## Tree View Actions

### BoxLang Servers Tree

Actions appear as **inline buttons** when hovering over a server item:

| Icon | Action | When Available |
| --- | --- | --- |
| ▶️ **Run** | Start the MiniServer | Server is stopped |
| 🐞 **Debug** | Start and debug the MiniServer | Server is running |
| ⏹️ **Stop** | Stop the MiniServer | Server is running |
| 🌐 **Open Browser** | Open the server in browser | Server is running |
| ✏️ **Edit** | Edit a server property | Server is stopped |
| 🗑️ **Delete** | Remove the server | Server is stopped |

### BoxLang Homes Tree

Actions appear as **inline buttons** when hovering over items:

| Icon | Action | When Available |
| --- | --- | --- |
| 🗑️ **Clear Class Files** | Delete compiled classes | On a BoxLang Home |
| 📂 **Open Home** | Open in file manager | On a BoxLang Home |
| 🗑️ **Remove Home** | Remove Home registration | On non-default homes |
| 📄 **Open Log** | Open log file | On a log file item |
| 🗑️ **Clear Log** | Clear log contents | On a log file item |
| ➕ **Install Module** | Install from ForgeBox | On the modules directory |
| 🗑️ **Remove Module** | Remove installed module | On a module item |
| 🌐 **Module Home Page** | Open module documentation | On a module item |

### Tree View Title Bar

| Button | Action |
| --- | --- |
| ➕ (Servers tree) | **Add Server** — Create a new MiniServer |
| ➕ (Homes tree) | **Add BoxLang Home** — Register a new BoxLang Home |

---

## Disabled Command Palette Entries

Some commands are intentionally hidden from the Command Palette because they are contextual. These only appear in tree views or context menus:

- All Server management commands (add, edit, delete, run, stop, debug, open browser)
- All BoxLang Home management commands (add, remove, open, clear, install module, etc.)
- **BoxLang: Run MiniServer Here** (Explorer context menu only)
- **BoxLang: Run Web Server** (legacy)

---

## Related Pages

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="miniserver.md" %}
{% endcontent-ref %}

{% content-ref url="boxlang-home-configuration.md" %}
{% endcontent-ref %}
