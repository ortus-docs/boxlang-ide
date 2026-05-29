---
description: >-
  Language Server Protocol features in the BoxLang IntelliJ plugin — diagnostics,
  semantic tokens, structure view, completions, and hover information.
icon: code
---

# LSP Features

The BoxLang IntelliJ plugin integrates with the BoxLang Language Server Protocol (LSP) to provide intelligent code assistance. The LSP runs as a separate process and communicates with the IDE to deliver real-time language features.

---

## Features Overview

| Feature | Description | Status |
| --- | --- | --- |
| **Semantic Tokens** | Enhanced syntax highlighting based on semantic meaning | ✅ Active |
| **Diagnostics** | Real-time error and warning reporting | ✅ Active |
| **Document Symbols** | Structure view with classes, methods, and properties | ✅ Active |
| **Completions** | Context-aware code completion suggestions | ✅ Active |
| **Hover Information** | Documentation and type information on hover | ✅ Active |
| **Go to Definition** | Navigate to symbol definitions | ✅ Active |
| **Find References** | Find all usages of a symbol | ✅ Active |
| **Code Actions** | Quick fixes and refactoring suggestions | ✅ Active |

---

## Semantic Tokens

Semantic tokens provide enhanced syntax highlighting beyond what the lexer can detect:

| Token Type | Example | Highlighting |
| --- | --- | --- |
| **Class** | `UserService` | Class name color |
| **Method** | `getUser()` | Method name color |
| **Property** | `user.name` | Property color |
| **Variable** | `local count` | Variable color |
| **Parameter** | `function(name)` | Parameter color |
| **Keyword** | `if`, `for`, `return` | Keyword color |
| **String** | `"hello"` | String color |
| **Number** | `42`, `3.14` | Number color |
| **Comment** | `// comment` | Comment color |
| **Operator** | `+`, `==`, `&&` | Operator color |

### Customizing Colors

1. Open **Settings → Editor → Color Scheme → BoxLang**
2. Adjust colors for each semantic token type
3. Changes apply immediately

---

## Diagnostics

The LSP reports errors and warnings in real-time as you type:

### Diagnostic Types

| Severity | Icon | Description |
| --- | --- | --- |
| **Error** | 🔴 | Syntax errors, type mismatches, undefined symbols |
| **Warning** | 🟡 | Potential issues, deprecated features, style violations |
| **Information** | 🔵 | Hints and suggestions |
| **Hint** | ⚪ | Minor style issues |

### Viewing Diagnostics

- **Inline** — Squiggly underlines in the editor
- **Problems Tool Window** — **View → Tool Windows → Problems** (Cmd+9 / Alt+9)
- **Status Bar** — Error/warning count at bottom right

### Common Diagnostics

**Syntax Errors:**
```
Unexpected token '}' at line 42
```

**Undefined Variables:**
```
Variable 'userService' is not defined
```

**Type Mismatches:**
```
Cannot assign String to Numeric
```

**Missing Imports:**
```
Cannot resolve symbol 'ArrayList'
```

---

## Document Symbols (Structure View)

The **Structure** tool window shows the outline of your BoxLang files:

**Open Structure View:**
- **View → Tool Windows → Structure** (Cmd+7 / Alt+7)
- Or press **Cmd+F12** (Ctrl+F12)

### Symbol Types

| Icon | Symbol | Description |
| --- | --- | --- |
| 📦 | Component | BoxLang class/component |
| 🔧 | Method | Function or method |
| 📋 | Property | Component property |
| 🏷️ | Variable | Local or scoped variable |
| 📄 | File | Included file |

### Navigation

- Click a symbol to jump to its location
- Use the search box to filter symbols
- Expand/collapse nested symbols

---

## Code Completion

The LSP provides context-aware completions as you type:

### Completion Types

| Type | Trigger | Example |
| --- | --- | --- |
| **Keywords** | Start of statement | `if`, `for`, `function` |
| **Variables** | After scope prefix | `variables.`, `local.`, `arguments.` |
| **Methods** | After `.` on object | `userService.get` → `getUser()` |
| **Properties** | After `.` on component | `user.` → `name`, `email` |
| **BIFs** | Function call context | `array` → `arrayAppend()`, `arrayLen()` |
| **Classes** | After `new` | `new ` → `ArrayList`, `HashMap` |
| **Snippets** | Code patterns | `for` → `for (var i = 1; i <= 10; i++)` |

### Completion Features

- **Parameter hints** — Shows function signature
- **Documentation** — Displays Javadoc-style comments
- **Auto-import** — Adds missing imports automatically
- **Smart completion** — Filters by expected type

### Triggering Completion

- **Automatic** — Appears as you type
- **Manual** — Press **Ctrl+Space** (Cmd+Space on Mac)
- **Smart** — Press **Ctrl+Shift+Space** for type-aware suggestions

---

## Hover Information

Hover over symbols to see documentation and type information:

### Hover Content

| Element | Information Shown |
| --- | --- |
| **Variable** | Type, scope, current value (in debug) |
| **Method** | Signature, parameters, return type, documentation |
| **Property** | Type, access level, documentation |
| **Class** | Full name, package, documentation |
| **Keyword** | Language reference link |

### Example Hover

```javascript
function getUser(required numeric id)
Returns: User
Throws: UserNotFoundException

Retrieves a user by ID from the database.

Parameters:
  id - The unique user identifier
```

---

## Go to Definition

Navigate to where a symbol is defined:

**Methods:**
- **Cmd+Click** (Ctrl+Click) on the symbol
- **Cmd+B** (Ctrl+B) with cursor on symbol
- **Navigate → Declaration** from menu

**Works for:**
- Variables → Declaration location
- Methods → Method definition
- Classes → Class file
- Properties → Property declaration

---

## Find References

Find all usages of a symbol:

**Methods:**
- **Alt+F7** (Option+F7) with cursor on symbol
- **Navigate → Usages** from menu
- Right-click → **Find Usages**

**Results show:**
- All locations where the symbol is used
- Grouped by file
- Preview of each usage

---

## Code Actions

Quick fixes and refactoring suggestions appear as lightbulb icons 💡:

### Common Code Actions

| Action | Description |
| --- | --- |
| **Add Import** | Import missing class or function |
| **Create Method** | Generate stub for undefined method |
| **Create Variable** | Declare undefined variable |
| **Fix Type** | Convert to expected type |
| **Remove Unused** | Delete unused imports or variables |
| **Extract Method** | Refactor selection into new method |
| **Inline Variable** | Replace variable with its value |

### Triggering Code Actions

- Click the lightbulb icon 💡 in the gutter
- Press **Alt+Enter** (Option+Enter)
- Right-click → **Show Context Actions**

---

## LSP Configuration

Configure LSP behavior in **Settings → Languages & Frameworks → BoxLang**:

| Setting | Description |
| --- | --- |
| **LSP Module** | Download, change, or delete the LSP module |
| **Max Heap Size** | Memory allocation for LSP server (64-8192 MB) |
| **LSP Modules** | BoxLang modules to install in LSP home |
| **LSP JVM Args** | Additional JVM arguments |

### Restarting the LSP

If the LSP becomes unresponsive:

1. Open **Settings → Languages & Frameworks → BoxLang**
2. Click **Change** next to LSP Module
3. Select the same version to restart
4. Or use **File → Invalidate Caches → Restart IDE**

---

## Troubleshooting LSP Issues

### LSP Not Starting

**Symptoms:** No diagnostics, no completions, structure view empty

**Solutions:**
1. Check LSP is installed in settings
2. Verify Java 21+ is configured
3. Check IDE logs: **Help → Show Log in Finder/Explorer**
4. Restart the IDE

### Slow Completions

**Symptoms:** Delay before completion popup appears

**Solutions:**
1. Increase LSP heap size (e.g., 1024 MB)
2. Close unused projects
3. Exclude large directories from indexing

### Missing Diagnostics

**Symptoms:** Errors not reported in editor

**Solutions:**
1. Check file is recognized as BoxLang (icon in tab)
2. Verify LSP is running (check settings status)
3. Restart the LSP module

---

## Related Pages

- [Settings Reference](settings-reference.md)
- [Runtime Management](runtime-management.md)
- [Debugging](debugging.md)
